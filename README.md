# TEST
외국인전담팀 TEST입니다.
<!DOCTYPE html>
<html>
<head>
  <title>사번 조회</title>
  <meta charset="UTF-8">
  <style>
    body { font-family: Arial, sans-serif; margin: 30px; }
    input, button { padding: 10px; font-size: 16px; }
    #result { margin-top: 20px; padding: 10px; background: #f3f3f3; border-radius: 5px; }
  </style>
</head>
<body>
  <h2>사번 조회 시스템</h2>
  <input type="text" id="sabunInput" placeholder="사번 입력" />
  <button onclick="search()">조회</button>
  <div id="result"></div>

  <script>
    async function search() {
      const sabun = document.getElementById("sabunInput").value.trim();
      const url = "https://script.google.com/macros/s/여기에_복사한_웹앱_URL/exec?sabun=" + sabun;
      
      try {
        const response = await fetch(url);
        const text = await response.text();
        let content;

        try {
          const json = JSON.parse(text);
          content = Object.entries(json)
            .map(([key, value]) => `<b>${key}:</b> ${value}`)
            .join("<br>");
        } catch {
          content = `<span style="color:red">${text}</span>`;
        }

        document.getElementById("result").innerHTML = content;
      } catch (err) {
        document.getElementById("result").innerHTML = "오류 발생: " + err;
      }
    }
  </script>
</body>
</html>
