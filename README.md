# Today I Learned

> Don’t let yesterday take up too much of today.” — Will Rogers

**_내가 오늘 배운 것들을 정리한 레포지토리_**

이 레포지토리는 기억의 지도를 만드는 데 의의가 있다. 따라서 상세한 내용은 공식 문서를 참조한다. 그러나 마땅히 참조할만한 공식문서가 없거나 내가 자주 헤매는 부분은 상세히 설명할 수도 있다.

자주 쓰는 것을 격려하기 위해 최대 150줄을 넘지 않도록 유의한다. 읽는 이의 입장에서도 너무 많은 글은 꺼려진다. 그리고 대부분 공식문서가 영어이므로 작성하는 포스트는 영어를 써서 최대한 오해의 소지를 피한다.

개념과 개념을 연결하기 위해 `Furthermore`섹션을 만들어서 이전 토픽, 이후 토픽, 그리고 관련 레퍼런스를 담는다. 이전 토픽과 이후 토픽은 TIL 레포에 담긴 링크이지만 레퍼런스는 외부 링크라는 점이 차이가 있다.

TIL 레포의 이슈는 내가 앞으로 쓸 포스트 내용을 빠르게 등록하는 데 쓰인다. 이슈는 키워드를, 이슈의 코멘트는 키워드에 해당하는 관련 주제를 다룬다. 그리고 관련 주제를 포스트로 작성했다면, 코멘트는 숨김 처리한다.

TIL 레포에서 단어 검색은 `cmd + k`로 검색창을 띄운 다음, `@dankim0213/today-i-learned`를 입력하고 tap을 누르면 할 수 있다. 만약 슬라이싱된 단어를 모두 검색하고 싶다면, 정규식을 활용하자. e.g. `@dankim0213/today-i-learned /type*/`

## Entry points

기억의 지도를 구성하는 시작점들이다. 여기서부터 천천히 길을 따라가면 전체적인 맥락을 이해할 수 있다.

- [How Browser Works (feat. frontend)](./FE/Web/how-browser-works.md)
- ~~BFS vs DFS (feat. algorithms)~~
- ~~Speaking JavaScript (feat. languages)~~

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
├── FE
│   ├── Assignment
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
