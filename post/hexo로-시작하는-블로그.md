---
title: HEXO와 Github page로 시작하는 블로그
date: 2018-12-27 20:16:57
tags: ["hexo", "blog"]
---

# HEXO와 Github page를 활용한 블로그

## 개요

기존의 티스토리 혹은 네이버 블로그를 이용하여 개발자 블로그를 시작하는 경우가 많다. 네이버나 티스토리의 경우 블로그 생성이 쉬우며 정형화되어 큰 세팅이 필요없지만 글을 작성할 때 작성한 md문서를 직접 옮겨 써야하는 귀찮음이 있다. 또한 나만의 개성을 가진 블로그 꾸미기가 어렵기 때문에 이러한 단점들을 보완해줄 HEXO를 이용하여 블로그를 생성하려한다.
<br>

## 시작

### 1. git 레퍼지토리 생성

다음과 같이 이름을 설정하여 git 레퍼지토리를 생성한다.

> 레퍼지토리 이름 : 계정이름.github.io
> 블로그의 주소는 `https://계정이름.github.io`로 생성된다.

<br>

### 2. Hexo 설치

npm을 통해 hexo를 설치한다.

```bash
npm install -g hexo-cli
```

<br>

### 3. hexo 블로그 생성

`hexo init 블로그이름`으로 hexo 블로그를 생성하고 필요한 모듈을 설치한다. 이때, `블로그이름`은 그냥 원하는 걸로 해도 상관없다.

```bash
hexo init 블로그이름
cd 블로그이름
npm install
```

<br>

### 4. Hexo 블로그를 Github에 연동

별도의 git명령어 없이도 자동으로 업로드를 hexo가 대신 해준다.
이를 위해선 git을 연동시켜야한다. 앞서 생성했던 `블로그이름`폴더로 가서 `_config.yml`을 열어본다.
아래와 같이 간단한 `title`, `subtitle`, `description`을 설정한다.
이때, `title`의 경우 블로그의 이름으로 설정된다.

```html
title: SnowJang Dev 
subtitle: Snow Jang front-end and ios developer blog
description: Development blog
```

그런 다음 git을 연동해야 하는데, 아래와 같이 앞에 생성 했던 레퍼지토리대로 자신의 깃 계정 이름을 넣어 수정 완료하면 된다.

```html
# Deployment 
## Docs: https://hexo.io/docs/deployment.html 
deploy: 
  type: git
  repo: https://github.com/snowjang24/snowjang24.github.io.git
```

hexo에서 github에 업로드하기 위해서는 다음과 같은 `npm` 모듈이 필요하다. 생성한 블로그 폴더 경로로 이동하여 다음과 같은 명령어를 입력하면 된다.

```bash
npm install hexo-deployer-git --save
```

<br>

### 5. 블로그 테마 설정

hexo의 장점은 다양하고 커스터마이징 가능한 테마를 쉽게 설치 가능하다는 점인데 흔히 쓰는 `clean blog`테마 말고 필자는 `vexo`라는 `vue`공식 document를 참고하여 만들어진 테마를 사용하였다.

먼저 자신의 블로그 폴더로 이동하여 아래의 순서로 명령어를 입력한다.

```bash
git clone https://github.com/yanm1ng/hexo-theme-vexo.git themes/vexo
cp -R themes/vexo/_source/* source/
```

그런 다음 `_config.yml`을 열어 테마를 수정하고, 저장한다.

```html
themes: vexo
```

만약 블로그 테마의 업데이트가 필요한 경우 다음과 같은 명령어를 통해 업데이트 한다.

```bash
cd themes/vexo
git pull
```

vexo의 포스트 기본 header의 경우 다음과 같으며 tags는 아래와 같이 입력하거나 `['Movies','Life']`로 입력하면 자동으로 생성된다.

```html
---
title: "Hello World"
date: 2016-06-10 23:00
banner: your-banner-link.jpg
tags:
  - Movies
  - Life
---
```

<br>

### 6. 글 작성(포스트 생성)

다음과 같은 명령어를 통해 쉽게 글을 작성할 수 있다.

```bash
hexo new "오늘의 포스팅"
```

처음 생성 시 다음과 같은 모양으로 header가 생기는데, 이는 표출되는 정보가 아닌 제목이나 날짜, 태그 등 기타 포스팅 될 글에 대한 정보를 담고 있다.

```html
title: "오늘의 포스팅" 
date: 2018-12-27 23:00
```

<br>

### 7. 로컬 확인

작성된 글은 로컬에서 서버를 구동시키면, 브라우저를 통해 확인할 수 있다. 다음과 같이 서버를 구동시키고 [http://localhost:4000](http://localhost:4000)로 접속하면 서비스할 블로그를 확인할 수 있다.

```bash
hexo server
```

<br>

### 8. Hexo 빌드 후 Github에 업로드

글을 생성하면 `markdown`파일로 생성된다. 이를 github page에 맞게 재생성하여 `html`로 바꿔 줘야 하는데 이때 사용하는 명령어는 다음과 같다.

```bash
hexo generate 또는 hexo g
```

이렇게 생성을 하고 추가로 github에 업로드까지 해줘야 실제 블로그에서 업데이트 된다. 이때 명령어는 다음과 같다.

```bash
hexo deploy 또는 hexo d
```

위의 빌드와 업로드를 한번에 하는 명령어는 다음과 같다.

```bash
hexo g --d
```

<br>

## 결론

HEXO를 설치하는것도 세팅하는 것도 정말 편하고 앞으로 글을 포스팅 할 일이 많을 것 같은데 쉽고 편하게 할 수 있을 것 같다. 아직은 테마를 추가하고 추가적인 커스텀을 하지 않았기 때문에, 흔한 형태의 블로그이지만 차차 나만의 블로그스럽게 수정해야겠다.

<br>

---

>  ** Reference**
>
>  * [vexo 테마](https://github.com/yanm1ng/hexo-theme-vexo)
