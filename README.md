<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <title>老师奖项问卷</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      font-family:Times New Roman,Kaiti;
      background-color: #f8f9fa;
      padding: 30px;
      color: #202124;
    }
    h2 {
      text-align: center;
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

<h2>老师奖项投票表单</h2>

<form id="voteForm" onsubmit="submitForm(event)">
  <div id="awardFields"></div>
  <button type="submit">提交问卷</button>
</form>

<script>
  const teachers = [
    "张老师", "李老师", "陈老师", "王老师", "林老师",
    "赵老师", "刘老师", "黄老师", "周老师", "吴老师",
    "郑老师", "谢老师", "曾老师", "许老师", "苏老师",
    "邓老师", "冯老师", "马老师", "高老师", "何老师"
  ];

  const awards = Array.from({ length: 20 }, (_, i) => 奖项 ${i + 1});
  const selections = Array(20).fill("");

  function createForm() {
    const container = document.getElementById("awardFields");
    awards.forEach((award, index) => {
      const card = document.createElement("div");
      card.className = "card";

      const label = document.createElement("label");
      label.textContent = award;

      const select = document.createElement("select");
      select.id = award${index};
      select.dataset.index = index;
      select.onchange = handleSelection;

      card.appendChild(label);
      card.appendChild(select);
      container.appendChild(card);
    });

    updateAllDropdowns();
  }

  function handleSelection(event) {
    const index = parseInt(event.target.dataset.index);
    selections[index] = event.target.value;
    updateAllDropdowns();
  }

  function updateAllDropdowns() {
    const used = new Set(selections.filter(name => name));
    for (let i = 0; i < 20; i++) {
      const select = document.getElementById(award${i});
      const current = selections[i];
      const options = teachers
        .filter(name => !used.has(name) || name === current)
        .map(name => <option value="${name}" ${name === current ? "selected" : ""}>${name}</option>);
      select.innerHTML = <option value="">-- 请选择老师 --</option> + options.join("");
    }
  }

  function submitForm(event) {
    event.preventDefault();
    if (selections.includes("")) {
      alert("请为所有奖项选择老师，且不重复。");
      return;
    }
    console.log("提交成功！数据如下：", selections);
    alert("提交成功！感谢参与投票。");
    // TODO: 将数据提交到 Google Sheets（下一个步骤）
  }

  createForm();
</script>

</body>
</html>
