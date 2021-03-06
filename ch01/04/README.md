## [JavaScript Practices](https://github.com/kickscar-javascript/basic-practices) / [ch01](https://github.com/kickscar-javascript/basic-practices/tree/master/ch01) / 04. Node.js

### 1. JavaScript Runtime

1. V8(Chrome JavaScript 엔진)으로 빌드된 OS 레벨에서 JavaScript 코드 실행이 가능한 JavaScript 런타임 환경(인터프리터) 이다. 

   ![](http://image.kickscar.me:8080/markdown/javascript-practices/ch01-0001.png)

2. 자체 HTTP 서버 라이브러리을 이용해 웹서버와 같은 서버 사이드 네트워크 애플리케이션 개발이 가능한 애플리케이션 플랫폼이다.

3. 대부분의 JavaScript가 웹 브라우저에서 실행되는 것과는 달리, 서버 측에서 실행된다.

4. 모듈 시스템을 CommonJS 명세를 사용해 왔으나 v12부터 ECMAScript의 공식 모듈 시스템을 사용한다.

5. REPL(Read-Eval-Print Loop) 환경을 포함하고 있어 대화식(Interactice) 테스트 및 프로그래밍도 가능하다.

### 2. 주요 버젼

1. 2009년 Ryan Dahl(라이언 달)이 Ajax 파일업로드의 진행상태 표시를 위해 처음 고안해 냈다.
2. 최초 버전은 리눅스와 macOS만 지원다가  2011년 7월 Microsoft와 파트너쉽을 맺고 Windows 용이 발표되었다.
3. 2011에 패키지 관리 툴인 npm(Node Package Manager)이 발표되었다.
4. 2013년 V0.10 으로 버전닝이 된 Node.js 가 공식 릴리즈 되었다. 
5. 2014년 12월, Fedor Indutny(페도 인더트니)가 차기 릴리즈 지연과 커뮤니케이션 문제등으로 Node.js의 포크(v0.12)인 io.js 로 갈라지면서 두 그룹으로 나뉘게 된다.
6. 2015년 9월, Node.js v0.12와 io.js v3.3은 병합되어 Node v4.0으로 다시 합쳐졌다.
7. v4 이후로 약 6개월 주기로 새로운 버전을 출시하고 있다. 짝수 버전의 경우 장기지원 버전(LTS) 이라고 하여 별도의 코드명을 부여받고 3년간 유지보수 대상이 된다.
8. 2019년 4월, Node.js v12(Erbium) 부터 ECMAScript 공식 모듈 시스템 사용을 실험적으로 지원하기 시작했다.
9. 최신 버전은 13.2.0, LTS 버전은 12.13.1이다. 최신 버전은 기능이 불안정할 수 있으므로 안정성을 보장하고 싶으면 LTS 버전(짝수 버젼)을 사용하는 게 좋다.

### 3. 개발 지원

1. 비동기 프로그래밍
   + 처음부터 Node는 고성능 비동기 애플리케이션 작성 플랫폼으로 구상되고 설계되었다.
   + 당연히,  JavaScript 엔진 기반으로 개발되었기 때문에 JavaScript 비동기 프로그래밍 ([ch10. 비동기 자바스크립트](https://github.com/kickscar-javascript/basic-practices/tree/master/ch10) 참고) 모델에 영향을 받아 개선되고 발전하여 왔다. 
     - 초기 프로그래밍 모델은 함수형 프로그래밍의 리액터 패턴(CPS에 기반한 코드 작성법)의 콜백함수 였다. 하지만  콜백 지옥(무한 들여쓰기, 소스코드가 대각선으로 계속 늘어지는 것)의 코드가 복잡해 지는 문제가 있다.
     - Generator와 Promise(ECMAScript 2015) 와 [async/await](http://rossboucher.com/await) 함수 지원(ECMASscipt 2017) 으로 지금은 동기 프로그래밍 코드처럼 쉽게 비동기 코드를 작성할 수 있다.
2. 최신 ECMAScript 표준 명세 지원
   + V8 JavaScript 엔진을 기반으로 하고 있지만 웹브라우저 보다 조금 빨리 ECMAScript 표준 명세를 지원하고 있다.
   + 클래스, Arrow Function, 블록 단위 변수 스코프, 상수, 템플릿 문자열 등 많은 부분이 개선된 ECMAScript 2015 표준 명세뿐만 아니라 ECMAScript 2019 최근 명세까지 지원한다.
3. 풀스택 개발
   + 프론트엔드와 백엔드를 JavaScript 같은 언어로 개발이 가능한 좁은 의미의 풀스택 개발이 가능하다.
   + 데이터 표현을 위한 실제적 표준 JSON을 풀스택 개발에서 별다른 변환 라이브러리 없이 사용할 수 있는 것도 장점이다. 
   + 특히, 데이터 저장소로 [MongoDB](https://www.mongodb.com/)나 [Elasticsearch](https://www.elastic.co/products/elasticsearch)를 사용하게 되면 데이터 저장, 처리, 표현까지의 전 계층(layer)이 JSON 형식으로 데이터 표현이 통일되는 이점도 있다.
   + 앞의 NoSQL 뿐만 아니라 전통적인 RDBMS 지원도 한다.
     +  MongoDB 연동: [Mongoose](http://mongoosejs.com/)
     + [Redis](http://redis.io/) 연동: [node_redis](https://github.com/NodeRedis/node_redis)
     + [MySQL](https://www.mysql.com/) 연동: [node-mysql](https://github.com/redblaze/node-mysql)
     + PostgreSQL 연동: [node-postgres](https://node-postgres.com/)
     + Elasticsearch 연동: [elasticsearch.js](https://www.elastic.co/guide/en/elasticsearch/client/javascript-api/current/index.html)
4. 다양한 개발 도구 및 라이브러리 지원
   + [트랜스컴파일](https://github.com/kickscar-javascript/basic-practices/tree/master/ch02/03)
     + 서버 개발 뿐만 아니라 웹브라우저 애플리케이션 개발에도 Node.js를 사용한다. 이를 위해서는 웹브라우저에서 지원하는 JavaScript 코드로 변환이 필요한데 이를 위한 개발도구이다.
     + Babel
   + [코드 품질 개선](https://github.com/kickscar-javascript/basic-practices/tree/master/ch02/02)
     + Lint 도구들로 실행 전 작성된 코드의 문제점을 보완하기 위한 유효성 검사 도구이다.
     + ESLint, JSLint, JSHint
   + [빌드](https://github.com/kickscar-javascript/basic-practices/tree/master/ch02/06) 및 [번들링](https://github.com/kickscar-javascript/basic-practices/tree/master/ch02/07)
     + 서버와 클라이언트 애플리케이션 개발에 사용되는 도구들의 단계적 실행과 실행 과정을 자동화하는 도구이다. 
     + JavaScript 코드 모듈 뿐만 아니라 다양한 리소스(CSS, Image 등) 모듈들을 하나의 JavaScript 번들로 생성하는 도구
     + Grunt, Gulp, Webpack
   + 웹 및 모바일 애플리케이션 프레임워크
     + Node.js 는 애플리케이션의 실행을 위한 플랫폼 역활만을 하기 때문에 웹 또는 모바일 애플리케이션 작성을 보다 편하게 그리고 빠르게 도와 줄 애플리케이션 프레임워크가 필요하다. [Express](https://github.com/expressjs/express) 는 기본적인 웹 애플리케이션 기능으로 구성된 계층을 제공하는 프레임워크이다.
     + Express를 기반으로 하는 [상위 수준의 많은 프레임워크](https://expressjs.com/en/resources/frameworks.html) 도 지원하고 있다
     +  웹애플리케이션 개발에서 화면(View) 개발에 필요한 템플릿 엔진도 지원한다. ( [Jade](http://jade-lang.com/), [mustache.js](https://github.com/janl/mustache.js/) )
   + 프로세스 관리
     + 단일 프로세스보다는 실제 서비스에서는 여러 프로세스에 나눠 Node를 실행하고 모니터링 할 필요가 생긴다.
     + Node.js 프로세스 관리 도구 [PM2](http://pm2.keymetrics.io/) 는 Node.js 다중 프로세스 실행을 도와 준다.
     + 프로세스별로 CPU와 메모리 사용량을 모니터링도 PM2를 통해 가능하다.

