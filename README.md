# nomad.math
<!DOCTYPE html>
<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Тілден - теңдеуге | Ұлттық құндылық – логика тірегі</title>
    <style>
        :root {
            --primary-color: #004d40; /* Терең көк-жасыл / көшпенділер түсі */
            --accent-color: #c5a059; /* Алтын түс */
            --bg-color: #fcf8f2;     /* Жылы кремді фон */
            --card-bg: #ffffff;
            --text-color: #2c3e50;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            /* Артқы фонға қазақы ою үлгісін беретін CSS өрнегі (pattern) */
            background-color: var(--bg-color);
            background-image: radial-gradient(var(--accent-color) 0.75px, transparent 0.75px), radial-gradient(var(--accent-color) 0.75px, var(--bg-color) 0.75px);
            background-size: 30px 30px;
            background-position: 0 0, 15px 15px;
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 800px;
            width: 100%;
            background: var(--card-bg);
            padding: 35px;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 77, 64, 0.15);
            border: 2px solid var(--accent-color);
            position: relative;
            overflow: hidden;
        }

        /* Үстіңгі бөлікке ұлттық өрнек сызығын беру */
        .container::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 6px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color), var(--primary-color));
        }

        h1 {
            color: var(--primary-color);
            text-align: center;
            font-size: 26px;
            margin-bottom: 5px;
            font-weight: 800;
        }

        .subtitle {
            text-align: center;
            color: #8c6d33;
            font-style: italic;
            margin-bottom: 25px;
            font-weight: 600;
            letter-spacing: 0.5px;
        }

        .task-box {
            background: #f4f8f7;
            border-left: 6px solid var(--primary-color);
            border-top: 1px solid #e0edea;
            border-right: 1px solid #e0edea;
            border-bottom: 1px solid #e0edea;
            padding: 18px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-size: 16px;
            line-height: 1.6;
        }

        .instructions {
            font-weight: bold;
            color: #334155;
            margin-bottom: 10px;
        }

        /* Драг-энд-дроп аймақтары */
        .drop-zone-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            align-items: center;
            background: #fafafa;
            border: 2px dashed #cbd5e1;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            min-height: 60px;
            justify-content: center;
        }

        .drop-slot {
            width: 95px;
            height: 50px;
            border: 2px dashed var(--primary-color);
            border-radius: 8px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            background: #ffffff;
            font-weight: bold;
            color: #64748b;
            font-size: 18px;
            transition: all 0.3s;
        }

        .drop-slot.drag-over {
            background: #e2e8f0;
            border-color: var(--accent-color);
            transform: scale(1.05);
        }

        .drop-slot.filled {
            background: #e6f4f1;
            color: var(--primary-color);
            border-style: solid;
            border-color: var(--primary-color);
        }

        /* Сүйрелетін элементтер палитрасы */
        .palette {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            background: #fdfbf7;
            border: 1px solid #faedcd;
            padding: 18px;
            border-radius: 10px;
            margin-bottom: 20px;
            justify-content: center;
        }

        .draggable-item {
            background: var(--primary-color);
            color: white;
            padding: 12px 18px;
            border-radius: 8px;
            cursor: grab;
            font-weight: bold;
            font-size: 16px;
            user-select: none;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            transition: transform 0.2s, background-color 0.2s;
        }

        .draggable-item:hover {
            background-color: #00332c;
        }

        .draggable-item:active {
            cursor: grabbing;
            transform: scale(0.95);
        }

        /* Батырмалар мен нәтиже */
        .btn-group {
            display: flex;
            gap: 12px;
            justify-content: center;
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 16px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.3s, transform 0.2s;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        button:hover {
            background-color: #00332c;
            transform: translateY(-2px);
        }

        .btn-reset {
            background-color: #78716c;
        }
        .btn-reset:hover {
            background-color: #57534e;
        }

        .result-message {
            margin-top: 20px;
            font-weight: bold;
            font-size: 16px;
            padding: 15px;
            border-radius: 8px;
            display: none;
            text-align: center;
        }
        .result-success {
            background: #e6f4ea;
            color: #137333;
            border: 1px solid #ceead6;
        }
        .result-error {
            background: #fce8e6;
            color: #c5221f;
            border: 1px solid #fad2cf;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>«Тілден – теңдеуге» платформасы</h1>
    <div class="subtitle">✦ Ұлттық құндылық – логика тірегі ✦</div>

    <!-- Мәтіндік есеп -->
    <div class="task-box">
        <strong>Мәтіндік есеп:</strong><br>
        Қазақтың ұлттық киіз үйін тігу кезінде шебер ұзындығы <b>x</b> метр арқан дайындады. Егер арқанның ұзындығы керегенің жалпы ұзындығынан <b>15%-ке артық</b> болып, ал олардың қосындысы <b>46 метрден артық емес</b> болса, математикалық теңсіздікті құрыңыз.
    </div>

    <div class="instructions">Төмендегі блоктарды ретімен жоғарыдағы бос орындарға сүйреп апарып қойыңыз:</div>

    <!-- Сүйрелетін элементтер палитрасы -->
    <div class="palette" id="palette">
        <div class="draggable-item" draggable="true" id="item1">x</div>
        <div class="draggable-item" draggable="true" id="item2">+</div>
        <div class="draggable-item" draggable="true" id="item3">0.15x</div>
        <div class="draggable-item" draggable="true" id="item4">&le;</div>
        <div class="draggable-item" draggable="true" id="item5">46</div>
    </div>

    <div class="instructions">Теңдеуді құру аймағы:</div>
    
    <!-- Бос орындар (Drop zones) -->
    <div class="drop-zone-container">
        <div class="drop-slot" data-answer="x"></div>
        <div class="drop-slot" data-answer="+"></div>
        <div class="drop-slot" data-answer="0.15x"></div>
        <div class="drop-slot" data-answer="&le;"></div>
        <div class="drop-slot" data-answer="46"></div>
    </div>

    <div class="btn-group">
        <button onclick="checkAnswer()">Тексеру</button>
        <button class="btn-reset" onclick="resetTask()">Қайта бастау</button>
    </div>

    <div id="result" class="result-message"></div>
</div>

<script>
    const draggables = document.querySelectorAll('.draggable-item');
    const slots = document.querySelectorAll('.drop-slot');
    let draggedElement = null;

    // Сүйреу процесін бастау
    draggables.forEach(item => {
        item.addEventListener('dragstart', (e) => {
            draggedElement = item;
            e.dataTransfer.setData('text/html', item.innerHTML);
        });
    });

    slots.forEach(slot => {
        slot.addEventListener('dragover', (e) => {
            e.preventDefault();
            slot.classList.add('drag-over');
        });

        slot.addEventListener('dragleave', () => {
            slot.classList.remove('drag-over');
        });

        slot.addEventListener('drop', (e) => {
            e.preventDefault();
            slot.classList.remove('drag-over');
            
            // Егер ұяшық бос болса, элементті орналастыру
            if (!slot.classList.contains('filled')) {
                slot.innerHTML = draggedElement.innerHTML;
                slot.classList.add('filled');
                draggedElement.style.display = 'none'; // Палитрадан жасыру
            }
        });
    });

    // Жауапты тексеру функциясы
    function checkAnswer() {
        let userAnswers = [];
        slots.forEach(slot => {
            userAnswers.push(slot.innerHTML.trim());
        });

        // Дұрыс жауап тізбегі: x, +, 0.15x, ≤ (немесе &le;), 46
        const correctAnswers = ['x', '+', '0.15x', '≤', '46'];
        
        let isCorrect = true;
        for (let i = 0; i < correctAnswers.length; i++) {
            let val = userAnswers[i];
            if (val === '&le;') val = '≤';
            
            if (val !== correctAnswers[i]) {
                isCorrect = false;
                break;
            }
        }

        const resultDiv = document.getElementById('result');
        resultDiv.style.display = 'block';

        if (isCorrect && userAnswers.filter(Boolean).length === 5) {
            resultDiv.className = 'result-message result-success';
            resultDiv.innerHTML = '🎉 Керемет! Теңсіздік дұрыс құрылды: <b>x + 0.15x ≤ 46</b> (немесе 1.15x ≤ 46). Ұлттық логикалық есеп сәтті орындалды!';
        } else {
            resultDiv.className = 'result-message result-error';
            resultDiv.innerHTML = '❌ Қате бар немесе барлық бос орындар толтырылмады. «Қайта бастау» батырмасын басып, қайта көріңіз.';
        }
    }

    // Қайта бастау функциясы
    function resetTask() {
        slots.forEach(slot => {
            slot.innerHTML = '';
            slot.classList.remove('filled');
        });
        draggables.forEach(item => {
            item.style.display = 'block';
        });
        document.getElementById('result').style.display = 'none';
    }
</script>

</body>
</html>
