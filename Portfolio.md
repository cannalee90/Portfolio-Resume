# 개인프로젝트

## Flashcard

**암기카드 React web app**

[Project Repository](https://github.com/cannalee90/flash-card)

### 사용한 기술

- `React`, `redux-observable`, `Gist`

### 기간 및 인원

- 기간: 2018/04 ~ 현재
- 담당: 기획 및 웹 프론트엔드

### 설명
- 암기카드를 React를 사용해서 웹 어플리케이션으로 구현 inspired by [jwasham/computer-science-flash-cards](https://github.com/jwasham/computer-science-flash-cards)
- 개인적인 기술부채를 청산하면서 진행
- `react-observable`, `react-router-v4`를 공부 및 실사용하기 위한 프로젝트
- 디펜던시를 최소화 하기 위해서 FE 프로젝트로 진행

### Trouble Shooting
- `Github API`에서는 웹 어플리케이션(browser only)의 경우 인증 토큰을 발급해주지 않는다.
  - firebase에서 제공하는 githubAuth API를 사용해서 해결.
  - refs [firebase github auth](https://firebase.google.com/docs/auth/web/github-auth)
  - fixed [#4](https://github.com/cannalee90/flash-card/pull/4)
  - fixed [dbb34ef4](https://github.com/cannalee90/flash-card/commit/dbb34ef4af2cb3bf2379c956dccff382db2a07f6)

- `redux-observable`
  - `redux-observable`을 사용할 경우, 비동기 액션이 언제 끝나는지 컴포넌트에서는 알 수가 없다.
  - `reducer`의 상태변화로만 알아채는 것이 하는것이 이상적이지만, 매번 이렇게 진행하기엔 사실상 어렵다.
  - `redux middleware`에서 `promise`를 래핑하는 방식으로 문제를 해결했다.
  - refs [redux-observable/redux-observable#90 (comment)](https://github.com/redux-observable/redux-observable/issues/90#issuecomment-237331721)
  - fixed [836061c3](https://github.com/cannalee90/flash-card/commit/836061c3fbb7b10310a78d183771a4c482e41825)

## 인하대학교 시간표 v2

**시간표를 좀 더 쉽게 작성하면서 좋은 강의를 추천받자**

[Project Repository](https://github.com/cannalee90/inhatime)

### 사용한 기술

- `React`, `Node.js`, `html`, `css`, `AWS`

### 기간 및 인원

- 기간: 2017/03 ~ 2017/06
- 담당: 기획, 웹 프론트엔드, 웹 백엔드, 배포
- 팀원: 2인

### 설명

- 시간표를 작성할 수 있고, 지금까지 들은 과목에 대한 평가를 하고 그 데이터를 기반으로 추천을 받을 수 있는 서비스.
- 졸업과제용 프로젝트로써, 현재는 배포중이지 않다
- [시연연상](https://www.youtube.com/watch?v=NfAYpNKgrYk&feature=youtu.be)

### Trouble Shooting

- 추천 서버와 웹 서버와의 데이터 동기화 이슈
  - 사용자가 평가한 데이터를 추천 서버와 공유야하는데, batch-job 형태가 아니라 실시간으로 요청이 들어가게된다. 즉 웹 서버에서 사용자가 데이터를 입력할때마다 추천 서버로 리퀘스트를 보내게 된다.
  - 각각의 서버가 하나씩 있다면 발생하지 않지만 추천서버가 늘어나게 되면 `race-condition`이 발생할 수 있다
  - Mysql의 table-lock을 사용하거나 큐를 사용해야할지 고민하다가, 구현 안정성을 고려해 `AWS SQS`를 사용했다.

### 후기

- 한명의 팀원의 개인사정으로 나가게 되서 서버와 프론트를 모두 개발해야 되는 상황이었다.
- 상대적으로 숙련도가 높은 언어와 프레임워크를 사용해서 완성할 수 있었던것 같다.
- `SQS`, `SES`, `EC2`, `Route53`, `CloudFront`, `S3`, `RDS`와 같은 AWS의 다양한 기능들을 사용해보았다.


## 인하대학교 시간표 v1

**시간표를 좀 더 쉽게 작성하자**

[Project Repository](https://github.com/cannalee90/inha-schedule)

### 사용한 기술

- `Jquery`, `Rails`, `html`, `css`

### 기간 및 인원 

- 기간: 2016/01 ~ 2017/02
- 담당: 기획, 웹 프론트엔드, 백엔드, 배포
- 인원: 1인

#### 설명
  - 교내 시간표 작성 사이트의 모바일 사용성이 매우 불편하지만 다른 대안이 없다.
  - 데스크탑에서도 매우 사용하기가 힘들고 IE7 기준 최적화가 되어있었다.

#### Trouble Shooting
  - 교내 사이트 크롤링의 어려움
    - Python `Request`와 `Bs4`를 사용해서 인자를 변경해가면서  진행했지만 제대로된 응답이 오지 않았다.
    - `Charles`를 사용해서 `http` 요청을 분석해서 제대로 해결

  - 크롤링 이슈
    - 교내 시간표를 크롤링 해서 얻는 정보가 정규화가 하나도 되어 있지 않았다.
    - 정규표현식을 사용해보려고 했지만, 끊임없이 나오는 예외 때문에 결국 하나하나 예외처리해가면서 진행했다.
  
#### 후기
  - 처음으로 기획 개발 배포까지 진행해본 프로젝트 아는 것이 정말 하나도 없었고 물어볼 사람도 하나도 없어서 힘들게 진행했다.
  - JS에 대한 이해가 하나도 없었고, 즉홍적으로 진행한 프로젝트여서 웹 프론트엔드쪽 코드가 매우 조악하다.
  - 개발의 흥미를 가지게 된 결정적 계기가 된 프로젝트이다.
  - 현재는 배포중이지 않다
