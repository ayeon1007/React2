# React2

# 2024-10-2

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
