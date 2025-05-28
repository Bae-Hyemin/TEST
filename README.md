# TEST
외국인전담팀 TEST입니다.
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>사번 조회</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 1rem;
    }
    input, button {
      padding: 8px;
      font-size: 16px;
      margin-right: 8px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #aaa;
      padding: 8px;
      text-align: left;
    }
  </style>
</head>
<body>
  <h2>사번으로 데이터 조회</h2>
  <input type="text" id="employeeId" placeholder="사번 입력" />
  <button onclick="searchData()">조회</button>
  <div id="result"></div>

  <script>
    const scriptUrl = 'https://script.google.com/macros/s/AKfycbzk62DBdmGqrq6OUC2bPid2Vm4a7ymRVslI777muCfSJpUJ_-v1qNKJLGTE--mu76w/exec'; // ← 여기에 본인의 Apps Script Web App URL을 넣으세요

    async function searchData() {
      const empId = document.getElementById('employeeId').value.trim();
      if (!empId) {
        alert("사번을 입력하세요.");
        return;
      }

      try {
        const response = await fetch(`${scriptUrl}?id=${encodeURIComponent(empId)}`);
        const data = await response.json();

        if (data.length === 0) {
          document.getElementById('result').innerHTML = `<p>해당 사번의 데이터를 찾을 수 없습니다.</p>`;
          return;
        }

        // 표 생성
        let table = `<table><thead><tr>`;
        Object.keys(data[0]).forEach(key => {
          table += `<th>${key}</th>`;
        });
        table += `</tr></thead><tbody>`;

        data.forEach(row => {
          table += `<tr>`;
          Object.values(row).forEach(value => {
            table += `<td>${value}</td>`;
          });
          table += `</tr>`;
        });

        table += `</tbody></table>`;
        document.getElementById('result').innerHTML = table;

      } catch (error) {
        console.error(error);
        document.getElementById('result').innerHTML = `<p>데이터를 불러오지 못했습니다.</p>`;
      }
    }
  </script>
</body>
</html>
