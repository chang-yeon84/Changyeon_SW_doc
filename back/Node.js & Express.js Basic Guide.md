-----

### **📚 Node.js & Express.js 시작 가이드**

이 문서는 Node.js를 활용한 백엔드 개발의 핵심 개념과 Express.js를 이용한 API 구축 방법을 설명합니다.

#### **1. Node.js란? 🌐**

**Node.js**는 \*\*"브라우저 밖에서 JavaScript를 실행할 수 있는 환경"\*\*입니다. 웹 브라우저가 아니라 서버나 컴퓨터에서도 JavaScript 코드를 구동할 수 있도록 해주는 도구입니다.

  * **비동기 방식**: 여러 작업을 동시에 처리해 서버의 효율과 속도를 높입니다.
  * **단일 언어**: 프론트엔드와 백엔드 모두 JavaScript를 사용해 개발 언어를 통일할 수 있습니다.

#### **2. `npm`: Node.js의 패키지 매니저**

`npm`(Node Package Manager)은 Node.js에 필요한 다양한 모듈(라이브러리)을 설치하고 관리하는 도구입니다.

  * `npm init -y`: 프로젝트를 초기화하고 `package.json` 파일을 생성합니다.
  * `npm install [패키지명]`: 필요한 패키지를 설치합니다. (예: `npm install express`)

-----

### **3. Node.js로 백엔드 구축하기**

백엔드는 앱의 **데이터를 관리하고 API를 제공**하는 서버 측 역할을 합니다. Node.js는 이런 API 서버를 구축하는 데 매우 강력하고 적합합니다. 캘린더 앱은 사용자 일정, 날씨, 교통 정보 등을 관리해야 하므로 백엔드 서버가 필수적입니다.

-----

### **4. Express.js와 CRUD API**

\*\*`Express.js`\*\*는 Node.js로 웹 서버와 API를 쉽고 빠르게 만들 수 있도록 도와주는 **프레임워크**입니다. 복잡한 서버 코드를 간결하게 작성할 수 있게 해줍니다.

#### CRUD란?

`CRUD`는 데이터베이스나 API에서 수행하는 4가지 기본 작업을 의미합니다.

  * **C**reate (생성): 새로운 데이터 추가 (예: `POST` 요청으로 새 일정 추가)
  * **R**ead (조회): 데이터 조회 (예: `GET` 요청으로 일정 목록 가져오기)
  * **U**pdate (수정): 기존 데이터 변경 (예: `PUT` 요청으로 일정 내용 수정)
  * **D**elete (삭제): 데이터 삭제 (예: `DELETE` 요청으로 일정 삭제)

#### Express.js로 간단한 CRUD API 만들기

아래 예시는 `Express.js`를 이용해 **`Read`** 작업을 수행하는 간단한 API 서버 코드입니다.

```javascript
// express 모듈 불러오기
const express = require('express');
const app = express();
const port = 3000;

// /api/schedule 경로로 들어오는 GET 요청을 처리합니다.
app.get('/api/schedule', (req, res) => {
  // 실제로는 데이터베이스에서 일정을 가져옵니다.
  const userSchedule = [
    { id: 1, task: "점심 식사", time: "12:30" },
    { id: 2, task: "프로젝트 회의", time: "15:00" }
  ];
  
  // JSON 형식으로 클라이언트에게 응답을 보냅니다.
  res.json(userSchedule);
});

// 서버를 시작하고 3000번 포트에서 요청을 기다립니다.
app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```

-----

### **1. Express.js 모듈 불러오기 (`require`)**

```javascript
const express = require('express');
const app = express();
const port = 3000;
```

  * `const express = require('express');`: 이 코드는 외부에서 설치한 `express` 모듈을 불러와 사용할 준비를 합니다. 마치 요리를 하기 전에 식재료(express)를 냉장고에서 꺼내는 것과 같아요.
  * `const app = express();`: 불러온 `express` 모듈을 사용해서 실제 웹 애플리케이션 객체(`app`)를 생성합니다. 이 `app` 객체가 바로 당신이 만들 **API 서버의 설계도** 역할을 합니다.
  * `const port = 3000;`: 서버가 실행될 포트 번호를 정의합니다. `3000번`은 개발 환경에서 주로 사용되는 포트 번호 중 하나입니다.

-----

### **2. API 엔드포인트 정의하기 (`app.get`)**

```javascript
app.get('/api/schedule', (req, res) => {
  // ... 요청 처리 로직
});
```

  * `app.get()`: 클라이언트의 **`GET` 요청**을 처리하겠다는 것을 의미합니다. 웹 브라우저 주소창에 URL을 입력하는 것이 가장 대표적인 `GET` 요청 방식이에요. 데이터를 가져올 때 사용합니다.
  * `'/api/schedule'`: 이것은 API의 \*\*URL 경로(Endpoint)\*\*를 정의합니다. 클라이언트는 `http://localhost:3000/api/schedule` 주소로 요청을 보내게 됩니다.
  * `(req, res) => { ... }`: 이 부분은 콜백 함수(Callback Function)로, 클라이언트의 요청이 들어왔을 때 실행될 코드 블록입니다. `req` 객체에는 \*\*요청(request)\*\*에 대한 정보(요청 데이터, 헤더 등)가 담겨 있고, `res` 객체는 서버가 \*\*응답(response)\*\*을 보낼 때 사용하는 객체입니다.

-----

### **3. 요청 처리 및 데이터 준비하기**

```javascript
  const userSchedule = [
    { id: 1, task: "점심 식사", time: "12:30" },
    { id: 2, task: "프로젝트 회의", time: "15:00" }
  ];
```

  * 이 부분은 클라이언트의 요청을 실제로 처리하는 로직입니다. 현재는 `userSchedule`이라는 변수에 미리 정의된 더미(dummy) 데이터를 배열 형태로 저장하고 있습니다.
  * 실제 서비스에서는 이 코드가 데이터베이스에 접속해서 사용자의 일정을 조회하고, 그 결과를 `userSchedule` 변수에 담는 역할을 하게 됩니다.

-----

### **4. JSON 형태로 응답 보내기 (`res.json`)**

```javascript
  res.json(userSchedule);
```

  * `res.json()`: 서버가 클라이언트로 데이터를 보낼 때, **JSON(JavaScript Object Notation)** 형식으로 변환하여 응답을 보내주는 메소드입니다. JSON은 웹에서 데이터를 주고받을 때 가장 널리 사용되는 표준 형식이에요.
  * 이 코드를 통해 `userSchedule` 배열이 자동으로 JSON 문자열로 변환되어 클라이언트에 전달됩니다.

-----

### **5. 서버 실행하기 (`app.listen`)**

```javascript
app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```

  * `app.listen(port, ...)`: 이 코드는 서버를 실행하고, 지정된 포트(`3000번`)에서 클라이언트의 요청을 기다리게 합니다. 마치 가게 문을 열고 손님을 기다리는 것과 같아요.
  * 두 번째 인자인 콜백 함수는 서버가 성공적으로 시작되었을 때 실행됩니다. 터미널에 `Server is running at...` 메시지가 표시되는 것은 서버가 정상적으로 작동하고 있다는 의미입니다.
