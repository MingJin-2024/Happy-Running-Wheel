# Happy-Running-Wheel
<!DOCTYPE html>
<html>
<head>
    <title>幸运转盘</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #f5f5f5;
            font-family: Arial;
        }
        #wheel {
            width: 300px;
            height: 300px;
            border-radius: 50%;
            position: relative;
            transition: transform 3s ease-out;
            cursor: pointer;
        }
        .section {
            position: absolute;
            width: 50%;
            height: 50%;
            transform-origin: bottom right;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 14px;
            color: white;
        }
        #arrow {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-bottom: 20px solid red;
            z-index: 10;
        }
    </style>
</head>
<body>
    <div style="text-align: center;">
        <h2>点击开始抽取快乐跑距离！</h2>
        <div style="position: relative;">
            <div id="arrow"></div>
            <div id="wheel"></div>
        </div>
    </div>

    <script>
        const prizes = ['double 5.20km', '5.55km', '6.66km', '7.77km', '8.88km'];
        const colors = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A', '#98D8C8', '#F7DC6F'];
        const wheel = document.getElementById('wheel');
        
        // 创建转盘扇形
        prizes.forEach((prize, index) => {
            const section = document.createElement('div');
            section.className = 'section';
            section.style.background = colors[index];
            section.style.transform = `rotate(${index * 60}deg)`;
            section.textContent = prize;
            wheel.appendChild(section);
        });

        let isSpinning = false;
        wheel.addEventListener('click', () => {
            if (isSpinning) return;
            isSpinning = true;
            
            const randomDegree = 1800 + Math.floor(Math.random() * 360);
            wheel.style.transform = `rotate(${randomDegree}deg)`;
            
            setTimeout(() => {
                isSpinning = false;
                const actualDegree = randomDegree % 360;
                const prizeIndex = Math.floor((360 - actualDegree) / 60);
                alert(`恭喜获得：${prizes[prizeIndex]}`);
            }, 3000);
        });
    </script>
</body>
</html>
