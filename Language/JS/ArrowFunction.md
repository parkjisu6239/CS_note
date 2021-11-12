- **Arrow Function**

  ```jsx
  // 함수 선언식
  function gretting(x){
  	return x*x
  }
  
  // 함수 표현식, 익명함수
  const gretting = function(x){
  	return x*x
  }
  
  // 표현식, 콜백함수의 경우 => 사용 가능
  const gretting = (x) => {
  	return x*x
  }
  
  // + 변수가 하나인 경우 파라미터의 괄호 제거 가능
  const gretting = x=> {
  	return x*x
  }
  
  // { return ~~ } 도 제거 가능
  const gretting = name => x*x
  ```