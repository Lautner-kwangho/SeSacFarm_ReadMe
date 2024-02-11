# SeSacFarm_ReadMe

## 기능
### 1. 로그인 및 회원 가입
  - 사용자가 직접 회원 가입할 수 있습니다
  - 서버로부터 값을 보내기 전 버튼을 통제합니다
  - 로그인 이 후 토근이 만료되는 걸 방지합니다
### 2. CURD
  - 게시물을 작성할 수 있습니다
  - 포스트한 게시물을 조회할 수 있습니다
  - 게시물에 들어간 댓글을 조회할 수 있습니다
  - 삭제 및 수정을 할 수 있습니다
  - 화면을 재사용합니다
### 3. 조건 
  - 기간 : 1월 3일 12시 ~ 1월 6일 20시 (4일간)
  - MVVM 패턴을 사용합니다
  - 라이브러리 Alamofire를 사용하지 않고 서버와 통신을 합니다
  - 디자인의 경우, 정해진 제약이 없으므로 기능 구현을 우선시
  * 서버의 경우 추후 닫음 (영상으로 앱 구성 및 기능 남김)
  ** 서버 URL은 되도록 외부 유출막기 위해 git에 올리지 않음
### 4. 사용 Stack
  - Swift, iOS, URLSession, Snapkit, Then
</br></br>
## 이슈 및 문제해결
### 1. SnapKit 
  - 빨리 layout을 만들기 위해 Snapkit을 사용하여 제작
  - 메인 이미지를 만들 경우, 초기 center, inset, offset, leading, trailing 등을 통하여 만들었음
  - 화면에는 정상적으로 나오나 노란색 경고문이 나와 우선 순위를 설정 약한 오류를 해결함
### 2. URLSession Error 
  - 공통적인 부분을 최소화하고자 함수를 만들어서 문구를 알려줘야 했음
  - 오류를 공통적으로 구분하기 위해 enum을 만들어서 구성하였으나 추후 서비스를 운영한다면 더욱 세부적으로 알려주는 것으로 수정 필요성 느낌
  - 최소 네트워크, response, data, error 등 4 ~ 5 개 오류 구분이 필요했음
### 3. URLSession Model
  - 서버로부터 모델을 만들다 보니 정확하지 않아 계속 수정하면서 만들어야 했음 (데이터는 받아오지만 모델이 맞지 않아 페이지 로딩을 실패함 -> 여기도 오류 세분화하여 상태 확인)
  - 서버 개발자의 역할과 앱 개발자의 역할을 좀 더 잘 알게 되었음
    (예를 들어, 데이터 소팅 관련)
### 4. Genric
  - 제레닉을 선언하고 사용하는데, get, set <-> didSet, willSet에 대하여 지식이 부족한 점이 있었음
  - 다시 한번 내용 정리하는 시간을 가지게 되었음
### 5. Sync vs Async
  - 동기 비동기 관련하여 문제가 발생
  - 데이터는 받아오지만 테이블뷰에는 나오지 않는 현상이 있었음
  - 먼저 데이터를 받아오고(동기처리) 이후 테이블뷰 업데이트(비동기처리) 
### 6. TableView Scroll
  - TableView를 할 경우 데이터를 받아오는데 View가 튀어서 오류 발생 -> 이후 tableViewPrefetch를 사용하여 해결!
### 7. 게시물
  - 게시물과 댓글을 같이 보여주기 위해서 이전 경험을 토대로 쉽게 구현함
  (이전 경험: section을 만들지 않고 cell 1, cell 2로 구분하여 데이터를 구분한 적이 있는데 이렇게 하면 데이터 전달하고 받는데 어려움을 겪었음 왜냐하면 tableView 자체가 재사용을 하고 이름의 중복으로 상세하게 값 전달하기에 부적절함을 느낌)
  - 현재 게시물은 Section 0으로 두고 Section 1은 댓글 영역으로 구분
### 8. 새로고침
  - 단순 조회만 할 경우, 메인 화면에서 데이터를 받아온 뒤에 상세 페이지로 들어가면 받아온 데이터를 더 보여주는 형식이 알맞다고 생각(속도와 네트워크 측면)
  - 댓글을 작성하고 수정 삭제할 경우, 새로고침 해줘야 했기 때문에 위에서 말한 기능은 부적절해보였음 -> 사용자가 작성하고 바로 보여줘야하는 화면의 경우 데이터를 미리 받아오고 보여주기 보다 서버로 요청을 보여주는 게 알맞다고 판단 
### 9. 기간
  - 기간이 짧아 디자인을 신경쓰기 보다 기능 구현에 중점을 두었음 (실제로 새로운 서비스를 만든다면 가벼운 기능부터 만들면 탄탄하게 잡아갈 수 있을지 않을까 생각)

<br/><br/>
## 구현 미리보기
<br/><img src="https://user-images.githubusercontent.com/80211277/156888453-e9462fba-1455-4d3e-be81-f3a03b503556.gif" width="240">   <img src="https://user-images.githubusercontent.com/80211277/156888442-72d33115-0064-4252-96dd-30554d11c153.gif" width="240">

