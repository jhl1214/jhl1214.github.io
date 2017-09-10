---
layout: post
title:  "Jekyll과 Github로 블로그 만들기"
author: Junho Lee
categories: Develop
tags:	jekyll github blog
cover:  "/assets/images/20170910_01.jpg"
---

[Jekyll](http://jekyllrb.com)은 마크다운을 베이스로 정적 HTML 웹사이트를 만들어주는 툴이다. Ruby 스크립트로 구현되어 있지만 ruby를 전혀 몰라도 블로그를 구성하는데 전혀 문제가 되지 않는다. 또한 [Jekyll Themes](http://jekyllthemes.org)에서 이미 구현되어 있는 다양한 테마를 사용하고 CSS를 수정하여 나만의 테마로 커스터마이징 역시 가능하다.

이 포스트는 [GitHub Pages](https://pages.github.com)에 Jekyll과 테마를 적용하며 겪은 삽질들을 기록해두고자 작성하게 되었다.

## 설치하기에 앞서..
맥북 사용자라면 기본적으로 Ruby가 모두 설치되어 있다. 다만 Jekyll을 설치하기 위해서는 ruby 버전이 지원되는지 확인이 우선적으로 필요하다.

```
ruby -v
ruby 2.0.0p247 (2013-06-27 revision 41674) [universal.x86_64-darwin13]
```

별도로 루비를 설치하거나 한적이 없다면 뒷 부분은 OS 버전마다 조금씩 차이날 수 있지만 기본적으로 **ruby 2.0** 이 설치되어 있다. Jekyll은 ruby 2.1 이상부터 지원이 되기 때문에 우선 지원하는 버전의 ruby를 설치해보도록 하자.

```
\curl -L https://get.rvm.io | bash -s stable --ruby
```

먼저 RVM 설치를 위해 위의 명령을 터미널에 복사하여 수행시키자.
RVM 설치가 완료 되었다면 ruby interpreter 를 설치해야 한다.

```
rvm install 2.1.0 --autolibs=enable
```

역시 위의 명령어를 복사하여 터미널에서 수행시키면 ruby interpreter가 설치된다. Interpreter 설치가 된 것을 확인 한 후에 

```
source /Users/{본인계정}/.rvm/scripts/rvm
```

rvm을 적용시키고 `rvm use 2.1.0` 을 수행해준다.

```
ruby -v
ruby 2.1.0p76 (2014-02-24 revision 45161) [x86_64-darwin13.0]
```

다시 ruby의 버전을 확인해보면 **ruby 2.1.0**으로 정상적으로 노출 되는 것을 확인할 수 있다.

## Jekyll 설치
이제 본격적으로 **jekyll**을 설치해보도록 하자.
터미널에 다음과 같은 명령으로 jekyll을 설치한다.

```
sudo gem install jekyll
```

만약 이 과정에서 에러가 발생한다면 대부분의 경우에는 `sudo gem update —system` 명령어를 통해 업데이트 후 다시 시도해보면 해결할 수 있다.

이제 로컬 디렉토리에 Jekyll을 설치하고 GitHub page와 연동을 해야 한다. 일반적으로 GitHub page는 `{깃허브계정명}.github.io` 와 같은 형태로 주소를 생성하게 된다. 

## Jekyll 생성 및 GitHub 연동
먼저 터미널에 아래와 같은 명령어를 수행하여 Jekyll로 하여금 기본적인 파일을 포함한 디렉토리를 생성하도록 한다.

```
jekyll new {깃허브계정명}.github.io
```

생성이 완료 되었다면 해당 디렉토리 내부로 이동하여 아래의 명령어를 통해 로컬 환경에서 정상적으로 작동하는지 확인해 볼 수 있다.

```
jekyll serve --watch
```

Jekyll이 디렉토리에 있는 설정 및 마크다운 파일들을 정적 페이지로 변환하고 작업이 완료 되면 서버가 실행되고 있다는 문구를 터미널에서 확인할 수 있다. 서버가 정상적으로 수행되었다면 브라우저를 열어 `localhost:4000` 을 통해 Jekyll이 잘 나타나는지 확인해 볼 수 있다.

[image:9804C433-97B6-4812-BE9B-C71EBE57389E-12150-00001DAE07A8787C/20170910_02.png]

이제 Github 레포지토리를 생성해야 한다. Github 레포지토리의 이름을 위에서 사용한 `{깃허브계정명}.github.io` 로 생성한다.

그 후 다시 터미널로 돌아와 jekyll에서 생성된 디렉토리에 git 설정을 해주도록 한다.
Git 사용이 익숙하지 않은 사용자들을 위해 아래에 커맨드 명령을 적어놓았다.

```
git init
git remote add origin git@github.com:{깃허브계정명}/{깃허브계정명}.github.io.git
git add *
git commit -m "Initial jekyll setup"
git push origin master
```

Github에 모든 내용을 푸시 하였다면 이제 `{깃허브계정명}.github.io` 로 브라우저를 통해 접근해보면 정상적으로 페이지가 노출 되는것을 확인할 수 있다.

## 테마 적용
WIP

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
[liquid]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
