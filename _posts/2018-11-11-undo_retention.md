---
layout: customize-posts
title: "undo_retention 이슈 및 작업 정리"
description: "Oracle Undo Retention에 관련하여 접할 기회가 있어 작성하였으며, 회사내에서 작업 간 이슈사항이 발생하여 추가 작업 하였습니다. 간단하게 절차식으로 구성하였으며 추가 궁금증은 구글검색이 필요합니다."
category:
    - DB
tags:
    - DB
published: true
---

#### 작업은 Toad For Oracle Tool을 사용하여 진행하였습니다.

## UNDO_RETENTION 정의
*   일관성 읽기를 위해 제공되는 Undo 데이타의 보유 기간을 결정합니다.
*   초기화 파일에서 설정하거나, ALTER SYSTEM 명령을 사용하여 동적으로 수정할 수 있습니다.
*   이 parameter는 초 단위로 지정됩니다. 기본값은 900초이며, 이는 Undo 데이타를 15분 동안 보유합니다.
*   UNDO_RETENTION을 설정한 후에도 UNDO 테이블스페이스의 크기가 너무 작으면 지정한 시간 동안 Undo 데이타가 보유되지 않습니다.
*   UNDO_RETENTION 파라미터는 현재 Undo 테이블스페이스에 UNDO_RETENTION 기간 동안 발생하는 모든 트랜잭션을 수용할 수 있을 만큼 충분한 커야 합니다.
*   대용량 이관작업이 있을때 undo tablespace가 비약적으로 상승이 된다.  보통 이럴때는 여분의 datafile를 하는 방법이 가장 쉽지만 datafile이 부족하여 추가가 불가할 경우 undo tablespace를 비워 상승하는 undo를 초기화(?) 시켜주면 임시적으로나마 undo tablespace가 100%에 도달하여 성능적 이슈가 발생하는것을  방지할 수 있다.

## UNDO_RETENTION 작업을 한 이유
UNDO_RETENTION을 하게된 이유는 대용량 DATA 이관 작업 중 비약적인 UNDO Tablespace 사이즈 증대로 인해 작업을 하게되었다.
기존에 추가한 DataFile의 부족으로 긴급하게 UNDO_RETENTION을 하기로 정했다.

## UNDO_RETENTION 절차

1. 임시 undo tablespace 생성
```sql
    create undo tablespce undotbs_temp datafile '~/~.dbf' size 1G;
```
2. 임시로 만든 tablespace 시스템 undo tablespace로 지정
```sql
    alter system set undo_tablespace=undotbs_temp scope=spfile;
        -- spfile or pfile 확인 필요
        select * from v$parameter where name like '%pfile%';
        
        -- undo_retention 임계시간 설정
        --undo tablespace 변경 지정을 하기 위해서는 트랜잭션이 없어야 한다.
        > alter system set "undo_retention" = 0 scope=memory; 
```
3. 기존에 비정상 적으로 확장된 undo tablespace drop
```sql
    -- tablespace에 추가된 datafile 제거 X
    drop tablespace undotbs1;
    -- tablespace에 추가된 datafile 제거 O
    drop tablespace undotbs1 including contents and datafiles;
```
4. 새로 사용할 undo tablespace를 생성
```sql
    create undo tablespce undotbs1 datafile '~/~.dbf' size 1G;
```
5. 새로 만든 undo tablespace를 시스템 undo tablespace로 지정
```sql
    alter system set undo_tablespace=undotbs1;
```
6. 임시로 만든 undotbs_temp drop
```sql
    -- os의 해당 계정으로 접색해서 imsi_undotbs1 테이블스페이스에 속판  파일 rm으로 삭제
    -- 온라인 DB의 경우 접속한 Tool의 세션을 모두 제거하면 *.dbf reuse 가능
    drop tablespace undotbs_temp--including contents and datafiles;
```
7. **_3번_** 의 drop tablespace undotbs1;의 쿼리를 사용했을 경우
```sql
    -- 부족하던 undo tablespace에 붙여둔 datafile를 including contents and datafiles를 하지 않았을때 아래 쿼리로 재사용 가능
    alter tablespace undotbs_temp add datafile '~/~dbf' reuse;
```
## 참고 undo retention 확인 쿼리
```sql
    select * from v$parameter where name = 'undo_retention';
```

## 참고 undo retention spfile, pfile
*   pfile의 경우 리스너, 인스턴스 기동 간 init.ora에 value로 지정된 TBS의 값을 읽어 오기 때문에 TBS를 변경한다면 init.ora 수정이 필요하다. TBS변경 후 설정을 하지 않을경우 리스너가 올라오지 않는다.

## UNDO_RETENTION 작업 간 이슈사항
위의 절차 중 2번 에서 undo tablespace가 변경 적용이 되지 않았다.
이유를 확인해 보니 온라인 중 트랜잭션이 지속적으로 들어오고 있어서 적용이 되지 않았었다.
추후 undo retention 작업을 하게 될 경우 가급적이면 live된 service는 다운 후 진행하는 게 정신건강에 좋을 것으로 판단된다...

위의 절차 중 3번 에서 "drop tablespace undotbs1;"을 사용하여 진행하였다.
진행에 있어 기대한 효과는 기존에 undotbs1에서 사용중인 datafile을 reset하여 undotbs_temp에 추가하는것이 목표였다.
하지만 undotbs1에서 사용하였던 datafile을 찾지를 못하는 상태가 되었다.
구글링을 통하여 확인을 해보니... Tool로 접속한 session을 제거하라는 가이드를 찾게 되었고, session을 끊고 다시 접속하여 확인을 해보니 reuse를 할 수 있게 되었다...
(작업 절차의 7번 에 해당하는 내용임)