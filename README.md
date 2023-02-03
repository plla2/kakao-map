# Kakao API활용 지역,이름으로 검색
React + kakao API + styled-components를 활용

## 🗺️ Repo 소개
검색창을 만들어 그곳에 장소나 도로 주소 등을 입력하면 지도상에 마크업되는 형태로 만들었습니다.

## 🖋️ 주요 기능
```
const options = {
      center: new kakao.maps.LatLng(33.450701, 126.570667),
      level: 3,
    };
```
위의 코드를 통해 첫 화면이 마운팅되고 뜨는 지도는 center값이 되고 축척을 level을 통해 정해준다.</br>


```
function displayPagination(pagination) {
      let paginationEl = document.getElementById("pagination"),
        fragment = document.createDocumentFragment(),
        i;
```
위의 코드로 검색결과 목록 하단에 페이지 번호를 표시하여 페이지가 2개이상일 때 옮길 수 있게해준다.

## ❌ 에러내용 및 해결
1. ```TypeError: Cannot read properties of undefined (reading 'map')``` </br></br>
에러 설명:
구글링을 통해 []빈배열로 값이 없기 때문에 map을 할 수가 없다는 것이였다.
React 는 렌더링이 화면에 커밋 된 후에야 모든 효과를 실행한다.
즉, React는 return에서 XXX.map(...)을 반복실행할 때,첫 턴에 데이터가 아직 안들어와도 렌더링이 실행되며 당연히 그 데이터는 undefined로 정의되어 오류가 나는 것이다. </br></br>
해결방법: 처음 node에서 에러가 생겨 주석처리한 let markers = [];을 주석해제 하여 에러를 해결하였다.</br>또, <script type=“text/javascript” src="//dapi.kakao.com/v2/maps/sdk.js?appkey=********&libraries=services&autoload=false"></script>를 입력하는 과정에서 잘못된 띄어쓰기가 존재해서 찾아내어 삭제하였다. </br></br></br>
2. ```Uncaught TypeError: Cannot set properties of undefined (setting backgroundColor)``` </br></br>
에러설명:  JS에서 정의되지 않은 속성을 사용하여 뜬 에러라고한다. </br></br>
해결방법:  backgroundColor대신&nbsp;color:""값을 사용하여 에러를 해결하였다.</br></br>
3. ```window.kakao.maps.LatLng is not a constructor``` </br></br>
에러설명: v3 스크립트를 동적으로 로드하기위해 사용한다.
스크립트의 로딩이 끝나기 전에 v3의 객체에 접근하려고 하면 에러가 발생하기 때문에
로딩이 끝나는 시점에 콜백을 통해 객체에 접근할 수 있도록 해 준다.
비동기 통신으로 페이지에 v3를 동적으로 삽입할 경우 react에 주로 사용된다.
v3 로딩 스크립트 주소에 파라메터로 autoload=false 를 지정해 주어야 한다.</br></br>
해결방법:
    ``` 
    <script type="text/javascript" src="http://dapi.kakao.com/v2/maps/sdk.js
    autoload=false"></script>
    <script type="text/javascript">
    kakao.maps.load(function() {
    const  map = new kakao.maps.Map(node, options);
    });
    </script>
    ``` 
    를 index.html head안에 넣어주어 해결하였다.
    
## ⚙️ Prerequisites
<ul>
<li>npm >= 6.0.0
<li>react >= 18.2.0
<li>styled-components >= 5.3.6
</ul>

### Install
```npx create-react-app .```</br>
```npm install styled-components```</br>
```
<script
type="text/javascript"
src="//dapi.kakao.com/v2/maps/sdk.js
appkey="kakao API에서 가져온 키"&libraries=services&autoload=false"
></script>
```

## 🖥️ 실행화면
첫 마운팅후 화면</br></br>
<img width="763" alt="스크린샷 2023-02-03 오후 3 15 53" src="https://user-images.githubusercontent.com/120915990/216526471-395aeec1-3b6a-4b16-a2df-b41e6fb1d324.png"></br></br>
"제주도"를 검색후 화면</br></br>
<img width="754" alt="스크린샷 2023-02-03 오후 3 18 05" src="https://user-images.githubusercontent.com/120915990/216526781-e96bac9a-147e-4958-9963-96bde13cecba.png"></br></br>
검색결과가 많을때 페이지를 넘길 수 있는 버튼</br></br>
<img width="752" alt="스크린샷 2023-02-03 오후 3 19 37" src="https://user-images.githubusercontent.com/120915990/216526985-45957d7b-9db1-4767-b0b7-9b88c5d4f903.png">



