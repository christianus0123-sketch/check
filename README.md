<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>☀️ 아침 조회 출석</title>
  <style>
    /* 전체 배경 및 폰트 설정 */
    body {
      font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, sans-serif;
      background-color: #f4f7f6; /* 부드러운 파스텔톤 배경 */
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      padding: 20px;
      box-sizing: border-box;
    }

    /* 출석 입력창 박스 디자인 */
    .container {
      background-color: #ffffff;
      padding: 30px 25px;
      border-radius: 16px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05); /* 은은한 그림자 효과 */
      width: 100%;
      max-width: 400px; /* PC에서도 너무 넓어지지 않게 고정 */
    }

    h2 {
      text-align: center;
      color: #333333;
      margin-bottom: 25px;
      font-size: 24px;
    }

    /* 각 입력 항목(학번, 이름 등)의 간격 */
    .form-group {
      margin-bottom: 20px;
    }

    /* 항목 제목(라벨) 디자인 */
    label {
      display: block;
      font-weight: 600;
      margin-bottom: 8px;
      color: #555555;
      font-size: 14px;
    }

    /* 입력칸 및 선택창 디자인 */
    input[type="text"], select {
      width: 100%;
      padding: 14px;
      border: 1px solid #e0e0e0;
      border-radius: 8px;
      font-size: 16px; /* 모바일 화면 확대 방지용 크기 */
      box-sizing: border-box;
      background-color: #fafafa;
      transition: border-color 0.3s;
    }

    /* 입력칸 클릭 시 테두리 색상 변화 */
    input[type="text"]:focus, select:focus {
      outline: none;
      border-color: #4CAF50;
      background-color: #ffffff;
    }

    /* 제출 버튼 디자인 */
    button {
      width: 100%;
      padding: 16px;
      background-color: #4CAF50; /* 편안한 초록색 메인 컬러 */
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
      margin-top: 10px;
    }

    button:hover {
      background-color: #45a049;
    }

    button:disabled {
      background-color: #cccccc;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>☀️ 아침 조회 출석</h2>
    
    <form id="checkInForm">
      <div class="form-group">
        <label for="id">학번</label>
        <input type="text" id="id" placeholder="예: 30101" required>
      </div>

      <div class="form-group">
        <label for="name">이름</label>
        <input type="text" id="name" placeholder="이름을 입력하세요" required>
      </div>
      
      <div class="form-group">
        <label for="mood">오늘의 기분</label>
        <select id="mood" required>
          <option value="" disabled selected>기분을 선택해주세요</option>
          <option value="😎 최고예요">😎 최고예요</option>
          <option value="🙂 좋아요">🙂 좋아요</option>
          <option value="😐 보통이에요">😐 보통이에요</option>
          <option value="🥱 피곤해요">🥱 피곤해요</option>
          <option value="🤒 아파요">🤒 아파요</option>
        </select>
      </div>
      
      <div class="form-group">
        <label for="todayGoal">오늘의 목표</label>
        <input type="text" id="todayGoal" placeholder="오늘 하루 다짐 한 마디!" required>
      </div>

      <button type="button" id="submitBtn" onclick="submitData()">출석하기</button>
    </form>
  </div>

  <script>
    function submitData() {
      // 입력값 확인 (빈칸 검사)
      const id = document.getElementById("id").value;
      const name = document.getElementById("name").value;
      const mood = document.getElementById("mood").value;
      const todayGoal = document.getElementById("todayGoal").value;

      if(!id || !name || !mood || !todayGoal) {
        alert("모든 항목을 입력해주세요.");
        return;
      }

      // 버튼 상태 변경 (중복 제출 방지)
      const submitBtn = document.getElementById("submitBtn");
      submitBtn.innerText = "제출 중...";
      submitBtn.disabled = true;

      // ★ 아래 따옴표 안에 선생님의 앱스스크립트 웹앱 배포 링크를 붙여넣으세요.
      const url = "https://script.google.com/macros/s/AKfycbxVnB3H_ur2EmqwBRbhKVkZCg_i_um72TEAZGTWxvQXXDdjbrxb9htMStjQToeN6eE/exec";
      
      const data = { id, name, mood, todayGoal };

      fetch(url, {
        method: "POST",
        headers: { "Content-Type": "text/plain;charset=utf-8" },
        body: JSON.stringify(data)
      })
      .then(response => {
        alert("✅ 출석이 완료되었습니다!");
        document.getElementById("checkInForm").reset();
      })
      .catch(error => {
        alert("❌ 오류가 발생했습니다. 다시 시도해 주세요.");
      })
      .finally(() => {
        // 전송이 끝나면 버튼 상태 원래대로 복구
        submitBtn.innerText = "출석하기";
        submitBtn.disabled = false;
      });
    }
  </script>
</body>
</html>
