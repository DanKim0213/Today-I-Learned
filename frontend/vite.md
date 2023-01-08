# Vite

Vite(프랑스어로 "빠르다(Quick)"를 의미하며, 발음은 "veet"와 비슷한 /vit/ 입니다.)은 빠르고 간결한 모던 웹 프로젝트 개발 경험에 초점을 맞춰 탄생한 빌드 도구이며, 두 가지 컨셉을 중심으로 하고 있습니다.

- 개발 시 네이티브 ES Module을 넘어 더욱 다양한 기능을 제공합니다. 가령, Hot Module Replacement (HMR)과 같은 것들 말이죠.
- 번들링 시, Rollup 기반의 다양한 빌드 커맨드를 사용할 수 있습니다. 이는 높은 수준으로 최적화된 정적(Static) 리소스들을 배포할 수 있게끔 하며, 미리 정의된 설정(Pre-configured)을 제공합니다.

## 목차

1. 내가 왜 Vite 를 선택했는지
1. Vite 를 왜 써야하나
1. Vite 와 Create-React-App 의 차이는
1. Templates
1. 개발할때 참조하면 좋을 문서
1. References

## 1. 내가 왜 Vite 를 선택했는지

CRA 사용 경험과 비교해봤을때 명령어의 이름만 차이만 있을뿐 명령어의 기능은 같았고 Vite를 통해 만들어진 프로젝트 특징 또한 같았다. 개발 단계에서 빌드 속도를 10 ~ 100배 끌어올릴 수 있다면 선택하지 않을 이유가 없다.

## 2. Vite 를 왜 써야하나

- 문제점: 애플리케이션이 점점 더 발전함에 따라 처리해야 하는 JavaScript 모듈의 개수가 극적으로 증가 -> JavaScript 기반의 도구는 성능 병목 현상이 발생
- 해결방법: Vite는 이러한 것에 초점을 맞춰, 브라우저에서 지원하는 ES Modules(ESM) 및 네이티브 언어로 작성된 JavaScript 도구 등을 활용해 문제를 해결하고자 합니다.
- 특징들:
  - 네이티브 ESM을 이용해 번들링 없이 온디맨드로 파일을 제공할 수 있어요!
  - 앱 크기에 상관없이 Hot Module Replacement(HMR)는 언제나 빠르게 동작해요.
  - 추가적인 모듈의 설치 없이 TypeScript, JSX, CSS 등을 사용할 수 있어요.
  - 유연하게 작성된 API는 TypeScript 역시 완벽하게 지원해요.

## 3. Vite 와 Create-React-App 의 차이는

- Vite (Native ESM-based by [esbuild](https://esbuild.github.io)) vs CRA (Javascript-based by [Webpack](https://webpack.js.org))
- vite는 HTTP 헤더를 이용해 퍼포먼스를 한 단계 높였습니다. 필요에 따라 소스 코드는 304 Not Modified로, 디펜던시는 Cache-Control: max-age=31536000,immutable을 이용해 캐시되도록 함으로써, 한 번의 요청이라도 덜 하도록 말이죠.

## 4. Templates

- [awesome-vite](https://github.com/vitejs/awesome-vite#templates)
- Vanilla, Vue 3, Vue 2, React, Svelte, and etc.

## 5. 개발할때 참조할 문서

- [ENV 사용하기](https://vitejs-kr.github.io/guide/env-and-mode.html)
- [에셋 가져오기](https://vitejs-kr.github.io/guide/assets.html#new-url-url-import-meta-url)
- [트러블슈팅](https://vitejs-kr.github.io/guide/troubleshooting.html#others)

## 6. References

- [Vite 공식문서](https://vitejs-kr.github.io)
- [awesome-vite](https://github.com/vitejs/awesome-vite#templates)
- [CRA 는 babel + Webpack 을 기본적으로 제공해요](https://create-react-app.dev/docs/getting-started/#get-started-immediately)
