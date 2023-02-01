<h1>오류해결</h1>

<h3>1. 콘솔에러:
TypeError: Cannot read properties of undefined (reading 'map')</br></br>
에러 설명:
구글링을 통해 []빈배열로 값이 없기 때문에 map을 할 수가 없다는 것이였다.
React 는 렌더링이 화면에 커밋 된 후에야 모든 효과를 실행한다.
즉, React는 return에서 XXX.map(...)을 반복실행할 때,첫 턴에 데이터가 아직 안들어와도 렌더링이 실행되며 당연히 그 데이터는 undefined로 정의되어 오류가 나는 것이다. </br></br>
해결방법: 처음 node에서 에러가 생겨 주석처리한 let markers = [];을 주석해제 하여 에러를 해결하였다.</br>또, <script type=“text/javascript” src="//dapi.kakao.com/v2/maps/sdk.js?appkey=********&​libraries=services&autoload=false"></script>를 입력하는 과정에서 잘못된 띄어쓰기가 존재해서 찾아내어 삭제하였다. </br></br></br>
<h3>2. 콘솔에러:&nbsp;Uncaught TypeError: Cannot set properties of undefined (setting backgroundColor)</br></br>
에러설명:&nbsp;JS에서 정의되지 않은 속성을 사용하여 뜬 에러라고한다. </br></br>
해결방법:&nbsp;backgroundColor대신&nbsp;color:""값을 사용하여&nbsp; 에러를 해결하였다.</br></br>
<h3> 3.콘솔에러:&nbsp;window.kakao.maps.LatLng is not a constructor</br></br>
에러설명:v3 스크립트를 동적으로 로드하기위해 사용한다.
스크립트의 로딩이 끝나기 전에 v3의 객체에 접근하려고 하면 에러가 발생하기 때문에
로딩이 끝나는 시점에 콜백을 통해 객체에 접근할 수 있도록 해 준다.
비동기 통신으로 페이지에 v3를 동적으로 삽입할 경우( ex> react, vue )에 주로 사용된다.
v3 로딩 스크립트 주소에 파라메터로 autoload=false 를 지정해 주어야 한다.</br></br>해결방법:
<script type="text/javascript" src="http://dapi.kakao.com/v2/maps/sdk.js?autoload=false"></script>
<script type="text/javascript">
kakao.maps.load(function() {
    const  map = new kakao.maps.Map(node, options);
});
</script>를 index.html head안에 넣어주어 해결하였다.
  
