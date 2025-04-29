# 😊 Build a Mood Tracker App with Emoji & Charts (JavaScript + LocalStorage)

Ever wondered how your moods shift throughout the week? Maybe you feel awesome on Mondays (you unicorn 🦄), or maybe Fridays bring the blues. What if you could **track your emotions daily** using just emojis?

Let’s build a fun little app that does exactly that — a **Mood Tracker** with:

- Emoji mood logging (happy, sad, excited 😍, etc.)
- LocalStorage to keep your data safe between reloads
- Timeline and calendar views to track emotional trends

---

## 🧠 Why Build a Mood Tracker?

Because mental wellness matters. And because it’s an awesome **frontend project** that involves:

- Event handling
- LocalStorage
- Dynamic DOM manipulation
- Time-based filtering
- Optional charting/calendar libraries

---

## 🎯 Challenge Overview

| Feature | Details |
| --- | --- |
| Mood Log | User selects an emoji to represent today's mood |
| LocalStorage Integration | Store mood + date locally |
| Timeline Views | View mood history by day/week/month |
| Bonus | Add a calendar heatmap for moods |

---

## 🏗️ Project Setup

You only need HTML, CSS, and JavaScript.

```html
<!-- index.html -->
<body>
  <h1>How Are You Feeling Today? 😊</h1>

  <div id="mood-picker">
    <button data-mood="happy">😊</button>
    <button data-mood="sad">😢</button>
    <button data-mood="neutral">😐</button>
    <button data-mood="excited">🤩</button>
    <button data-mood="angry">😠</button>
  </div>

  <h2>Your Mood Timeline</h2>
  <select id="view-mode">
    <option value="day">Daily</option>
    <option value="week">Weekly</option>
    <option value="month">Monthly</option>
  </select>

  <ul id="mood-log"></ul>
</body>

```

---

## 🧪 Logging a Mood

Use JavaScript to handle emoji clicks and save the mood to LocalStorage.

```
// mood-tracker.js
const moodButtons = document.querySelectorAll('#mood-picker button');

moodButtons.forEach(button => {
  button.addEventListener('click', () => {
    const mood = button.dataset.mood;
    const date = new Date().toISOString().split('T')[0]; // YYYY-MM-DD

    let moods = JSON.parse(localStorage.getItem('moods') || '[]');
    moods.push({ date, mood });
    localStorage.setItem('moods', JSON.stringify(moods));

    renderMoods();
  });
});

```

---

## 🗂️ Display Mood History

Now, show past moods in the selected view (daily/weekly/monthly).

```
function renderMoods() {
  const view = document.getElementById('view-mode').value;
  const log = document.getElementById('mood-log');
  const moods = JSON.parse(localStorage.getItem('moods') || '[]');

  log.innerHTML = '';

  const grouped = groupMoodsBy(moods, view);

  for (const date in grouped) {
    const li = document.createElement('li');
    li.textContent = `${date}: ${grouped[date].map(m => emojiForMood(m.mood)).join(' ')}`;
    log.appendChild(li);
  }
}

function groupMoodsBy(moods, view) {
  const groups = {};
  moods.forEach(entry => {
    let key;
    const d = new Date(entry.date);

    if (view === 'day') {
      key = entry.date;
    } else if (view === 'week') {
      const week = getWeekNumber(d);
      key = `${d.getFullYear()}-W${week}`;
    } else if (view === 'month') {
      key = `${d.getFullYear()}-${(d.getMonth() + 1).toString().padStart(2, '0')}`;
    }

    if (!groups[key]) groups[key] = [];
    groups[key].push(entry);
  });
  return groups;
}

function getWeekNumber(date) {
  const firstJan = new Date(date.getFullYear(), 0, 1);
  return Math.ceil((((date - firstJan) / 86400000) + firstJan.getDay() + 1) / 7);
}

function emojiForMood(mood) {
  return {
    happy: "😊", sad: "😢", neutral: "😐", excited: "🤩", angry: "😠"
  }[mood];
}

```

---

## 🔄 Listen to View Change

Update the timeline when view mode changes:

```
document.getElementById('view-mode').addEventListener('change', renderMoods);
window.addEventListener('DOMContentLoaded', renderMoods);

```

---

## 📅 Bonus: Calendar View with Heatmap

For bonus points, use [**Cal-Heatmap**](https://cal-heatmap.com/) or a simple grid system to build a **calendar heatmap of moods**.

Example idea (pseudo-code):

```
// Build calendar and fill each day with mood emoji
for each date in month:
  drawBox(date)
  fillBoxWithEmoji(mood)

```

You could also color-code:

- 😊 Green
- 😐 Yellow
- 😢 Blue
- 😠 Red

---

## 🧠 Real Use Case

You're not just building a toy. This app can help:

- Journal your mental health trends
- Spot patterns (e.g., mood dips on Mondays)
- Track improvements over time

It’s also a great frontend portfolio project with real user value.

---

## 🧩 Diagram: Timeline View vs Calendar View

```
Timeline View (Grouped)

2025-06-10: 😊
2025-06-11: 😐

Week View:
2025-W23: 😊 😊 😢

Calendar View:
🗓️ Grid of boxes filled with emoji or color based on mood

```

---

## 🚀 What You’ve Learned

- Handling user input with events
- Saving data to `LocalStorage`
- Dynamically rendering and grouping entries
- Thinking in **time-based views** (day/week/month)
- Optional data visualization with calendars

---

## 📌 Final Thoughts

Whether you’re coding for fun or mental clarity, this Mood Tracker project packs a punch. With emoji, storage, and timeline views, you're combining **UX, JavaScript logic, and data handling**.

Want the full source code or a downloadable version with charts? Just ask—I’ve got you covered 💡