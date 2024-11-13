# React2

# 202230234 조아연

# 2024-11-13

UI 프레임 워크

UI 라이브러리

- UI 라이브러리, 프레임워크, 유틸리티 기능이 필수는 아님
- 다만 생산성 향상 및 UI의 일관성을 유지하는데 많은 도움을 받을 수 있음
- ex : chakra ui, tailwind css, headless ui 등 (bootstrap도 있음)

chakra ui

- 오픈소스 컴포넌트 라이브러리로, 모듈링이 되어 있고, 접근성이 뛰어나며 보기 좋은 UI를 만들 수 있음
- 버튼, 모달, 입룍 등 다양한 내장 컴포넌트 제공
- dark mode, light mode 지원
- chakra ui의 getColorMode훅을 사용하여 현재 사용하는 컬러 모드를 확인할 수 있음
- 기본 컴포넌트를 조합해서 새로운 컴포넌트를 쉽게 만들 수 있음
- TypeScript로 작성되었으며 개발자에게 편함

tailwind css

- 다른 프레임워크와는 다르게 CSS규칙만을 제공
- 자바스크립트 모듈이나 리액트 컴포넌트를 제공하지 않기 때문에 필요한 경우 직접 만들어서 사용
- 변수값을 조정하여 개성있는 디자인을 만둘 수 있고, 자유도가 높다
- dark mode, light mode 지원
- 빌드 시점에 사용하지 않는 클래스는 제거 되기 때문에 높은 수준의 최적화를 지원
- CSS 클래스와 접두사를 활용한 모바일 데스크톱, 태블릿 화면에서 원하는 규칙을 지정할 수 있음

headless ui

- TailwindCss를 만든 팀의 무료 오픈소스 프로젝트
- TailwindCss는 웹 컴포넌트 안에서 사용할 수 있는 CSS클래스만 제공
- 따라서 모달, 버튼 등 동적인 컴포넌트를 만드려면 직접 자바스크립트 코드를 작성해야 함
- 이런 단점을 보완하기 위해 headless ui가 등장

Next.js의 UI Framework  
Project 생성

- tailwind 사용을 위해 프로젝트를 다시 생성
- 프로젝트를 다시 생성하지 않고 설정할 수도 있지만 과정이 다소 복잡
- 프로젝트는 Next.js 14로 함

```js
$ npx create-next-app@14

프로젝트 이름은 자유, 나머지는 모드 yes로 한다
(난 tailwind, TypeScript만 yes함 )
```

- 구글에서 chakra ui 검색하고 사이트에 접속
- Home 화면에서 Start building 버튼을 클릭하고 Next.js 선택
- App/chakra/page.js 파일 생성

React-icon

-

# 2024-11-6

CSS와 내장 스타일링 메서드  
Styled JSX

- Styled JSX는 CSS-in-JS라이브러리, 내장 모듈이기 때문에 설치가 필요 없음
- 즉 CSS 속성 지정을 위해 자바스크립트를 사용할 수 있는 라이브러리

```js
간단한 예시 코드

"use client";

export default function CssEx() {
  return (
    <>
      <h1>CssEx Page</h1>
      <button className="button">버튼 1 </button>
      <style jsx>{`
        .button {
          background: orangered;
          color: white;
        }
      `}</style>
    </>
  );
}
```

CSS-in-JS 단점

- IDE나 코드 편집기 등 개발 도구에 대한 지원 부족
- 문법 하이라이팅, 자동 완성, 린트(lint)기능을 제공하지 않음
- 코드 내에서 CSS에 대한 의존성이 점점 커지기 때문에 앱 번들도 커지고 느려짐
- 서버에 미리 CSS를 생성해도 클라이언트에서 리엑트 하이드레이션이 끝나면 CSS를 다시 생성 해야함

CSS Module

- CSS-in-JS의 단점을 회피하기 위한 좋은 방법은 CSS Module이다

```js
간단한 예시 코드
import styles from "./page.module.css"

export default function Home() {
  return (
    <>
    <h1 className = {styles.main} >북쪽에 계신 아름다운 메리메리</h1>
    </>
  )
}
```

- 클래스들은 컴포넌트 스코프를 갖는다
- 생성된 HTML 페이지 소스를 보면 class 이름이 바뀌어 있는 것을 확인할 수 있음
- Styled JSX때와 마찬가지로 이런 고유한 이름 때문에 다른 파일이라면 같은 class명을 사용해도 충돌이 일어나지 않음
- 만들 전역 CSS를 선언하고 싶다면 styles/globals.css를 만들고 사용
- 파일명은 반드시 globals가 아니어도 되지만 암묵적 합의는 지키는 것이 좋음

```js
html,
body {
  padding: 0;
  margin: 0;
}
```

SASS

- Next에서 기본으로 지원하는 건 처리기
- 단 패키지 설치가 필요 $npm install sass
- SASS 및 SCSS 문법으로 CSS Module을 만들고 사용할 수 있음

```js
import scss from "../styles/joo.module.scss";

export default function SassEx() {
  return (
    <>
      <div>
        <h1 className={scss.woo}>SassEx Page</h1>
        <button className={scss.bar}>Button</button>
      </div>
    </>
  );
}
```

```js
$joo: red;

.woo {
  color: black;
  background-color: aqua;
}

.bar {
  color: $joo;
}

```

# 2024-10-30

데이터 불러오기

- Next 클라이언트와 서버 모두에서 데이터를 불러올 수 있음
- 데이터 베이스에서 데이터를 가져올 수도 있지만 안전하지 않아 권장하지 않음. 데이터 베이스와 접근은 백엔드에서 처리하는 것이 좋음
- Next는 프론트앤드만!

서버가 데이터 불러오기  
두가지 방법으로 HTTP 요청을 만들고 처리할 수 있음

- 첫 번째는 Node의 내장 HTTP 라이브러리를 사용할 수 있다. 다만 서브파티 HTTP 클라이언트와 비교했을 때 설정하고 처리해야 할 작업이 더 많은 편...
- 두 번째 방법은 HTTP 클라이언트 라이브러리를 사용할 수 있다. 가장 유명한 것이 Axios? 이다

서버에서 REST API 사용하기

- Public API는 어떤 인증이나 권한도 필요 없으며 누구나 호출할 수 있음
- Private API는 호출 전 반드시 인증과 권한 검사를 거쳐야 함

REST API - 개요

- HTTP URL 동일된 자원 식별자를 이용해서 자원을 명시
- HTTP Method를 통해 자원에 CRUD를 적용
- REST API란 REST의 규칙을 적용한 API를 의미

CRUD?

- Create : 데이터 생성 (POST)
- Read : 데이터 조회 (GET)
- Update : 데이터 수정 (PUT(전체 수정), PACTH(조금 수정할 것들만))
- Delete : 데이터 삭제 (DELETE)

JSON Server

- Backend가 개발되기 전이나, 외부 API가 결정되지 않았다면 local에 Json server를 구축하고 Frontend 개발을 하기에 적합한 node 패키지

```js
Json server 설치 명령
npm i -g json-server
```

Axios

- Next.js에서 REST API룰 다룰 떄는 보통 axios와 fetch 중 하나를 선택하는 경우가 있다

Feach?

- 내장 API 브라우저에 내장되어있어 별도의 설치 필요 없음
- 스트림 처리 : 데이터를 스트리밍으로 처리할 수 있는 기능이 있어, 큰 파일을 처리하는데 유용

결론은 복잡한 요청이나 에로 초리가 필요한 경우는 axios

```js
axios 설치 명령
npm i axios
```

Axios 사용하기

- axios.get()을 통해 받아온 응답 객체인 res는 단순히 JSON 데이터만 담고 있는 것이 아니라 HTTP 통신과 관련된 여러 정보들을 함께 포함하고 있다

# 2024-10-23

Image component - Remote

- Pixabay와 같은 외부 이미지를 사용하려면 next.config.mjs에 URL을 추가해야함
- 만일 파일이 없다면 Project Root에 추가하면 됨

```js
// next.config.mjs
/** @type {import('next').NextConfig} */
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocal: "https",
        hostname: "cdn-pixabay.com",
      },
    ],
  },
};

export default nextConfig;

// about/page.jsx
{
  /*외부 이미지 출력*/
}
<Image
  src="https://cdn.pixabay.com/photo/2023/08/09/15/06/child-8179655_1280.jpg"
  alt="신발"
  width={300}
  height={500}
/>;
```

- 서비스에 따라 도메인은 차이날 수 있음
  -pixabay의 경우 원하는 이미지를 우클릭하고 이미지 주소 복사로 주소를 복사 -나머지는 local image사용법과 같음

코드 구성과 데이터 불러오기
디렉토리 구조 구성

- next.js에서는 특정 파일과 디렉토리가 저장된 위치에 있어야 함 \_app.js 나 document.js 파일,
  pagee/ 와 public/
  -Node moudules/: 프로젝트와 의존성 패키지를 설치하는 디렉토리
- pages/ : 애플리케이션의 페이지 파일을 저장하고 라우팅 시스템 관리
- public/ : 컴파일된 CSS및 자바스크립트 파일, 이미지, 아이콘 등의 정적 자원 관리
- styles/ : 스타일링 포멘(CSS, SASS, LESS등)과 관계없이 스타일링 모듈 관리

컴포넌트 구성

- 컴포넌트는 세가지로 분류, 각 컴포넌트와 관련된 스타일 및 텍스트 파일을 같은 곳에 두어야 함
- 코드를 더 효율적으로 구성하기 위해 아토믹 디자인 원칙에 따라 디렉토리를 구성
- atoms : 가장 기본적인 컴포넌트 관리 ex : button, input, p와 같은 표준 html요소를 감싸는 용도로 사용
- molecules : atom에 속한 컴포넌트 여러 개를 조합하여 복잡한 구조로 만든 컴포넌트 관리 ex : input, label을 합쳐서 만든 새로운 컴포넌트
- organisms : molecules , atoms룰 섞어서 더 어렵게! 만든 컴포넌트 관리 ex : footer, carousel 컴포넌트
- templates : 위의 모든 컴포넌트를 어떻게 배치할 지 결정해서 사용자가 쉽게 접근할 수 있는 페이지

유틸리티 페이지

- 컴포넌트를 만들지 않는 코드 파일을 유틸리티 스크립트라고 함

데이터 불러오기

- next는 클라이언트, 서버 모두에서 데이터를 불러올 수 있음
- 데이터 베이스에서 데이터를 가져올 수도 있지만 안전하지 않기 때문에 권장 안 함
- next는 프론트엔드만 담당하는 것이 좋음

# 2024-10-11 (보강주 수업)

Next.js의 Layout

- app.jsx는 서버에 요청할 때 가장 먼저 실행되는 컴포넌트
- 페이지에 적용할 때 공통 레이아웃을 선언하는 곳

```js
기본 코드
import "@/styles/globals.css";

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

```

Page Project Layout

- document.jsx는 \_app.jsx 다음에 실행
- 각 페이지에서 공통적으로 사용될 html, head, body 안에 들어갈 내용을 선언한다
- onClick 같은 이벤트나 css는 이곳에 선언하지 않음

```js
기본 코드
import {Html, Head, Main, NextScript} from "next/document"

export default function Document() {
  return (
    <Html lang="en">
    <Head />
    <body>
      <Main/>
      <NextScript />
    </body>
    </Html>
  );
}
```

App Project - Layout

- Layout.jsx는 app 디렉토리 아래에 위치
- Layout.jsx는 page Project 사용하던 \_app.jsx와 document.jsx를 대체
- 이 파일은 삭제해도 프로젝트를 실행하면 자동으로 다시 생겨남

```js
기본 구조
export const metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
};

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

App Project Layout = meta data

- metadata에서 모든 페이지에 적용될 meta data를 선언할 수 있음
- title의 경우에는 각 페이지에 맞게 작성하는 것이 SEO에 좋다

App Project Layout

```js
기본 코드
export default function RootLayout {(children)} {
  return (
    <html lang="ko">
      <body>
        <h1>===== Header =====</h1>
        <header></header>
        <main>{children}</main>
        <footer>
          <h2>---Footer---</h2>
        </footer>
      </body>
    </html>
  );
}
```

Link component

```js

- Link component를 이용해서 Narbar component를 만들어봄
import Link from "next/link";

export default function Navbar() {
  return (
    <nav>
      <Link href="/">HOME</Link>
      <Link href="/foo">foo</Link>
      <Link href="/about">about</Link>
      <Link href="/help">help</Link>
    </nav>
  );
}


```

Link vs router.push

- Link component를 이용해서
  App Project - link component를 이용해서 Narbar component를 만들어봄
- a tag는 html 동기식으로 전체가 reload 되기 때문에 외부 링크를 할 때 사용함
- 일반적으로 내부 링크 이동시에는 사용하지 않는 것이 좋다

- router.push는 빌드 후 이동할 주소가 html 상에 노출되지 않기 때문에 SEO에 취약
- link 컴포넌트는 빌드 후 a tag로 자동 반환
- 내부 페이지로의 이동할 때에 이 방식을 사용해야 SPA 방식으로 전체 html 중 필요한 부분만 비동기식으로 리렌더링 됨
- 따라서 특별한 경우가 아니면 link 컴포넌트 사용을 권장

Image component - local

Static Resource

- 정적 자원 중 이미지 파일은 SEO에 많은 영향을 미침
- 다운로드 시간이 많이 걸리고, 렌더링 후에 레이아웃이 변경되는 등 UX에 영향을 마침
- 이것을 누적 레이아웃 이동 (CLS : Cumulative Layout Shift)
- image 컴포넌트를 사용하면 CLS문제를 해결

- lazy loading 이미지 로드 시점을 필요할 때까지 지연시키는 기술
- 이미지 사이즈 최적화로 사이즈를 1/10이하로 줄요줌
- Placehoder를 제공
- WebP와 같은 최신 이미지 포멧 및 최신 포멧을 지원하지 않는 브라우저를 위해 png나 jpge와 같은 예전 이미지 포멧도 제공
- Pixabay나 Unplash와 같은 외부 이미지 서비스로 이미지를 제공
- image 컴포넌트를 사용하면 다양한 props를 전달할 수 있음

```
주요 props

- src = " "
- width = { 500 }
- height = { 500 }
- alt = " "
- Placeholder "blue" (외부 이미지는 blurDataURL = ' '로 처리)
- loading = "lazy"
```

Image Component - local

- 정적 자원은 기본적으로 public 디렉토리에 저장
- 정적 자원은 번들링 이후에도 변하지 않기 때문
- 여러 종류의 정적 자원을 사용할 경우 public의 root에 각각 디렉토리를 만들어 사용!
- 이미지를 불러오는 방법봐 import하는 방법 2가지
- 직접 불러올 땐 경로는 /images/[이미지이름.확장자]로 하기

```js
import Image from "next/image";

export default function About() {
  return (
    <div>
      <h1>About</h1>
      <p>This is the about page</p>
      <Image src="/image/person.jpg" alt="사람" width={300} height={500} />
    </div>
  );
}
```

# 2024-10-2

실습을 주로 진행

```js
PAGE - ROUTER;
import { useRouter } from "next/router";

export default function Joo() {
  const router = useRouter();
  const { blog, joo, id, name, pid } = router.query;
  console.log(blog, joo, id, name, pid);

  return (
    <>
      <h1>joo: {joo}</h1>
      <h1>blog:{blog}</h1>
      <h1>id : {id}</h1>
      <h1>name: {name}</h1>
      <h1>pid: {pid}</h1>
    </>
  );
}
//http://localhost:3000/blog/joo?id=1234&name=jo&pid=1122
```

```js
PAGE - ROUTER;
import { useRouter } from "next/router";

export default function Joo() {
  const router = useRouter();
  const { joo, id, name, pid } = router.query;
  console.log(joo, id, name, pid);

  return (
    <>
      <h1>joo[0]: {joo[0]}</h1>
      <h1>joo[1]: {joo[1]}</h1>
      <h1>joo[2]: {joo[2]}</h1>
      <h1>id : {id}</h1>
      <h1>name: {name}</h1>
      <h1>pid: {pid}</h1>
    </>
  );
}
//http://localhost:3000/blog/joo/bar/joobar
```

```js
APP - ROUTER;
export default function Page(props) {
  console.log(props);
  return (
    <>
      <h1>joo:{props.params.joo}</h1>
      <h1>id:{props.searchParams.id}</h1>
      <h1>name:{props.searchParams.name}</h1>
    </>
  );
}
```

# 2024-9-25

Next.js 기초와 내장 컴포넌트

- Next는 서버사이드 랜더링 외에도 많은 내장 컴포넌트와 함수를 제공한다

라우팅 시스템

- React의 React Router, Reach Router 등은 클라이언트 라우팅만 구현할 수 있음
- Next는 파일 시스템 기반 페이지와 라우팅을 한다
- 페이지는 /page 디렉토리 안의 *js, *jsx, *ts, *tsx파일에서 export한 React의 컴포넌트이다

```js
export default function Example() {
  return (
    <div>
      <h1>Example 1</h1>
      <h1>Example 2</h1>
      <h1>Example 3</h1>
    </div>
  );
}
```

# 2024-09-11

서버 사이드 랜더링 (SSR)

- 생소할 수 있지만 웹 페이지를 제공하는 가장 흔한 방법
- APM을 이용하는 일반적인 웹 페이지 생성이라고 보면 됨
- 여기에 자바 스크립트 코드가 적제되면 동적으로 페이지 내용을 렌더링

SSR의 장점

- 더 안전한 웹 애플리케이션 : 쿠키 관리, 주요 API, 데이터 검증 등과 같은 작업을 서버에서 처리하기 때문에 데이터를 클라이언트에 노출할 필요 없음
- 더 뛰어난 웹 사이트 호환성 : 클라이언트 환경이 자바스크립트를 사용하지 못하거나 오래된 브러우저를 사용하더라도 서비스를 제공할 수 있음
- 더 뛰어난 SEO : 서버가 렌더링한 HTML을 받기 때문에 봇이다 웹 크롤러가 페이지를 렌더링 할 필요가 없다

SSR이 최적의 렌더링 전략이 아닌 경우

- 클라이언트가 페이지를 요청할 때마다 페이지를 다시 렌더링 할 수 있는 서버가 필요
- 다른 방식에 비해 SSR이 더 많은 자원을 소모하고, 더 많은 부하를 보이며 유지 보수 비용도 증가
- 페이지에 대한 요청을 처리하는 시간이 길어짐
- 페이지가 외부 API또는 데이터 소스에 접근해야 한다면 해당 페이지에 렌더링할 때마다 이를 다시 요청해야함
- 페이지 간의 이름은 CSR에 비해 느림
- 중요한 것은 Next.js가 기본적으로 빌드 시점에 정적으로 페이지를 만든다는 것
- 페이지에서 외부 API를 호출하거나 데이터베이스에 접근하는 등 동적 작업을 해야 한다면 해당하는 함수를 페이지에 export해야함

클라이언트 사이드 렌더링 (CSR)

- React 앱을 실행하면 렌더링 시작 전에 빈 화면이 한동안 유지 되는 것이 보임
- 이는 서버에서 스크립트와 스타일만 포함된 HTML을 전송하기 때문
- 실제 렌더링은 클라이언트에서 이루어짐
- CSR로 생성한 앱의 HTML을 보면 div태그 하나 뿐, 그래서 빈 화면만 보였던 것
- 빌드 과정에서 js, css파일을 HTML페이지에 불러오도록 만들고 root div에 렌더링

CSR을 사용할 때의 주요 이점

네이티브 앱처럼 느껴지는 웹 앱

- 전체 자바스크립트 번들을 다운로드 한다는 것은 렌더링 할 모든 페이지가 이미 브라우저에 다운로드가 되어 있다는 뜻
- 다른 페이지로 이동해도 서버에 요청할 필요 없이, 바로 페이지를 이동할 수 있음
- 페이지를 바꾸기 위해 새로 고칠 필요가 없음

쉬운 페이지 변환

- 클라이언트에서 내비게이션은 브라우저 화면을 새로 고칠 필요 없이 다른 페이지로의 이동을 가능하게 만듦
- 페이지 간 전환에 멋진 효과를 넣을 수도 있다. 애니메이션을 방해할 요소가 없기 때문

지연된 로딩과 성능

- 웹 앱은 최소로 필요한 HTML만 렌더링함
- 버튼을 누르면 나오는 모달도 실제 버튼이 눌렸을 때 동적으로 생성하게 됨
  서버 부하 감소 = 서버리스 환경에서 웹 앱을 제공할 수도 있음

정적 사이트 생성(SSG : Static Site Generation)

- SSG 일부 또는 전체 페이지를 빌드 시점에 미리 렌더링함
- SSG는 SSR 및 CSR과 비교했을 때 다음과 같은 장점이 있음

쉬운 확장

- 정적 페이지는 단순 HTML 파일이므로 CDN을통해 파일을 제공하거나, 캐시에 저장하기 쉬움

뛰어난 성능

- 빌드 시점에 HTML페이지를 미리 렌더링하기 때문에 페이지를 요청해도 클라이언트나 서버가 무언가를 처리할 필요 없음

더 안전한 API요청

- 외부 API를 호출하거나, 데이터베이스에 접근하거나, 보호해야 할 데이터에 접근할 일이 없다
- 필요한 모든 정보가 빌드 시점에 미리 페이지로 렌더링 되어 있기 때문

# 2024-8-28

React를 개발하다 처음 NEXT를 사용하면 제일 놀라는 기능이 Router이다

[Pages Router]

- pages 디렉토리가 root이고 index.js가 index.page가 된다
  클라우드 중심의 라우팅

[App Router]

- app 디렉토리가 root이고 page.js가 index.page가 된다
  서버 중심의 라우팅

Node.js 13 vs 14

Data Fetching : 13까지는 getServerSideProps, getStaticProps 메소드를 이용해서 구현했으나, 14에선 SSG(정적 사이트 생성), SSR(서버측 렌더링), 및 ISR(충분적 정적 재생성)에서 오직 하나의 API만을 사용해서 구현할 수 있게 되었다

이미지 최적화 : 13까지는 도구를 사용하였으나, 14에서부턴 자체적으로 지원
보안 강화 : XSS 공격에 대한 보호 기능이 강화되고, 보안 관련 헤더 설정을 더욱 쉽게 만들었다
