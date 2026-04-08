<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Финансовый Помощник</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap" rel="stylesheet" />
<style>
  :root {
    --primary-color: #4A90E2;
    --background-gradient: linear-gradient(135deg, #74ebd5 0%, #ACB6E5 100%);
    --card-background: #fff;
    --font-color: #333;
    --border-color: #ddd;
    --button-hover: #357ABD;
    --side-color: #f0f8ff;
  }
  body { margin: 0; padding: 0; font-family: 'Montserrat', sans-serif; background: var(--background-gradient); color: var(--font-color); }
  .menu-toggle { display: none; position: fixed; top: 15px; left: 20px; background: var(--primary-color); color: #fff; padding: 10px 15px; border-radius: 10px; font-weight: 600; cursor: pointer; z-index: 1001; box-shadow: 0 4px 8px rgba(0,0,0,0.2); }
  .main-wrapper { display: flex; min-height: 100vh; padding: 20px; gap: 20px; }
  .sidebar { flex: 1; max-width: 280px; background-color: var(--side-color); border-radius: 15px; padding: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); display: flex; flex-direction: column; gap: 15px; transition: transform 0.3s ease; }
  @media(max-width: 768px){ .sidebar { position: fixed; top: 0; left: 0; height: 100%; width: 80%; max-width: 300px; transform: translateX(-100%); z-index: 1000; } .sidebar.active { transform: translateX(0); } .main-wrapper { flex-direction: column; padding-top: 70px; } .menu-toggle { display: block; } }
  .sidebar h2 { font-size: 1.5em; margin-bottom: 10px; color: #222; }
  .advice { background: #fff; padding: 12px; border-radius: 12px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); font-size: 0.9em; line-height: 1.4; border-left: 4px solid var(--primary-color); }
  .content { flex: 3; min-width: 300px; }
  .container { max-width: 100%; display: flex; flex-direction: column; background: var(--card-background); border-radius: 20px; box-shadow: 0 10px 20px rgba(0,0,0,0.15); padding: 20px; }
  h1 { text-align: center; margin-bottom: 10px; font-weight: 600; font-size: 2em; color: #222; }
  .balance { text-align: center; font-size: 1.5em; margin-bottom: 20px; color: #2e7d32; font-weight: 600; letter-spacing: 1px; }
  .form-group { display: flex; flex-direction: column; gap: 8px; }
  label { font-weight: 600; font-size: 0.95em; }
  input[type="number"], input[type="text"], select { padding: 10px 12px; border-radius: 8px; border: 1px solid var(--border-color); font-size: 0.95em; }
  input[type="number"]:focus, input[type="text"]:focus, select:focus { outline: none; border-color: var(--primary-color); box-shadow: 0 0 6px rgba(74, 144, 226, 0.2); }
  button { padding: 12px; background-color: var(--primary-color); color: #fff; border: none; border-radius: 8px; font-size: 1em; cursor: pointer; font-weight: 600; transition: background-color 0.3s, transform 0.2s; width: 100%; margin-top: 15px; }
  button:hover { background-color: var(--button-hover); transform: translateY(-1px); }
  table { width: 100%; border-collapse: collapse; margin-top: 30px; }
  thead { background: #f5f5f5; }
  th, td { padding: 12px; text-align: center; border-bottom: 1px solid #eee; font-size: 0.9em; }
  th { font-weight: 600; }
  tbody tr:hover { background-color: #f0f8ff; transition: background-color 0.2s; }
  .delete-btn { background-color: #e53935; padding: 8px 12px; border-radius: 8px; color: white; font-weight: 600; border: none; cursor: pointer; transition: background-color 0.3s; }
  .delete-btn:hover { background-color: #d32f2f; }
  @media(max-width: 900px){ .main-wrapper { flex-direction: column; padding: 10px; } }
</style>
</head>
<body>
<button class="menu-toggle" id="menuToggle">Меню</button>
<div class="main-wrapper">
  <aside class="sidebar" id="sidebar">
    <h2>Советы экономии 💡</h2>
    <div class="advice"><strong>Не тратьте всё сразу!</strong> Попробуйте придерживаться бюджета и откладывать небольшую сумму.</div>
    <div class="advice"><strong>Планируйте покупки заранее.</strong> Составляйте список и избегайте импульсивных трат.</div>
    <div class="advice"><strong>Обучайтесь финансам.</strong> Читайте статьи, смотрите видео и совершенствуйтесь!</div>
    <div class="advice"><strong>Контролируйте расходы.</strong> Ведите учет и следите за категориями.</div>
    <div class="advice"><strong>Экономьте на мелочах.</strong> Используйте скидки, купоны и акции.</div>
  </aside>
  <div class="content">
    <div class="container">
      <h1>Финансовый Помощник</h1>
      <div class="balance" id="balance">Баланс: 0 ₽</div>
      <form id="recordForm">
        <div class="form-group">
          <label for="type">Тип операции</label>
          <select id="type" required>
            <option value="">Выберите</option>
            <option value="Доход">Доход</option>
            <option value="Расход">Расход</option>
          </select>
        </div>
        <div class="form-group">
          <label for="category">Категория</label>
          <input type="text" id="category" placeholder="Введите категорию..." required />
        </div>
        <div class="form-group">
          <label for="amount">Сумма (₽)</label>
          <input type="number" id="amount" placeholder="0" min="0" required />
        </div>
        <div style="text-align:center; margin-top:15px;">
          <button type="submit">Добавить запись</button>
        </div>
      </form>
      <div class="records">
        <h2 style="text-align:center; margin-top:40px;">История</h2>
        <table id="recordsTable" aria-label="История операций">
          <thead>
            <tr>
              <th>Тип</th>
              <th>Категория</th>
              <th>Сумма (₽)</th>
              <th>Дата</th>
              <th>Действие</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
      </div>
    </div>
  </div>
</div>
<script>
const menuBtn = document.getElementById('menuToggle');
const sidebar = document.getElementById('sidebar');
menuBtn.onclick = () => { sidebar.classList.toggle('active'); }

let records = JSON.parse(localStorage.getItem('records')) || [];
function updateBalance() {
  const total = records.reduce((acc, rec) => {
    return rec.type === 'Доход' ? acc + rec.amount : acc - rec.amount;
  }, 0);
  document.getElementById('balance').textContent = `Баланс: ${total} ₽`;
}
function renderRecords() {
  const tbody = document.querySelector('#recordsTable tbody');
  tbody.innerHTML = '';
  records.forEach((rec, index) => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${rec.type}</td>
      <td>${rec.category}</td>
      <td>${rec.amount}</td>
      <td>${rec.date}</td>
      <td><button class="delete-btn" data-index="${index}">Удалить</button></td>
    `;
    tbody.appendChild(tr);
  });
  document.querySelectorAll('.delete-btn').forEach(btn => {
    btn.onclick = () => {
      const idx = btn.dataset.index;
      records.splice(idx,1);
      localStorage.setItem('records', JSON.stringify(records));
      renderRecords();
      updateBalance();
    }
  });
}
document.getElementById('recordForm').onsubmit = e => {
  e.preventDefault();
  const type = document.getElementById('type').value;
  const category = document.getElementById('category').value;
  const amount = parseFloat(document.getElementById('amount').value);
  if(!type || !category || isNaN(amount)) return;
  const date = new Date().toLocaleString();
  records.push({type, category, amount, date});
  localStorage.setItem('records', JSON.stringify(records));
  renderRecords();
  updateBalance();
  e.target.reset();
}
updateBalance();
renderRecords();
</script>
</body>
</html>
