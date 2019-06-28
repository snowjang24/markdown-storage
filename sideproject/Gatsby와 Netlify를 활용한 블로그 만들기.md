# Gatsby와 Netlify를 활용한 블로그 만들기

## Gatsby에 대하여

### 나의 블로그 연대기

처음에 블로그를 시작했을 때는, [jekyll](https://jekyllrb-ko.github.io/)을 사용하여 블로그를 만들었다. 그러다 얼마 지나지 않아 HEXO와 VEXO테마로 넘어가게 되었는데, 한창 Node와 Vue를 공부해야지 할 때였다. 
이번에 Gatsby로 넘어오게 된 이유도 같다. React를 공부하다 보니 React를 사용해서 나만의 블로그를 만들어보고 싶어졌다. 이번에는 테마를 최소화하여 진짜 **나만의 블로그**를 만들어 보려 한다.

![image-20190616131542912](Gatsby와 Netlify를 활용한 블로그 만들기/image-20190616131542912-0658542.png)



### Gatsby란?

Gatsby는 

![image-20190616002109786](Gatsby와 Netlify를 활용한 블로그 만들기/image-20190616002109786-0612069.png)

gatsby에서는 gatsby-cli를 제공하고 있으며, 이를 이용하면 쉽게 설치하고 실행할 수 있다.

```bash
npm install --global gatsby-cli
gatsby new [프로젝트 폴더명]
cd [프로젝트 폴더명]
gatsby develop
```

* `gatsby develop` 명령어를 통해 development 서버를 시작한다. 인터넷에 publish하는 것이 아닌 로컬 환경에서 서버를 실행한다.

빌드가 성공적으로 끝나면 다음과 같은 링크 두 개를 볼 수 있다.

![image-20190616135518723](/Users/soonho/project/markdown-storage/sideproject/Gatsby와 Netlify를 활용한 블로그 만들기//image-20190616135518723.png)

