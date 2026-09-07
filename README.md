# songchaeeun030030.github.io
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>광주 상권 프로토타입</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: sans-serif;
    }
    body {
      margin: 0;
      background: #f5f7fb;
      color: #222;
    }
    .screen {
      display: none;
      padding: 24px 20px;
      max-width: 480px;
      margin: 0 auto;
    }
    .screen.active {
      display: block;
    }
    .card {
      background: white;
      border-radius: 12px;
      padding: 20px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }
    h1 {
      font-size: 22px;
      margin: 0 0 8px;
    }
    p {
      margin: 0 0 16px;
      color: #555;
    }
    button {
      background: #2563eb;
      color: white;
      border: none;
      padding: 12px 18px;
      border-radius: 8px;
      font-size: 16px;
      width: 100%;
      cursor: pointer;
    }
    button.secondary {
      background: #e5e7eb;
      color: #222;
    }
    input, select {
      width: 100%;
      padding: 12px;
      border: 1px solid #ccc;
      border-radius: 8px;
      margin-top: 8px;
      font-size: 16px;
    }
    .result-item {
      border-bottom: 1px solid #eee;
      padding: 14px 0;
    }
    .result-item:last-child {
      border-bottom: none;
    }
    .hint {
      margin-top: 20px;
      font-size: 14px;
      color: #666;
    }
  </style>
</head>
<body>

  <!-- 1) 메인 화면 -->
  <div id="screen-main" class="screen active">
    <div class="card">
      <h1>광주 상권 프로토타입</h1>
      <p>상권 고민을 간단히 입력하면,<br>추천 방향과 체크 포인트를 보여줘요.</p>
      <button onclick="show('screen-input')">시작하기</button>
      <p class="hint">이 프로토타입은 해커톤 시연용 예시입니다.</p>
    </div>
  </div>

  <!-- 2) 상권 입력 화면 -->
  <div id="screen-input" class="screen">
    <div class="card">
      <h1>어떤 상권을 보고 싶나요?</h1>
      <p>예시 데이터를 바탕으로 결과를 보여줘요.</p>

      <label style="display:block; margin-top:16px;">상권 선택</label>
      <select id="region">
        <option value="상무">상무지구</option>
        <option value="충장">충장로/금남로</option>
        <option value="전대">전남대 주변</option>
        <option value="송정">송정역 주변</option>
      </select>

      <label style="display:block; margin-top:16px;">고민 입력</label>
      <input id="concern" type="text" placeholder="예: 유동인구는 많은데 매출이 안 나와요">

      <button onclick="show('screen-result')">결과 보기</button>
      <button class="secondary" onclick="show('screen-main')" style="margin-top:10px;">돌아가기</button>
    </div>
  </div>

  <!-- 3) 결과 화면 -->
  <div id="screen-result" class="screen">
    <div class="card">
      <h1>추천 요약</h1>
      <p id="summary">입력한 상권과 고민을 바탕으로 예시를 보여줘요.</p>

      <div class="result-item">
        <strong>체크 포인트 1</strong>
        <p>유동인구와 방문 목적을 먼저 분리해서 보세요.</p>
      </div>
      <div class="result-item">
        <strong>체크 포인트 2</strong>
        <p>경쟁 가게 밀집도와 시간대별 차이를 확인해보세요.</p>
      </div>
      <div class="result-item">
        <strong>추천 방향</strong>
        <p id="recommend">예시: 시간대별 프로모션 또는 유입 경로 개선</p>
      </div>

      <button class="secondary" onclick="show('screen-input')" style="margin-top:14px;">다시 입력</button>
    </div>
  </div>

  <script>
    function show(id) {
      document.querySelectorAll('.screen').forEach(function(s) {
        s.classList.remove('active');
      });
      document.getElementById(id).classList.add('active');
    }

    // 결과 화면에서 입력값 반영 예시
    document.addEventListener('DOMContentLoaded', function() {
      var regionSelect = document.getElementById('region');
      var concernInput = document.getElementById('concern');

      // 결과 화면으로 넘어갈 때 입력값을 반영해 메시지 바꾸기
      var originalShow = show;
      show = function(id) {
        if (id === 'screen-result') {
          var region = regionSelect.value;
          var concern = concernInput.value.trim() || '상권 고민';
          document.getElementById('summary').textContent =
            region + ' 상권 / "' + concern + '" 기준으로 예시를 보여줘요.';
        }
        originalShow(id);
      };
    });
  </script>

</body>
</html>

