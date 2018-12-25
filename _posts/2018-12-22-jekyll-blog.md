---
layout: customize-posts
title: "지킬(Jekyll) 깃허브(github) 블로그 만들기"
date: 2018-12-21
description: "지킬(Jekyll)을 이용하여 깃허브(github)에 정적(static) 블로그 만들기 입니다. 구축 및 사용 환경은 mac os 에서 작성하였습니다. 또한 블로그 구축, 커스터마이징을 간단하게 어느 설정 파일에서 수정 및 추가하면되는지 확인 하실 수 있으시며 내부기능은 github 댓글 API utterances 추가하였습니다."
keywords:
    - jekyll
    - 지킬
    - github
    - 깃허브
    - blog
    - 블로그
category:
    - etc
tags:
    - Jekyll
    - github
published: true
sitemap: 
changefreq: daily
priority: 1.0
---

>#### Mac OS 를 활용하여 구축하였습니다.

## Github Blog(Jekyll) 만들게 된 이유

기존에는 티스토리 블로그를 사용하고 있었지만 요즘들어 Github을 통해 Blog를 만들고 싶은 가장큰 이유는 **불안감**이 있었다.   
글재주가 없지만 블로그를 하는 목적은 개인기록을 하기 위해서였고, 기존에 사용하던 형태의 블로그 들은 기록하여 올리기가 쉽지만 **백업**이라는 문제가 항상 불안하게 만들었다.  
기껏 작성다했는데 이게 어떠한 이슈로 인해 데이터가 날라간다면 복구할 방법이 없기 때문이다.  
따로 백업해두면 되긴하지만 귀찮음은 존재하기에..  

그래서 문득생각한 것 중 하나가 AWS EC2를 활용해 DB 연결하여 백업시킬까?도 생각해봤지만 언젠가는 무료티어가 만료가 되고 과금이 발생하기에 깔끔하게 접게 되었습니다. 
 
그러다 주변 친구의 추천과 구글검색을 통해 알게된 *.github.io는 나의 모든 **걱정(백업)**과 **조건(무료)**을 만족시켜주었다 ㅠㅠ  
로컬저장소, 원격저장소를 오고가며(?) 사용을 해야하기에 어쩔수없이 백업이 되고 더군다나 무료!! 과금없이 불안 없이 개인적으로 기록할 공간을 만들 수 있기에 바로 만들기로 마음 먹었다.  
Github Blog를 구축할 기반언어도 다양하게 존재하지만 나는 그중 **Jekyll**을 사용하기로 하였다.  
이유는 단순했다 theme가 이뻐보였고, macbook (jekyll은 ruby기반입니다. - mac은 기본적으로 ruby를 지원함)이 있어서였다.

#### 아래부터는 구축까지 한 과정과 진행간의 이슈가있던 내용을 정리해 두려한다.

## Jekyll 구축 과정

시작하기전에 **bundler**와 **jekyll**설치가 필요하다 
```java
➜  ~ gem install bundler
/System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- rubygems/core_ext/kernel_warn (LoadError)
  from /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require'
  from /Library/Ruby/Site/2.3.0/rubygems.rb:1395:in `<top (required)>'
  from <internal:gem_prelude>:4:in `require'
  from <internal:gem_prelude>:4:in `<internal:gem_prelude>'
```
??시작 부터에러가 떳다... root권한으로 안해서 그런가 싶어 아래 명령어로 했다.

```java
➜  ~ sudo gem install bundler jekyll
Password:
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /usr/bin directory.
```
...구글링이 필요하다..  
 위의 error log를 통해 검색한 결과 **rvm(Ruby Version Manager)**이라는 키워드가 나왔다. 아래 명령어를 통해 설치하였다.

```java
➜  ~ \curl -L http://get.rvm.io | bash -s stable
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   194  100   194    0     0    291      0 --:--:-- --:--:-- --:--:--   291
100 24593  100 24593    0     0  14893      0  0:00:01  0:00:01 --:--:--  133k
Downloading https://github.com/rvm/rvm/archive/1.29.6.tar.gz
Downloading https://github.com/rvm/rvm/releases/download/1.29.6/1.29.6.tar.gz.asc
Found PGP signature at: 'https://github.com/rvm/rvm/releases/download/1.29.6/1.29.6.tar.gz.asc',
but no GPG software exists to validate it, skipping.
Installing RVM to /.rvm/
    Adding rvm PATH line to /.profile /.mkshrc /.bashrc /.zshrc.
    Adding rvm loading line to /.profile /.bash_profile /.zlogin.
Installation of RVM in /.rvm/ is almost complete:

  * To start using RVM you need to run `source /.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
```
하단에 설치 후 적용과 터미널 리부팅이 필요하다는 문구 확인.!  
rvm 설치 후 적용과 재부팅 진행하여 ruby를 설치하여 버전을 확인해보자.
```java
➜  ~ source /.rvm/scripts/rvm

➜  ~ rvm install 2.5.3
````` 중략 `````
ruby-2.5.3 - #generating global wrappers - please wait
ruby-2.5.3 - #gemset created /.rvm/gems/ruby-2.5.3
ruby-2.5.3 - #importing gemsetfile /.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.5.3 - #generating default wrappers - please wait
ruby-2.5.3 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.5.3 - #complete
Ruby was built without documentation, to build it run: rvm docs generate-ri

➜  ~ ruby -v
ruby 2.5.3p105 (2018-10-18 revision 65156) [x86_64-darwin18.2.0]
```

rvm 설치 완료 후 **bundler**와 **Jekyll**을 설치하자
```java
➜  ~ gem install bundler jekyll
Fetching: bundler-1.17.2.gem (100%)
Successfully installed bundler-1.17.2
````` 중략 `````
Parsing documentation for jekyll-3.8.5
Installing ri documentation for jekyll-3.8.5
Done installing documentation for public_suffix, addressable, colorator, http_parser.rb, eventmachine, em-websocket, concurrent-ruby, i18n, rb-fsevent, ffi, rb-inotify, sass-listen, sass, jekyll-sass-converter, ruby_dep, listen, jekyll-watch, kramdown, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, jekyll after 44 seconds
26 gems installed
```
설치 완료 후 본인 github에 repository 생성하자 생성 규칙은 githubId.giyhub.io 로 만들어야 한다.  
repository생성 하면 원격저장소는 완료가 되며, 로컬저장소에 clone을 받자
```java
➜ git clone "clone url"
```

Clone한 로컬저장소에 **Jekyll**로 신규로 만들어보자.
```java
➜  blog jekyll new sksggg123.github.io
Running bundle install in /git/blog/sksggg123.gitghub...
  Bundler: The dependency tzinfo-data (>= 0) will be unused by any of the platforms Bundler is installing for. Bundler is installing for ruby but the dependency is only for x86-mingw32, x86-mswin32, x64-mingw32, java. To add those platforms to the bundle, run `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java`.
  Bundler: Fetching gem metadata from https://rubygems.org/...........
  Bundler: Fetching gem metadata from https://rubygems.org/.
  Bundler: Resolving dependencies...
  Bundler: Using public_suffix 3.0.3
````` 중략 `````
  Bundler: Installing minima 2.5.0
  Bundler: Bundle complete! 4 Gemfile dependencies, 29 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in /git/blog/sksggg123.github.io
```

변환이 완료되면 기본적인 Jekyll의 구조는 아래와 같이 생성이 된다.  
* 404.html
* Gemfile
* Gemfile.lock
* _config.yml
* _posts
* about.md
* index.md

>**bundle exec jekyll serve** 명령어를 통해 로컬에서 블로그를 띄워보자!!  

접속은 http://localhost:4000 으로 접속을 하면 default 페이지를 확인 할 수 있다.  
본인 원격저장소로 커밋을 하면 외부에서 접속하여 확인이 가능하다.  
```java
git add .
git commit -m "commit message"
git push -u original master

완료 후 브라우저창에 [username].github.io 치면 로컬에서 본 화면을 볼 수 있게된다.
```
이렇게 하면 기본적인 블로그 구축은 완료가 된다.  
이제 다음으로는 theme를 적용 해보자!

## minimal-mistakes theme 적용
minimal-mistakes 테마가 뭔가 심플하면서도 나한테는 마음에 들어 적용하기로 하였다.  
github에서 fork한 횟수도 가장 많은 테마이기도하고... 디자인이 괜찮았다.  

github fork하여 사용하지 않고 직접 [사이트](https://github.com/mmistakes/minimal-mistakes/releases)로 가서 아카이브 버전 url을 복사하여 tar.gz 파일을 받았다.  
나중에 다른테마 혹은 상위버전으로 바꿀때 형상관리가 이게 더 좋다고 판단하여 그러기로 하였다.  

clone한 로컬저장소 밖에 theme 디렉토리를 생성하여 아카이브 파일을 그쪽으로 받음.  
```wget "복사한 url"```
을 통하여 tar.gz 으로 내려 받아 ```tar -xvzf *.tar.gz```으로 압축해제 하였다.
위에 까지 압축을 풀면 아래와 같은 형식의 디렉토리 구조를 갖는다
```java
-rw-r--r--@  1 gwonbyeong-yun  staff    25M 12 21 17:54 4.14.1.tar.gz -- 압축파일 
drwxr-xr-x  17 gwonbyeong-yun  staff   544B 12 21 18:03 minimal-mistakes-4.14.1 -- 압축해제 디렉토리
drwxr-xr-x  25 gwonbyeong-yun  staff   800B 12 22 02:50 sksggg123.github.io -- 블로그 로컬저장소
```

다음으로는 본인 clone repository로 이동하여 rm -rf * 과감하게 실행하고,  
압축풀어둔 파일로 이동하여 불필요한 파일 삭제하자 파일 리스트는 아래와 같다.
* .editorconfig
* .gitattributes
* .github
* /docs
* /test
* CHANGELOG.md
* minimal-mistakes-jekyll.gemspec
* README.md
* screenshot-layout.png
* screenshot.png

_posts (생성한 블로그의 포스트 저장소), _draft (배포할 포스트의 로컬 저장소 - bundle exec jekyll serve 로 로컬 상태 확인할때 - 배포시 블로그의 등록은 되지 않는다) 위의 2개의 디렉토리가 없기에 theme디렉토리에 생성하여 준다.  

```mkdir _posts```  
```mkdir _draft```  

생성이 완료되면 아래의 명령어를 통해 블로그 로컬저장소로 **Copy**해오자  
```cp /tar압축해제한 디렉토리/. .../clone한 블로그 디렉토리/``` 를 통해 카피해오기

다음은 Gemfile 에서 아래와 같이 수정하자
```java
source "https://rubygems.org"

gem "jekyll", "~> 3.8.5"
#gem "minima", "~> 2.0"
gem "minimal-mistakes-jekyll"

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.6"
end

gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

gem "wdm", "~> 0.1.0" if Gem.win_platform?
```
수정완료 후 ```budle``` 명령어를 수행하여 설정 적용을 적용하자!

```bundle exec jekyll serve``` 를 통해 localhost:4000 으로 테마 적용 확인해보면 정상으로 바뀐 것을 알 수 있다.

## minimal-mistakes theme적용 후 설정 수정
테마 적용까지는 완료 되었다. 이제 자기 입맛에 맛게 커스텀하면 나만의 블로그가 생기게 된다.!!!  
나는 네비게이션, 카테고리, 태그 와 프로필 등... 아직 수정은 여기까지 밖에 안하였다.  
틈틈히 원하는 것이 있을때 변경하면 될 것 같다. 나는 아래와 같은 파일들을 만들고 수정하였다. 
```
수정추가한 파일 리스트
* 수정
  1. /_data/navigation.yml
  2. /_includes/archive-single.html
  3. _config.yml
* 추가
  1. /_layouts/customize-posts.html
  2. /_pages/about.md
  3. /_pages/category-archive.md
  4. /_pages/tag-archive.md  
  5. /assets/images/* (프로필 등...)
```
우선 네비게이션 설정이다.  
설정은 아래 파일을 수정해야 한다.  
```/_data/navigation.yml``` 의 파일을 아래와 같이 수정하였다.  
```yaml
# main links
main:
#  - title: "Github"
#    url: https://github.com/sksggg123
#  - title: "Sample Posts"
#    url: /year-archive/
#  - title: "Sample Collections"
#    url: /collection-archive/
#  - title: "Sitemap"
#    url: /sitemap/
  - title: "tag"
    url: /tags/
  - title: "Category"
    url: /categories/
  - title: "About"
    url: /about/
```
위에까지만 설정하고 ```bundle exec jekyll serve```하여 확인해보면 상단에 링크들이 생기는 것을 확인할 수 있다.  
하지만 링크를 클릭하면 404가 뜰 것 이다. _pages라는 디렉토리가 필요하다.  
```mkdir _pages``` 디렉토리를 생성하자  

/_pages/about.md

```yaml
---
permalink: /about/
title: "About"
excerpt: "Minimal Mistakes is a flexible two-column Jekyll theme."
layouts_gallery:
  - url: /assets/images/mm-layout-splash.png
    image_path: /assets/images/mm-layout-splash.png
    alt: "splash layout example"
  - url: /assets/images/mm-layout-single-meta.png
    image_path: /assets/images/mm-layout-single-meta.png
    alt: "single layout with comments and related posts"
  - url: /assets/images/mm-layout-archive.png
    image_path: /assets/images/mm-layout-archive.png
    alt: "archive layout example"
#last_modified_at: 2018-11-21T14:49:33-05:00
toc: true
---
>## History..
```

/_pages/categoryarchive.md

```yaml
---
title: "Posts by Category"
layout: categories
permalink: /categories/
author_profile: true
toc: true
---
```

/_pages/tag-archive.md

```yaml
---
title: "Posts by Tag"
permalink: /tags/
layout: tags
author_profile: true
---
```

로컬페이지를 재시작하여 확인해보면 링크 클릭 스 랜딩이 되고 카테고리와 태그별로 구분되어 나오게 된다.  
```/_include/``` 하위에 html 문서들이 있다. 이 템플릿 들을 통하여 페이지가 구성이되고 본인 마음에 안들면 해당 파일을 찾아 수정을 하면 본인만의 블로그 페이지가 된다.!

## 댓글 기능! (utterances - github issue 관리 기능 API)
기본적으로 사용가능하게 해주는 댓글 기능들이 되게 많았지만, 나는 깃헙의 이슈관리 해주는 기능을 사용해보려고 한다.  
utterances기능을 사용하기전에 추가해줘야되는 부분이 있다.
* 신규 블로그 코멘트 관리하는 repository 생성
* _config.yml 수정
* _utterances.html 수정
repository 는 아래와 같이 있어야 한다.  
![repository](/assets/images/upload/Your_Repositories.png)

```_config.yml``` 파일을 아래와 같이 수정해보자.  
```yaml
comments:
  provider               : "utterances" # false (default), "disqus", "discourse", "facebook", "google-plus", "staticman", "staticman_v2", "utterances", "custom"
  utterances:
    theme                : # "github-light" (default), "github-dark"
```
```/_includes/commonts-providers/utterances.html``` 수정이 필요하다.  
```html
<script>
  'use strict';

  (function() {
    var commentContainer = document.querySelector('#utterances-comments');

    if (!commentContainer) {
      return;
    }

    var script = document.createElement('script');
    script.setAttribute('src', 'https://utteranc.es/client.js');
    // script.setAttribute('repo', '{{ site.repository }}');
    script.setAttribute('repo', 'username/comment-repository');
    script.setAttribute('issue-term', 'pathname');
    script.setAttribute('theme', '{{ site.comments.utterances.theme | default: "github-light" }}');
    script.setAttribute('crossorigin', 'anonymous');

    commentContainer.appendChild(script);
  })();
</script>
```
위에만 설정하고 로컬을 재빌드 해도 post한 글 하단에 comment기능이 보이지가 않는데 이거는 로컬환경이라 나오지가 않는거였다.  
원격저장소에 commit과 push를 하여 **username.github.io**로 접속하여 확인을 하면된다.  
코맨트를 작성하면 처음에는 error가 뜬다 그건 utterances APP을 설치해주면 된다. 설치는 [여기]()에서 All repository 선택하여 등록하면 끝난다.

실제로 작성하여 확인을 해보면 아래와 같이 이슈관리에 코맨트가 등록이 되는 걸 확인 할 수 있다.  
![comment](/assets/images/upload/testPage1__·_Issue__1_·_sksggg123_blog-comments.png)


## Githbu Blog 생성 부터 테마 적용 완료!
이렇게 기본적으로 페이지 생성을 완료 하였고, 사용을 하다가 본인이 원하는 테마가 있으면 바꿔도 보고 기존 테마에서 본인만의 기능을 추가하여도 괜찮을것 같다.!  
정리도 안된 글 보시느라 수고많으셨습니다. 혹시 잘못된 부분이 있거나 조언해주실 부분이 있으시면 피드백 주시면 감사하겠습니다. ^^
