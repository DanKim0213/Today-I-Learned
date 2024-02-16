# Today I Learned

> Don’t let yesterday take up too much of today.” — Will Rogers

**_내가 오늘 배운 것들을 정리한 레포지토리_**

이 레포지토리는 기억의 지도를 만드는 데 의의가 있다. 따라서 상세한 내용은 공식 문서를 참조한다. 그러나 마땅히 참조할만한 공식문서가 없거나 내가 자주 헤매는 부분은 상세히 설명할 수도 있다.

자주 쓰는 것을 격려하기 위해 최대 150줄을 넘지 않도록 유의한다. 읽는 이의 입장에서도 너무 많은 글은 꺼려진다. 그리고 대부분 공식문서가 영어이므로 작성하는 포스트는 영어를 써서 최대한 오해의 소지를 피한다.

개념과 개념을 연결하기 위해서, 문서를 시작할때 이전 토픽을 그리고 문서가 끝날때 `Furthermore`섹션에 이후 토픽 및 관련 레퍼런스를 담는다. 이전 토픽과 이후 토픽은 TIL 레포에 담긴 링크이지만 레퍼런스는 외부 링크이다.

TIL 레포의 이슈는 내가 앞으로 쓸 포스트 내용을 빠르게 등록하는 데 쓰인다. 이슈는 키워드를, 이슈의 코멘트는 키워드에 해당하는 관련 주제를 다룬다. 그리고 관련 주제를 포스트로 작성했다면, 코멘트는 숨김 처리한다.

TIL 레포에서 단어 검색은 `cmd + k`로 검색창을 띄운 다음, `@dankim0213/today-i-learned`를 입력하고 tap을 누르면 할 수 있다. 만약 슬라이싱된 단어를 모두 검색하고 싶다면, 정규식을 활용하자. e.g. `@dankim0213/today-i-learned /type*/`

[INDEX](#index)를 통해 각 문서에 대한 간략한 정보를 알 수 있다. 문서에 대한 간단한 정보는 `head` 리눅스 명령어를 사용해 10줄씩 정리한다. e.g. `head Develop/**/*`. 따라서, 각 문서의 상단에 TL;DR;을 작성하자.

## Entry points

기억의 지도를 구성하는 시작점들이다. 여기서부터 천천히 길을 따라가면 전체적인 맥락을 이해할 수 있다.

- [What Happens Behind Browser (feat. develop)](./Develop/Web/what-happens-behind-browser.md)
- [Introduction to Algorithms (feat. algorithms)](./Algorithms/introduction-to-algorithms.md)
- ~~Speaking JavaScript (feat. languages)~~
- [Introduction to Test (feat. develop)](./Develop/Test/introduction-to-test.md)

## Tree

때로는 키워드로 관련 정보를 찾는다. 이에 따라 내가 다루는 키워드를 폴더형태로 구성했다. 만약 찾는 정보의 키워드가 여기 없다면, 새로운 이슈를 생성해 앞으로 담을 내용을 간략히 정리한다.

```
.
├── Algorithms
│   ├── DataStructures
│   ├── Graph
│   ├── Optimization
│   ├── Search
│   └── Undefined
├── Develop
│   ├── Reactjs
│   ├── Test
│   └── Web
├── Languages
│   ├── JavaScript
│   ├── Python
│   ├── SQL
│   └── TypeScript
└── Tools
    ├── Git
    ├── Google
    └── VIM
```

## Index

Develop

<details>
  <summary>Reactjs</summary>

    ==> Develop/Reactjs/components-must-be-pure.md <==
    # Component Must Be Pure

    TL;DR;

    - Components must be pure since, by doing so, React can restart rendering without wasting time.
    - Strict mode can help surface mistakes caused by impure functions as soon as possible.
    - `Event handler` is the saviour to comply with purity, in response to side effects.
    - `useEffect()` call is your last resort, in response to side effects.

    So far, you've looked over [What Makes React Exceptional](./what-makes-react-exceptional.md).

    ==> Develop/Reactjs/react-hook-form.md <==
    # React Hook Form

    Simple form validation with React Hook Form.

    [Quick Start](https://react-hook-form.com/get-started#Quickstart)

    ==> Develop/Reactjs/what-makes-react-exceptional.md <==
    # What Makes React Exceptional

    TL;DR;

    - Tell React your destination, not turn by turn where to go - Declarative UI Programming.
    - All React “sees” is the UI tree you return, based on which it changes the DOM nodes.

    So far, you've looked over [How Browser Renders Content](../Web/how-browser-renders-content.md)

</details>

<details>
  <summary>Web</summary>

    ==> Develop/Web/how-browser-renders-content.md <==
    # How Browser Renders Content

    TL;DR;

    1. DOM tree
    2. CSSOM tree
    3. Render tree
    4. Layout
    5. Paint


    ==> Develop/Web/responsive-design.md <==
    # Responsive Design

    Table of Content

    1. Types of design
    1. Responsive Design
    1. Media queries
    1. Macro layouts
    1. Micro layouts
    1. Typography

    ==> Develop/Web/testing-tool.md <==
    # Load Testing Tool

    Content

    1. K6
    1. Lighthouse
    1. Furthermore

    ## K6


    ==> Develop/Web/what-happens-behind-browser.md <==
    # What Happens Behind Browser

    TL;DR;

    1. IP address for the domain
    2. TCP Connection
    3. HTTP request to the server
    4. Response from the server
    5. Browser rendering.

</details>

<details>
  <summary>Test</summary>

    ==> Develop/Test/check-arguments.md <==
    # Check arguments

    TL;DR;

    - You have two options to check arguments.
    - One of them is `mockFn.toHaveBeenCalledWith()`.
    - The other is `mockFn.toHaveBeenReturnedWith()`.

    Make sure you've read [Introduction to Test](./introduction-to-test.md).


    ==> Develop/Test/how-to-handle-errors-with-jest.md <==
    # How to handle errors with Jest

    ## Agenda

    1. The goal of this post
    2. expect.assertions(number) rather than done()
    3. .rejects rather than try-catch
    4. .toThrow rather than toMatch or toEqual
    5. Use-case 1: Handle Error in a function
    6. Use-case 2: Handle Error in an asynchronous function

    ==> Develop/Test/index-of-kent-c-dodds.md <==
    # Index of Kent C. Dodds

    ## How to use

    - How to use jest.mock() and use the exported function as if jest.fn():[app-03](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/app-03.js)
    - How to test custom hooks with `renderHook()`: [custom-hook-02](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/custom-hook-02.js) to [custom-hook-03](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/custom-hook-03.js)
    - How to use `mockFn.fn()` with `mockFn.mockResolvedValueOnce()` for dependency injection:
      [dependency-injection](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/dependency-injection.js)
    - How to use MSW: [http-jest-mock](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/http-jest-mock.js) and [http-msw-mock](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/http-msw-mock.js)
    - How to use queryBy: [mock-component](https://github.com/kentcdodds/react-testing-library-course/blob/main/src/__tests__/mock-component.js)

    ==> Develop/Test/introduction-to-test.md <==
    # Introduction to Test

    TL;DR;

    - Test as simple as possible.
    - Test as much as users would use.
    - Test as precisely as possible.

    > [The more your tests resemble the way your software is used, the more confidence they can give you.](https://testing-library.com/docs/guiding-principles/)


    ==> Develop/Test/test-as-much-as-users-would-use.md <==
    # Test as much as Users would use

    TL;DR;

    - Priority when to query: `Role` > `LabelText` > `Text`.
    - Avoid to use `TestId`.
    - Use `user-event` over `fire-event`.
    - You can't access component methods or the component instance.

    Make sure you've read [Introduction to Test](./introduction-to-test.md).

    ==> Develop/Test/test-as-precisely-as-possible.md <==
    # Test as precisely as possible

    TL;DR;

    - Use proper queries.
    - Make your tests more declarative.
    - Query within elements.

    Make sure you've read [Introduction to Test](./introduction-to-test.md).


    ==> Develop/Test/test-as-simple-as-possible.md <==
    # Test as simple as possible

    TL;DR;

    - Write Integration tests rather than Unit tests.
    - Isolate modules by mocking.
    - Separte concerns by tests for meaningful test fails.

    Make sure you've read [Introduction to Test](./introduction-to-test.md).

</details><br />

Algorithms

<details>
  <summary>Introduction</summary>

    ==> Algorithms/introduction-to-algorithms.md <==
    # Introduction to Algorithms

    TL;DR;

    - Algorithms are largely divided into two parts: _Brute-force_ and _Divide-and-Conquer_.
    - You should be used to _Data Structure_ before diving into Algorithms.
    - You could unexpectedly run into two errors: _Recursion Error_ and _Timeout Error_.

    ==> Algorithms/bfs-vs-dfs.md <==
    # BFS vs DFS

    TL;DR;

    - Either BFS or DFS: problems solved by just checking link between nodes.
    - BFS: not only checking link but also achieving your goal in the middle of searching.
    - DFS: not only checking link but also achieving your goal in the end of searching.

    ## Either BFS or DFS

</details>

<details>
  <summary>Search</summary>

</details><br />
