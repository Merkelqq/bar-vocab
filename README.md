[index.html.html](https://github.com/user-attachments/files/33439492/index.html.html)
# bar-vocab<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Словарь для бара</title>
  <style>
    body { font-family: system-ui, sans-serif; background: #121212; color: #e0e0e0; padding: 20px; }
    h1 { text-align: center; margin-bottom: 5px; color: #ffffff; }
    .subtitle { text-align: center; color: #aaaaaa; margin-bottom: 25px; }

    .controls { display: flex; gap: 10px; flex-wrap: wrap; justify-content: center; margin-bottom: 20px; }
    input { padding: 10px; border: 1px solid #444; border-radius: 6px; width: 140px; background: #1e1e1e; color: #ffffff; }
    #search { width: 240px; }
    button { padding: 10px 16px; background: #bb86fc; color: #000000; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; }
    button:hover { background: #9d5ccc; }

    table { width: 100%; border-collapse: collapse; margin-top: 10px; background: #1e1e1e; box-shadow: 0 1px 3px rgba(0,0,0,0.5); }
    th, td { border: 1px solid #333; padding: 12px; text-align: left; color: #e0e0e0; }
    th { background: #2c2c2c; color: #cccccc; }
    .tag-slang { background: #ffcc00; color: #000000; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; font-weight: bold; }
  </style>
</head>
<body>
  <h1>Словарь для бара</h1>
  <p class="subtitle">Слова, сленг, поиск, добавление — всё в одном файле</p>

  <div class="controls">
    <input id="search" type="text" placeholder="Поиск по словам…">
    <input id="word" type="text" placeholder="Слово (англ)">
    <input id="trans" type="text" placeholder="Транскрипция (рус)">
    <input id="translation" type="text" placeholder="Перевод">
    <input id="example" type="text" placeholder="Пример фразы">
    <button onclick="addWord()">Добавить</button>
  </div>

  <table>
    <thead>
      <tr>
        <th>Слово</th>
        <th>Транскрипция</th>
        <th>Перевод</th>
        <th>Пример</th>
        <th>Тип</th>
      </tr>
    </thead>
    <tbody id="tableBody"></tbody>
  </table>

  <script>
    const initialWords = [
      { word: 'vibe', trans: 'вайб', translation: 'атмосфера', example: 'I like the vibe here.', type: 'сленг' },
      { word: 'chill', trans: 'чилл', translation: 'расслабляться, спокойный', example: 'Let’s just chill.', type: 'сленг' },
      { word: 'lit', trans: 'лит', translation: 'круто, огонь', example: 'This party is lit!', type: 'сленг' },
      { word: 'dope', trans: 'доуп', translation: 'очень крутой', example: 'That track is so dope!', type: 'сленг' },
      { word: 'hang out', trans: 'хэнг аут', translation: 'тусить, проводить время', example: 'We’re hanging out at my place.', type: 'сленг' },
      { word: 'smooth', trans: 'смуз', translation: 'приятно, гладко', example: 'The drinks are smooth.', type: 'база' },
      { word: 'crowded', trans: 'краудед', translation: 'многолюдно', example: 'It’s too crowded in here.', type: 'база' },
      { word: 'sick', trans: 'сик', translation: 'потрясающий (сленг)', example: 'That DJ set was sick.', type: 'сленг' },
      { word: 'rad', trans: 'рэд', translation: 'круто (винтажный сленг)', example: 'That’s so rad.', type: 'сленг' },
      { word: 'fierce', trans: 'фирс', translation: 'дерзко, мощно, стильно', example: 'She looks fierce tonight.', type: 'сленг' },
      { word: 'groovy', trans: 'груви', translation: 'классно, в ритме, кайфово', example: 'This beat is so groovy.', type: 'сленг' },
      { word: 'legit', trans: 'лиджит', translation: 'по-настоящему, реально, честно', example: 'He’s legit the best bartender.', type: 'сленг' },
      { word: 'straight-up', trans: 'стрэйт-ап', translation: 'честно, прямо, без обмана', example: 'Straight-up, this cocktail is amazing.', type: 'сленг' },
      { word: 'off the chain', trans: 'оф зе чейн', translation: 'суперкруто, запредельно', example: 'This place is off the chain.', type: 'сленг' },
      { word: 'baller', trans: 'бэллер', translation: 'успешный, стильный, уверенный', example: 'He walks in like a total baller.', type: 'сленг' },
      { word: 'swag', trans: 'свэг', translation: 'стиль, харизма, крутая подача', example: 'He’s got serious swag.', type: 'сленг' },
      { word: 'blazing', trans: 'блэйзинг', translation: 'очень круто, ярко, мощно', example: 'The whole night was blazing.', type: 'сленг' },
      { word: 'epic', trans: 'эпик', translation: 'эпично, грандиозно', example: 'That sunset was epic.', type: 'база' },
      { word: 'insanely', trans: 'инсэйнли', translation: 'безумно, невероятно', example: 'This drink is insanely good.', type: 'база' },
      { word: 'flawless', trans: 'флолесс', translation: 'идеально, без изъянов', example: 'Her outfit is flawless.', type: 'база' },
      { word: 'stunning', trans: 'станинг', translation: 'потрясающе красивый', example: 'You look stunning tonight.', type: 'база' },
      { word: 'effortless', trans: 'эффортлес', translation: 'легко, непринуждённо, будто без усилий', example: 'She looks effortless but so cool.', type: 'база' },
      { word: 'lowkey', trans: 'лоуки', translation: 'тихо, по-скромному, не на публику', example: 'Lowkey, I love this song.', type: 'сленг' },
      { word: 'highkey', trans: 'хайки', translation: 'открыто, громко, без стеснения', example: 'Highkey, this is the best night ever.', type: 'сленг' },
      { word: 'salty', trans: 'солти', translation: 'обиженный, недовольный, «солёный»', example: 'Don’t be salty, we’ll go next time.', type: 'сленг' },
      { word: 'stoked', trans: 'стоукд', translation: 'в восторге, заряженный', example: 'I’m so stoked for this gig.', type: 'сленг' },
      { word: 'amped', trans: 'эмпт', translation: 'заряженный, на адреналине', example: 'Everyone’s amped for the show.', type: 'сленг' },
      { word: 'buzzed', trans: 'базд', translation: 'слегка навеселе, лёгкий кайф', example: 'I’m just buzzed, nothing heavy.', type: 'сленг' },
      { word: 'wasted', trans: 'вэйтед', translation: 'сильно пьян, «в хлам»', example: 'He was wasted by midnight.', type: 'сленг' },
      { word: 'toss back', trans: 'тос бэк', translation: 'опрокинуть (напиток)', example: 'Just toss back one shot and relax.', type: 'сленг' },
      { word: 'sip', trans: 'сип', translation: 'пить маленькими глотками', example: 'I’ll just sip my drink slowly.', type: 'база' },
      { word: 'kick back', trans: 'кик бэк', translation: 'отдохнуть, расслабиться', example: 'Let’s kick back and enjoy the music.', type: 'база' },
      { word: 'zone out', trans: 'зоун аут', translation: 'выпасть из реальности, отвлечься', example: 'I just zoned out for a minute.', type: 'сленг' },
      { word: 'on point', trans: 'он поинт', translation: 'идеально, точно в цель', example: 'Your style is on point tonight.', type: 'сленг' },
      { word: 'solid', trans: 'солид', translation: 'надёжный, хороший, крепкий вариант', example: 'That’s a solid plan.', type: 'база' },
      { word: 'vibes only', trans: 'вайбс онли', translation: 'только атмосфера, без лишних слов', example: 'Tonight it’s vibes only.', type: 'сленг' }
    ];

    let words = JSON.parse(localStorage.getItem('barVocab')) || initialWords;

    function renderTable(filter = '') {
      const tbody = document.getElementById('tableBody');
      tbody.innerHTML = '';

      words.forEach(w => {
        if (filter && !w.word.toLowerCase().includes(filter.toLowerCase()) &&
            !w.translation.toLowerCase().includes(filter.toLowerCase())) {
          return;
        }

        const tr = document.createElement('tr');
        const typeTag = w.type === 'сленг' ? '<span class="tag-slang">сленг</span>' : w.type;
        tr.innerHTML = `
          <td><b>${w.word}</b></td>
          <td>${w.trans}</td>
          <td>${w.translation}</td>
          <td>${w.example}</td>
          <td>${typeTag}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    function addWord() {
      const word = document.getElementById('word').value.trim();
      if (!word) return;

      const newWord = {
        word,
        trans: document.getElementById('trans').value.trim(),
        translation: document.getElementById('translation').value.trim(),
        example: document.getElementById('example').value.trim(),
        type: 'база'
      };

      if (newWord.translation.toLowerCase().includes('сленг') ||
          newWord.example.toLowerCase().includes('slang')) {
        newWord.type = 'сленг';
      }

      words.unshift(newWord);
      localStorage.setItem('barVocab', JSON.stringify(words));
      renderTable();
      clearInputs();
    }

    function clearInputs() {
      document.getElementById('word').value = '';
      document.getElementById('trans').value = '';
      document.getElementById('translation').value = '';
      document.getElementById('example').value = '';
    }

    document.getElementById('search').addEventListener('input', (e) => {
      renderTable(e.target.value);
    });

    renderTable();
  </script>
</body>
</html>
