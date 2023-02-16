# box 모델

: html 요소는 박스 모양으로 구성되어 있다. box-model이라고 부른다.

- content(내용) : 요소의 실제 내용이 차지하는 영역
- padding(패딩) : 내용과 테두리 사이의 간격
- border(테두리) : 내용과 패딩을 감싸는 테두리
- margin(마진) : 테두리와 이웃하는 요소 사이의 간격, 외부 여백

# box-sizing 속성

## content-box

- default 값
- content 영역을 기준으로 box의 size를 적용한다.
- 예를 들어 width가 50px, padding이 10px이면
  content를 기준으로 크기를 잡기 때문에
  실제 보이는 border영역까지의 width는 60px이 된다.
- content-box를 잘 사용하지 않는다.

## border-box

- border 영역을 기준으로 box의 size를 적용한다.
- 보통 border-box로 속성을 잡고 개발한다.
- 사람이 보는 width, height 크기와 브라우저 상의 크기가 일치
