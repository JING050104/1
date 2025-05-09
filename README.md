<html lang="zh">
<head>
  <meta charset="UTF-8">
  <title>Teacher Awards 2025</title>
    <style>
    body {
      font-family: 'Roboto', sans-serif;
      background-color: #f8f9fa;
      padding: 30px;
      color: #202124;
    }
    h2 {
      text-align: left;
      color: #1a73e8;
    }
    .card {
      background-color: white;
      border-radius: 8px;
      box-shadow: 0 1px 3px rgba(60,64,67,0.3);
      padding: 20px;
      margin-bottom: 20px;
    }
    label {
      display: block;
      font-weight: bold;
      margin-bottom: 8px;
      color: #202124;
    }
    select {
      width: 100%;
      padding: 10px;
      border: 1px solid #dadce0;
      border-radius: 4px;
      font-size: 16px;
      background-color: white;
      appearance: none;
    }
    button {
      background-color: #1a73e8;
      color: white;
      font-size: 16px;
      padding: 12px 24px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      display: block;
      margin: 20px auto;
    }
    button:hover {
      background-color: #1765cc;
    }
  </style>
</head>
<body>
  <h1>Teacher Awards 2025: The Yik Chiao Teacher Star Poll</h1>
  <h2>你心目中的“教师之星”是谁？⭐  <br>
是那个讲课超有梗、考试还会偷偷提示的“神助攻老师”？   <br>
还是每天像福尔摩斯一样盯作业、却又偷偷关心你的“刀子嘴豆腐心老师”？👀 <br>
 <br>
【益侨教师之星】票选正式开始啦！   <br>
用你宝贵的一票，向你最爱的老师送上最闪亮的荣誉～✨ <br>
 <br>
📌 规则简单：   <br>
- 每人只能投一次票哦（公平公正，老师不许贿选！）   <br>
- 按照你真实的感受选择就对了，老师不会生气，真的！ <br>
-给每个老师一票，不要重复选！让票选更神圣！ <br>
 <br>
快来投票吧🏆<h2/>
  <form id="voteForm">
    <label>中文姓名：</label>
    <input type="text" name="name" required><br>

    <label>班级：</label>
    <select name="class" required>
      <option value="">请选择班级</option>
      <option value="1R">1R</option>
      <option value="2R">2R</option>
      <option value="3R">3R</option>
      <option value="4R">4R</option>
      <option value="4Y">4Y</option>
      <option value="5R">5R</option>
      <option value="6R">6R</option>
      <option value="6Y">6Y</option>
    </select><br>

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

    const selected = new Map();

    function renderOptions(currentIndex) {
      return teachers.filter(t => {
        // 只排除其他下拉框中选的老师
        for (const [key, val] of selected) {
          if (key !== currentIndex && val === t) return false;
        }
        return true;
      });
    }

    function createAwardSelect(index, awardName) {
      const label = document.createElement("label");
      label.textContent = awardName;

      const select = document.createElement("select");
      select.name = `award${index}`;
      select.dataset.index = index;
      select.required = true;

      const render = () => {
        const currentValue = selected.get(index) || "";
        const options = renderOptions(index);
        select.innerHTML = '<option value="">请选择老师</option>';
        options.forEach(teacher => {
          const option = document.createElement("option");
          option.value = teacher;
          option.textContent = teacher;
          if (teacher === currentValue) option.selected = true;
          select.appendChild(option);
        });
      };

      select.addEventListener("change", () => {
        selected.set(index, select.value);
        document.querySelectorAll("select[data-index]").forEach(sel => {
          const i = Number(sel.dataset.index);
          renderOptions(i).forEach((teacher) => {
            if (![...sel.options].some(o => o.value === teacher)) {
              const option = document.createElement("option");
              option.value = teacher;
              option.textContent = teacher;
              sel.appendChild(option);
            }
          });
          [...sel.options].forEach(option => {
            if (
              option.value &&
              !renderOptions(i).includes(option.value) &&
              sel.value !== option.value
            ) {
              option.remove();
            }
          });
        });
      });

      // 初始化渲染
      render();

      return [label, select];
    }

    window.addEventListener("DOMContentLoaded", () => {
      const container = document.getElementById("awardFields");
      awards.forEach((award, i) => {
        const [label, select] = createAwardSelect(i, award);
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
