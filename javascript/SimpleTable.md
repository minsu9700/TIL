# DOM 객체를 이용하여 간단한 테이블 만들기
***

## 부가설명

1. **border-collapse는 표(table)의 테두리와 셀(td)의 테두리 사이의 간격을 어떻게 처리할 지 결정**
2. **"border-collapse: collapse;"는 표의 테두리와 셀의 테두리 사이의 간격을 없앰. 겹치는 부분은 한 줄로 나타냄**
3. **"document.createElement()"는 지정한 tagname의 HTML 요소(element)를 만드는 메서드(method)**
4. **"Node.appendChild()" 부모 노드에 자식 노드를 추가하는 메서드 오로지 Node 객체만 받을 수 있음 한 번에 하나의 노드만 추가가능**
5. **"inner.HTML" 속성은 HTML 요소 안에 데이터를 추가하는 메서드**



***

### 본문

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Create Simple Table</title>
    <style>
        table{
            border-collapse: collapse;
            border-spacing: 0;
        }
        th,td{
            padding: 10px 20px;
            border: 1px solid #000;
        }
    </style>
</head>
<body id="body">
 
    <script src="script1.js"></script>
</body>
</html>
```
***

### javascript 파일(script1.js)

```javascript

let table = document.createElement("table"); // table 태그 생성
let thead = document.createElement("thead"); // thead 태그 생성
let tbody = document.createElement("tbody"); // tbody 태그 생성

table.appendChild(thead);                   // thead 태그가 table 태그에 귀속
table.appendChild(tbody);                   // tbody 태그가 table 태그에 귀속
document.getElementById('body').appendChild(table); // table태그가 id가 body인 body 태그에 귀속

let row_1 = document.createElement("tr");
let heading_1 = document.createElement("th");
heading_1.innerHTML = "No";                     // 태그 안에 데이터 추가 (innerHTML)
let heading_2 = document.createElement("th");
heading_2.innerHTML = "Name";                   // 태그 안에 데이터 추가 (innerHTML)
let heading_3 = document.createElement("th");
heading_3.innerHTML = "Country";                // 태그 안에 데이터 추가 (innerHTML)

row_1.appendChild(heading_1);
row_1.appendChild(heading_2);
row_1.appendChild(heading_3);
thead.appendChild(row_1);

let row_2 = document.createElement("tr");
let row_2_data_1 = document.createElement("td");
row_2_data_1.innerHTML = "1.";
let row_2_data_2 = document.createElement("td");
row_2_data_2.innerHTML="MS";
let row_2_data_3 = document.createElement("td");
row_2_data_3.innerHTML = "KOREA";

row_2.appendChild(row_2_data_1);
row_2.appendChild(row_2_data_2);
row_2.appendChild(row_2_data_3);
tbody.appendChild(row_2);

let row_3 = document.createElement("tr");
let row_3_data_1 = document.createElement("td");
row_3_data_1.innerHTML = "2.";
let row_3_data_2 = document.createElement("td");
row_3_data_2.innerHTML = "LS";
let row_3_data_3 = document.createElement("td");
row_3_data_3.innerHTML = "KOREA";

row_3.appendChild(row_3_data_1);
row_3.appendChild(row_3_data_2);
row_3.appendChild(row_3_data_3);
tbody.appendChild(row_3);
```
***
### display

![simple](https://user-images.githubusercontent.com/42503786/174019605-27adf986-7ce9-40f4-95d6-b23df1164e98.png)
