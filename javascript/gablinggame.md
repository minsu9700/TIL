# 자바스크립트 이벤트 객체 활용 
***
## 숫자 3개(0~2 랜덤값)를 두고 3개가 모두 일치하면 성공을 일치하지 않으면 실패를 출력하는 게임

```html

<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>겜블링게임</title>
</head>
<body>
    <h3>겜블링 게임</h3>
    <p>각 숫자를 클릭하면 0에서 2사이의 난수로 바뀝니다. 모두 같은 수가 나오면 승리합니다.</p>
    <hr>

    <div>
        <span id="first">0</span>
        <span id="second">0</span>
        <span id="third">0</span>
    </div>

    <div id="result"></div>

    <script>
        
        first.addEventListener("click", ran_num);  //onclick 리스너로 ran_num 함수 등록
        second.addEventListener("click", ran_num); // onclick 리스너로 ran_num 함수 등록
        third.addEventListener("click", newran_num); //onclick 리스너로 newran_num 함수 등록
        result.addEventListener("click", restart); //onclick 리스너로 restart 함수 등록

       function ran_num(e){ //e는 이벤트 객체

            var obj = e.currentTarget; // 현재 이벤트를 받은 DOM 객체
            obj.innerHTML = Math.floor(Math.random() * 3); 
       }

       function newran_num(e){ //e는 이벤트 객체

            var obj = e.currentTarget; // 현재 이벤트를 받은 DOM 객체
            obj.innerHTML = Math.floor(Math.random() * 3);

            if (first.innerHTML == second.innerHTML && second.innerHTML == third.innerHTML)
            {
                var result = document.getElementById("result");
                result.innerHTML = "Success(click here to do again)"
            }

            else
            {
                var new_result2 = document.getElementById("result");
                new_result2.innerHTML = "fail(click here to do again)";
            }
       }

       function restart(e){ // e는 이벤트 객체
           var obj = e.currentTarget; // 현재 이벤트를 받은 DOM 객체
           obj.innerHTML = "";
           first.innerHTML = 0; // 0으로 초기화
           second.innerHTML = 0; // 0으로 초기화
           third.innerHTML = 0; // 0으로 초기화
       }

    </script>
</body>
</html>
```

### 결과 

![결과](https://user-images.githubusercontent.com/42503786/172754986-dbbe5572-a25d-408e-b1c3-a87fe3da7900.png)
