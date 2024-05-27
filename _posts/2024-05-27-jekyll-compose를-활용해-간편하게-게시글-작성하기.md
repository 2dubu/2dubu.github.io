---
layout: post
title: jekyll-compose를 활용해 간편하게 게시글 작성하기
date: 2024-05-27 01:01 +0900
description: jekyll-compose를 통해 보다 쉽게 게시글을 작성해보자!
image: /assets/img/posts/20240527/thumbnail.png
pin:
category: [Blog]
tags: [github.io, jekyll, chirpy, jekyll-compose]
---

Jekyll 기반의 블로그를 만들어 배포했다면, 글을 작성하는 방법은 다음과 같습니다.

1. markdown 파일을 `_posts` 폴더에 생성합니다. 

2. 파일명은 `yyyy-mm-dd-title.md` 형식으로 생성해야 합니다.

3. 생성한 파일의 상단에 다음과 같이 글의 여러 설정 값들을 기입해야 합니다.

   - ```markdown
     ---
     layout: post
     title: this is title!
     date: 2024-05-27 01:01 +0900
     description: this is description!
     image: /assets/img/posts/thumbnail.png
     pin: false
     category: [Blog]
     tags: [github.io, jekyll, chirpy, jekyll-compose]
     ---
     ```
     
     

글을 쓰기 위해 다음과 같은 작업을 매번 반복하는 것은 매우 번거롭습니다. 반복작업을 줄이기 위해 **jekyll-compose**를 사용하여 포스팅을 보다 빠르게 진행해 봅시다.



## jekyll-compose?

[jekyll-compose](https://github.com/jekyll/jekyll-compose)는 포스트나 페이지 초안을 생성하는 하위 명령어를 추가해,  Jekyll 글 작성을 간소화 시켜주는 Ruby 기반의 plugin 입니다. 

이 외에도 많은 plugin들이 있으니 필요하다면 [이곳](https://jekyllrb-ko.github.io/docs/plugins/your-first-plugin/)을 확인해보시면 좋을 것 같습니다.

<br/>

## jekyll-compose 설치

jekyll 블로그의 root directory에 접근해 `Gemfile` 의 하단에 다음과 같은 `gem` 코드를 추가합니다.

```console
$ cd /.../username.github.io # root directory 접근
```

{: file='Gemfile'}

```
gem 'jekyll-compose', group: [:jekyll_plugins]
```

jekyll-compose 플러그인을 설치합니다.

```console
$ bundle
```

<br/>

## 명령어 기본 설정

이제 jekyll-compose plugin을 통해 게시글을 생성할 수 있는데, 그 전에 게시글에 기본 정보를 설정합니다. `_config.yml` 파일을 열어 아래 코드를 추가해줍니다.

{: file='_config.yml'}

```yaml
jekyll_compose:
  auto_open: false # 게시글 생성 시 파일 자동 열림 여부를 설정합니다
  default_front_matter:
    posts:
      description: # post 파일 생성 시 기본적으로 넣고 싶은 내용이 있다면 작성합니다
      category:
      tags:
```
auto_open 기능이 제대로 동작하기 위해서는 게시글 작성에 사용할 에디터를 설정해줘야 합니다. 저는 auto_open 기능을 꺼두었지만, 설정 방법은 다음과 같습니다.

```console
$  vi ~/.zshrc
```

다음 코드를 추가해줍니다.

```shell
export JEKYLL_EDITOR=code # 사용하는 에디터를 설정합니다
```

```console
$ source ~/.zshrc
```

{: .prompt-info }

>만약 vscode를 사용하신다면 vscode를 터미널에서 인식하려면 별도의 과정이 필요합니다.  
>vscode 진입 - View - Command Palette - “shell” 검색 - Shell Command: Install ‘code’ command in path

<br/>

## 파일 생성

이제 아래의 명령어를 통해 설정한 형태로 글의 초안 markdown 파일을 자동으로 생성할 수 있다.

```console
$ bundle exec jekyll post "post title"
```

다른 명령어

```
  draft      # Creates a new draft post with the given NAME
  post       # Creates a new post with the given NAME
  publish    # Moves a draft into the _posts directory and sets the date
  unpublish  # Moves a post back into the _drafts directory
  page       # Creates a new page with the given NAME
  rename     # Moves a draft to a given NAME and sets the title
  compose    # Creates a new file with the given NAME
```

<br/>

## alias 설정

명령어가 너무 기므로 `alias` 를 통해 약어를 설정해 사용할 수 있습니다.

```console
$ vi ~/.zshrc
```

쉘 설정을 열어 다음 코드를 추가해줍니다.

```shell
alias post='cd ~/.../username.github.io && bundle exec jekyll post'
```

```console
$ source ~/.zshrc
```

바뀐 내용을 적용시킵니다.

<br/>

이제 아래의 명령어를 통해 더 간편한 글 생성이 가능해졌습니다!

```console
$ post "post title"
```



## 마무리

본 글은 [Koesnam](https://10kseok.github.io/posts/easy-to-make-default-mdfile-to-use-jekyll-compose/#1-jekyll-compose-%EC%84%A4%EC%B9%98)님의 포스트와 [공식 문서](https://github.com/jekyll/jekyll-compose)를 참고해 작성했습니다.

{: .prompt-info }

> 포스트에 틀린 부분이 존재할 수 있습니다. 발견 시 댓글로 알려주시면 확인 후 수정하도록 하겠습니다. :)
