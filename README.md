<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <title>Teacher Awards 2025</title>
  <style>
    body {
      font-family: Times New Roman, KaiTi;
    }
    h1 {
      color: #4CAF50;
    }
    p {
      font-size: 1.2em;
    }
    .form-container {
      border: 1px solid #ddd;
      padding: 20px;
      margin-top: 20px;
      background-color: #f9f9f9;
    }
    label {
      font-weight: bold;
    }
    select, input[type="text"] {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      background-color: #4CAF50;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>
  <h1>Teacher Awards 2025: The Yik Chiao Teacher Star Poll</h1>
  <p>
    你心目中的“教师之星”是谁？⭐<br>
    是那个讲课超有梗、考试还会偷偷提示的“神助攻老师”？<br>
    还是每天像福尔摩斯一样盯作业、却又偷偷关心你的“刀子嘴豆腐心老师”？👀<br><br>
    【益侨教师之星】票选正式开始啦！<br>
    用你宝贵的一票，向你最爱的老师送上最闪亮的荣誉～✨<br><br>
    📌 规则简单：<br>
    - 每人只能投一次票哦（公平公正，老师不许贿选！）<br>
    - 按照你真实的感受选择就对了，老师不会生气，真的！<br>
    - 给每个老师一票，不要重复选！让票选更神圣！<br><br>
    快来投票吧🏆
  </p>

  <form id="voteForm" method="POST" action="https://script.google.com/macros/s/AKfycbzyNlGXrk9FA4mCQIb-AKdbq7lfM-9r3PVpI_UAmGgVcAAudrEMtn67pAHa5-AqoXDbxg/exec">
    <label>中文姓名：</label>
    <input type="text" name="name" required /><br><br>

    <label>班级：</label>
    <select id="class" name="class" required>
      <option value="">请选择班级</option>
      <option value="1R">1R</option>
      <option value="2R">2R</option>
      <option value="3R">3R</option>
      <option value="4R">4R</option>
      <option value="4Y">4Y</option>
      <option value="5R">5R</option>
      <option value="6R">6R</option>
      <option value="6Y">6Y</option>
    </select><br><br>

    <div id="awardFields"></div>

    <button type="submit">提交</button>
  </form>

  <script>
    const teachers = [
      "林金龙校长", "黄莉蚡副校长", "谭锐涟副校长", "陈惠媛副校长",
      "王秀玉师", "张月娇师", "李佩芬师", "徐凯君师", "陈佩仪师",
      "石敏静师", "方采灵师", "李慧琴师", "蓝美蔚师", "Cik Ainnur Zahirah",
      "刘筱莹师", "李丽琴师", "Cik Nurdini Qistina", "郑艺璇师",
      "Pn. Hanizatul Akma", "黄蛟鄕师"
    ];

    const awards = [
      "最有爱心老师 · Most Caring Teacher",
      "最阳光灿烂老师 · Most Cheerful Teacher",
      "最严格有爱的老师 · Strict but Loving Teacher",
      "最有创意老师 · Most Creative Teacher",
      "最搞笑老师 · Most Entertaining Teacher",
      "最有耐心老师 · Most Patient Teacher",
      "最有型老师 · Most Stylish Teacher",
      "最具启发性老师 · Most Inspirational Teacher",
      "最亲民最配合的老师 · Most Approachable Teacher",
      "最勤奋老师 · Most Hardworking Teacher",
      "最冷静沉稳老师 · Most Calm & Composed Teacher",
      "最关怀学生老师 · Most Student-Caring Teacher",
      "最有纪律的老师 · Most Disciplined Teacher",
      "最会用科技的老师 · Most Tech-Savvy Teacher",
      "最有拼劲老师 · Most Spirited Teacher",
      "最可爱活泼老师 · Most Adorable and Energetic Teacher",
      "最有文采老师 · Best Rhymer or Poet Teacher",
      "最幽默又聪明老师 · Funniest but Smartest Teacher",
      "最活跃课外活动老师 · Most Active in Co-curricular Teacher",
      "学校领航之星 · Star of School Drive & Direction"
    ];

    const selectedMap = new Map();

    function generateOptions(exclude = "") {
      return teachers
        .filter(name => ![...selectedMap.values()].includes(name) || name === exclude)
        .map(name => `<option value="${name}">${name}</option>`)
        .join("");
    }

    function refreshAllSelects() {
      document.querySelectorAll("select.teacher-select").forEach(select => {
        const currentValue = select.value;
        select.innerHTML = `<option value="">请选择老师</option>` + generateOptions(currentValue);
        select.value = currentValue; // 保持当前选中值
      });
    }

    window.addEventListener("DOMContentLoaded", () => {
      const container = document.getElementById("awardFields");

      awards.forEach((title, index) => {
        const label = document.createElement("label");
        label.textContent = title;

        const select = document.createElement("select");
        select.name = `award${index + 1}`;
        select.classList.add("teacher-select");
        select.required = true;

        select.innerHTML = `<option value="">请选择老师</option>` + generateOptions();

        select.addEventListener("change", () => {
          selectedMap.set(index, select.value);
          refreshAllSelects();
        });

        container.appendChild(label);
        container.appendChild(document.createElement("br"));
        container.appendChild(select);
        container.appendChild(document.createElement("br"));
        container.appendChild(document.createElement("br"));
      });
    });
  </script>
</body>
</html>
