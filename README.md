# sparta moviestars

- 사용 패키지

  - flask
  - pymongo
  - requests
  - bs4

- 프로젝트를 시작하기 전에 먼저 데이터를 모아주고 시작하자 (크롤링) - init_db.py

- 만들 API

  1. 조회(Read) 기능: 영화인 정보 전체를 조회
  2. 좋아요(Update) 기능: 클라이언트에서 받은 이름(name_give)으로 찾아서 좋아요(like)를 증가
  3. 삭제(Delete) 기능: 클라이언트에서 받은 이름(name_give)으로 영화인을 찾고, 해당 영화인을 삭제

- GET연습 (보여주기)
  - 우리가 만들 기능은 영화인 정보를 카드로 보여주기(Read) 이다.
  - 개발자 도구 - 검사에서 어떤 요소에 어떤 데이터가 보일지 분석해보자.
    - 영화인 이름
    - 영화인 이미지 : 이미지 src 속성
    - 좋아요 개수
    - 최근 작품 내용이 들어가는 부분
  - API 만들고 사용하기 - 영화인 조회 API (Read -> GET)
    1. 요청 정보
    - 요청 URL = /api/list, 요청 방식 = GET
    - 요청 데이터: 없음
    2. 서버가 제공할 기능
    - 데이터 베이스에 영화인 정보를 조회(Read)하고, 영화인 정보를 응답 데이터로 보냄
    3. 응답 데이터: (JSON 형식) 'stars_list' = 영화인 정보 리스트
  - 순서
    1. 클라이언트와 서버 연결 확인하기 (함수에 대한 연결, 동작 테스트)
    2. 서버부터 만들기
    - 서버 로직
      1. mystar 목록 전체를 검색. id는 제외하고 like가 많은 순으로 정렬
      2. 성공하면 success 메세지와 함께 stars_list 목록을 클라이언트에 전달
    3. 클라이언트 만들기
    - 클라이언트 로직
      1. #star_box의 내부 html 태그를 모두 삭제
      2. 서버에 1) GET 방식으로, 2) /api/list 라는 주소로 stars_list를 요청
      3. 서버가 돌려준 stars_list를 stars라는 변수에 저장
      4. for 문을 활용해서 stars 배열의 요소를 차례대로 조회
      5. stars[i] 요소의 name, url, img_url, recent, like 키값을 활용하여 값 조회
      6. 영화인 카드 코드 만들어 #star-box에 붙이기
    4. 완성 확인하기
    - 동작 테스트 : 새로고침 했을 때 영화인 정보가 조회되는지 확인
