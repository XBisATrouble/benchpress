# 卧推增力计划 Web 页面实现计划

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 构建一个纯静态 HTML 页面，用户输入卧推最大重量后自动计算 4 个训练级别的各组重量，并支持一键保存为图片，部署到 GitHub Pages。

**Architecture:** 单文件 `index.html`，内含全部 HTML/CSS/JS。训练数据硬编码为 JS 常量，重量计算纯前端完成。截图使用 CDN 引入的 `html2canvas` 库。

**Tech Stack:** HTML5, CSS3, Vanilla JavaScript, html2canvas (CDN), GitHub Pages

---

### Task 1: 初始化 Git 仓库并创建基础 HTML 骨架

**Files:**
- Create: `index.html`
- Create: `README.md`

**Step 1: 初始化 git 仓库**

```bash
cd /Users/xubinxbchen/Desktop/Workshop/benchpress
git init
git add docs/
git commit -m "docs: add design and implementation plan"
```

**Step 2: 创建 README.md**

```markdown
# 卧推增力计划

卧推渐进式力量训练计划计算器。输入你的最大重量（1RM），自动生成各训练级别的组次安排。

## 使用

访问：https://<username>.github.io/benchpress
```

**Step 3: 创建 index.html 基础骨架**

创建 `index.html`，内容如下：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>卧推增力计划</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    /* 样式占位，Task 2 填充 */
  </style>
</head>
<body>
  <div id="app">
    <h1>卧推增力计划</h1>
    <p>页面骨架</p>
  </div>
  <script>
    // JS 占位，Task 3 填充
  </script>
</body>
</html>
```

**Step 4: 提交骨架**

```bash
git add index.html README.md
git commit -m "feat: add html skeleton and readme"
```

---

### Task 2: 添加完整 CSS 样式

**Files:**
- Modify: `index.html`（`<style>` 块）

**Step 1: 替换 `<style>` 占位内容为完整样式**

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: #1a1a1a;
  color: #f0f0f0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  min-height: 100vh;
  padding: 24px 16px;
}

#app {
  max-width: 1100px;
  margin: 0 auto;
}

h1 {
  text-align: center;
  font-size: 1.8rem;
  color: #f5a623;
  margin-bottom: 24px;
  letter-spacing: 0.05em;
}

/* 输入区域 */
.input-section {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  margin-bottom: 32px;
  flex-wrap: wrap;
}

.input-section label {
  font-size: 1rem;
  color: #ccc;
}

.input-section input {
  width: 100px;
  padding: 8px 12px;
  font-size: 1.1rem;
  background: #2a2a2a;
  border: 2px solid #444;
  border-radius: 8px;
  color: #f0f0f0;
  text-align: center;
  outline: none;
  transition: border-color 0.2s;
}

.input-section input:focus {
  border-color: #f5a623;
}

.input-section .unit {
  color: #aaa;
  font-size: 0.95rem;
}

button.calc-btn {
  padding: 8px 20px;
  background: #f5a623;
  color: #1a1a1a;
  font-size: 1rem;
  font-weight: 700;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

button.calc-btn:hover {
  background: #e09510;
}

/* 卡片网格 */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-bottom: 32px;
}

@media (max-width: 800px) {
  .cards-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .cards-grid {
    grid-template-columns: 1fr;
  }
}

/* 训练卡片 */
.card {
  background: #242424;
  border: 1px solid #333;
  border-radius: 12px;
  overflow: hidden;
}

.card-header {
  background: #f5a623;
  color: #1a1a1a;
  text-align: center;
  padding: 10px;
  font-size: 1rem;
  font-weight: 700;
  letter-spacing: 0.05em;
}

.card table {
  width: 100%;
  border-collapse: collapse;
}

.card table th {
  background: #2e2e2e;
  color: #aaa;
  font-size: 0.75rem;
  padding: 6px 8px;
  text-align: center;
  border-bottom: 1px solid #333;
}

.card table td {
  padding: 8px;
  text-align: center;
  font-size: 0.9rem;
  border-bottom: 1px solid #2e2e2e;
}

.card table tr:last-child td {
  border-bottom: none;
}

.card table tr:nth-child(even) td {
  background: #272727;
}

.weight-cell {
  color: #f5a623;
  font-weight: 700;
  font-size: 1rem;
}

/* 保存按钮 */
.save-section {
  text-align: center;
}

button.save-btn {
  padding: 12px 36px;
  background: #2a2a2a;
  color: #f5a623;
  font-size: 1rem;
  font-weight: 700;
  border: 2px solid #f5a623;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}

button.save-btn:hover {
  background: #f5a623;
  color: #1a1a1a;
}

button.save-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

**Step 2: 在浏览器打开 index.html 目视验证样式（无数据状态下背景、字体颜色正常）**

```bash
open /Users/xubinxbchen/Desktop/Workshop/benchpress/index.html
```

**Step 3: 提交**

```bash
git add index.html
git commit -m "feat: add full CSS styling"
```

---

### Task 3: 实现 HTML 结构（输入区 + 卡片区 + 保存按钮）

**Files:**
- Modify: `index.html`（`<body>` 中 `#app` 内容）

**Step 1: 替换 `<body>` 中 `#app` 内容**

```html
<div id="app">
  <h1>卧推增力计划</h1>

  <div class="input-section">
    <label for="maxWeight">最大重量</label>
    <input type="number" id="maxWeight" value="95" min="1" max="500" step="0.5">
    <span class="unit">kg</span>
    <button class="calc-btn" onclick="calculate()">计算</button>
  </div>

  <div class="cards-grid" id="cardsGrid">
    <!-- 由 JS 动态生成 -->
  </div>

  <div class="save-section">
    <button class="save-btn" onclick="saveImage()">保存图片</button>
  </div>
</div>
```

**Step 2: 目视验证 HTML 结构正常渲染（输入框、按钮可见）**

```bash
open /Users/xubinxbchen/Desktop/Workshop/benchpress/index.html
```

**Step 3: 提交**

```bash
git add index.html
git commit -m "feat: add html structure for input and cards"
```

---

### Task 4: 实现核心 JavaScript 逻辑

**Files:**
- Modify: `index.html`（`<script>` 块）

**Step 1: 替换 `<script>` 占位内容为完整 JS**

```javascript
// 训练数据（比例 ratio，次数 reps）
const LEVELS = [
  {
    name: '级别一',
    sets: [
      { ratio: 0.50, reps: '10' },
      { ratio: 0.70, reps: '5' },
      { ratio: 0.85, reps: '3' },
      { ratio: 0.85, reps: '5' },
      { ratio: 0.70, reps: '10' },
      { ratio: 0.60, reps: '10' },
    ]
  },
  {
    name: '级别二',
    sets: [
      { ratio: 0.50, reps: '10' },
      { ratio: 0.75, reps: '5' },
      { ratio: 0.85, reps: '3' },
      { ratio: 0.90, reps: '2~3' },
      { ratio: 0.85, reps: '5' },
      { ratio: 0.80, reps: '7' },
    ]
  },
  {
    name: '级别三',
    sets: [
      { ratio: 0.50, reps: '10' },
      { ratio: 0.65, reps: '7' },
      { ratio: 0.75, reps: '5' },
      { ratio: 0.85, reps: '3' },
      { ratio: 1.00, reps: '1~2' },
      { ratio: 0.85, reps: '5' },
    ]
  },
  {
    name: '级别四',
    sets: [
      { ratio: 0.50, reps: '10' },
      { ratio: 0.70, reps: '5' },
      { ratio: 0.85, reps: '2' },
      { ratio: 1.05, reps: '1~2' },
      { ratio: 1.00, reps: '1' },
      { ratio: 0.85, reps: '5' },
    ]
  }
];

// 格式化重量：整数不显示小数，否则保留1位
function formatWeight(w) {
  return Number.isInteger(w) ? String(w) : w.toFixed(1);
}

// 渲染所有卡片
function calculate() {
  const maxWeight = parseFloat(document.getElementById('maxWeight').value);
  if (!maxWeight || maxWeight <= 0) return;

  const grid = document.getElementById('cardsGrid');
  grid.innerHTML = '';

  LEVELS.forEach(level => {
    const card = document.createElement('div');
    card.className = 'card';

    const rows = level.sets.map((s, i) => {
      const weight = s.ratio * maxWeight;
      return `
        <tr>
          <td>${i + 1}</td>
          <td class="weight-cell">${formatWeight(weight)} kg</td>
          <td>${s.reps}</td>
        </tr>`;
    }).join('');

    card.innerHTML = `
      <div class="card-header">${level.name}</div>
      <table>
        <thead>
          <tr>
            <th>组</th>
            <th>重量</th>
            <th>次数</th>
          </tr>
        </thead>
        <tbody>${rows}</tbody>
      </table>`;

    grid.appendChild(card);
  });
}

// 保存图片
function saveImage() {
  const btn = document.querySelector('.save-btn');
  const grid = document.getElementById('cardsGrid');
  const maxWeight = document.getElementById('maxWeight').value;

  btn.disabled = true;
  btn.textContent = '保存中...';

  html2canvas(grid, {
    backgroundColor: '#1a1a1a',
    scale: 2,
  }).then(canvas => {
    const a = document.createElement('a');
    a.href = canvas.toDataURL('image/png');
    a.download = `benchpress-${maxWeight}kg.png`;
    a.click();
  }).finally(() => {
    btn.disabled = false;
    btn.textContent = '保存图片';
  });
}

// 支持回车触发计算
document.getElementById('maxWeight').addEventListener('keydown', e => {
  if (e.key === 'Enter') calculate();
});

// 页面加载后自动计算一次
calculate();
```

**Step 2: 在浏览器验证功能**

```bash
open /Users/xubinxbchen/Desktop/Workshop/benchpress/index.html
```

验证清单：
- [ ] 页面加载后 4 张卡片自动显示（基于默认 95kg）
- [ ] 修改最大重量后点击"计算"，重量正确更新
- [ ] 回车键触发计算
- [ ] 点击"保存图片"，弹出下载，文件名含最大重量

**Step 3: 提交**

```bash
git add index.html
git commit -m "feat: implement calculation and save-image logic"
```

---

### Task 5: 部署到 GitHub Pages

**Files:** 无新文件，仅 git 操作

**Step 1: 在 GitHub 创建新仓库**

在 https://github.com/new 创建名为 `benchpress` 的公开仓库（不勾选 Initialize）。

**Step 2: 推送代码**

```bash
cd /Users/xubinxbchen/Desktop/Workshop/benchpress
git remote add origin https://github.com/<your-username>/benchpress.git
git branch -M main
git push -u origin main
```

**Step 3: 启用 GitHub Pages**

在仓库 Settings → Pages → Source 选择 `main` 分支，根目录 `/`，保存。

**Step 4: 验证部署**

等待约 1 分钟后访问：
```
https://<your-username>.github.io/benchpress
```

验证清单：
- [ ] 页面正常加载
- [ ] 4 张训练卡片显示
- [ ] 移动端布局正常（2 列）
- [ ] 保存图片功能正常

---

## 完成标准

- `index.html` 单文件，无构建步骤
- 输入任意正数最大重量，4 个级别的重量实时更新
- 保存图片文件名格式：`benchpress-{n}kg.png`，分辨率 2x
- GitHub Pages 可公开访问
