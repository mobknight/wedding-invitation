# 개발 History

### Customize the CSS library
CSS Library 없으면 너무 귀찮을 것 같아서, Tailwind를 건드렸다가 결국 익숙한 Bulma를 사용했다. 색깔 커스터마이징을 위해 Sass도 설치했다.

> package.json에 
`"build-bulma": "sass --load-path=node_modules custom.scss ./src/custom.css",`

> css 커스터마이징 후 build-bulma 실행
```bash
npm run build-bulma
```

### 네이버 지도 가져오기
네이버 지도가 구글이나 카카오 대비 깔끔해 보여서 네이버 지도를 넣기로 했는데... 그러려면 Naver Maps API v3를 써야 한다. 일단 네이버 클라우드 플랫폼에 가입하고, 결제 카드 등록하고, API 요청을 위한 클라이언트 아이디 받고, NCP 콘솔에서 한도 설정(Web, 월 천만 건까지 무료) 및 CORS 허용할 도메인 입력하는 건 기본이고...
네이버 지도 SDK는 npm install 할 수 있는게 타입스크립트밖에 없다. 타입스크립트는 싫다. 그래서 자바스크립트 SDK를 `<script src=...>`로 가져오고 Docs에 나오는 대로 코딩했더니, 콘솔에 `naver is not defined` 에러 로그가 뜬다. 외부 js 라이브러리 로드 끝나기도 전에 `new naver.maps.` 하는 부분이 실행되고 있으니 그렇지. `<script src=... on:load={() => {loaded = true}}>`를 주고, `loaded == true`일 때 map DOM을 렌더링하고 네이버 지도 설정 관련 함수를 실행하도록 바꿨다. 그래도 문제가 생겨서 찾아보니 이 부분도 어싱크라서 map DOM이 그려지기 전에 함수를 실행하고 있더라. 그래서 지도 설정 함수를 async로 바꾸고, 맨 앞에 `await tick()`을 추가했다.

```js
import { tick } from 'svelte';
await tick();
```

`await tick()`은 스벨트에서 변수 변화에 따른 화면 재구성이 끝날 때까지 기다리는 함수다. 이거 넣고 해결했다.


### 갤러리 만들기
처음에는 `import.meta.glob("$lib/gallery/*.jpg)`로 디렉토리 내 전체 파일을 어레이로 읽어오고, 이 어레이 기반으로 바둑판식으로 썸네일을 띄우고, 썸네일을 클릭하면 modal 창에 큰 이미지가 뜨게 만들었다. `svelte-gestures`의 `swipe`를 통해 큰 이미지에 대한 좌/우 스와이프도 구현하고. 근데 안 이쁘다는 피드백을 받아서 모조리 갈아 엎었다.

`Swiper`를 사용해서 Carousel 형태의 메인 사진 + 썸네일을 만들고, 클릭시 modal도 구현했다. CSS 때문에 너무 고생했다. 아직도 div 내 컴포넌트에 대한 세로 정렬은 너무 힘들다. CSS 라이브러리 걷어치울까 하는 생각을 몇 번이나 했는데, 결국 parent 쪽에 `height: auto; width: auto; max-height: 100%; max-width: 100%` 넣고, figure에는 ratio 명시하고(`is-2by3`), img에는 `object-fit: scale-down;` 넣는 걸로 해결했다.

dev에서는 문제가 없었는데, 빌드/배포하고 나서 보니 갤러리 내 이미지가 전혀 안 뜬다. 원인은 `import.meta.glob` 부분이었는데, Vite에서 이미지를 말면서 파일명에 hash를 집어넣는 문제 + 디렉토리 맘대로 바꾸는 문제 때문에 `import.meta.glob`으로 가져온 어레이 내 파일명과 빌드된 파일명이 전부 다른 상황이 나온다. vite config에서 rollup option을 바꿔도, sveltekit에서 이 옵션을 오버라이드하기 때문에 해결할 수 없다. 이건 https://kit.svelte.dev/docs/images#sveltejs-enhanced-img 를 적용해서 해결했는데, 빌드시 enhanced img에서 어차피 파일명을 다 바꾸면서 다중 파일을 생성하고 코드를 그에 맞게 적절히 바꿔주는 듯.

