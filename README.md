<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اشتراک گذاری متن</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #6c5ce7;
            --secondary-color: #a29bfe;
            --accent-color: #fd79a8;
            --text-color: #2d3436;
            --bg-color: #f9f9f9;
            --card-bg: #ffffff;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
        }

        .container {
            width: 100%;
            max-width: 600px;
            margin: auto;
            animation: fadeIn 0.8s ease-out;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
        }

        h1 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 30px;
            font-size: 2rem;
            position: relative;
        }

        h1::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 3px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
            border-radius: 3px;
        }

        .form-group {
            margin-bottom: 25px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--primary-color);
        }

        textarea {
            width: 100%;
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 10px;
            resize: vertical;
            min-height: 150px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }

        textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.2);
        }

        .btn {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 50px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(108, 92, 231, 0.3);
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(108, 92, 231, 0.4);
        }

        .btn:active {
            transform: translateY(1px);
        }

        .btn::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 5px;
            height: 5px;
            background: rgba(255, 255, 255, 0.5);
            opacity: 0;
            border-radius: 100%;
            transform: scale(1, 1) translate(-50%);
            transform-origin: 50% 50%;
        }

        .btn:focus:not(:active)::after {
            animation: ripple 1s ease-out;
        }

        .result {
            margin-top: 30px;
            text-align: center;
            animation: slideUp 0.5s ease-out;
        }

        .result-link {
            display: block;
            margin-top: 15px;
            padding: 15px;
            background-color: rgba(108, 92, 231, 0.1);
            border-radius: 10px;
            word-break: break-all;
            color: var(--primary-color);
            font-weight: 600;
            text-decoration: none;
            transition: all 0.3s ease;
        }

        .result-link:hover {
            background-color: rgba(108, 92, 231, 0.2);
        }

        .copy-btn {
            margin-top: 20px;
            background: linear-gradient(45deg, var(--accent-color), #ff7675);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(253, 121, 168, 0.3);
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .copy-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(253, 121, 168, 0.4);
        }

        .copy-btn.copied {
            background: linear-gradient(45deg, #00b894, #55efc4);
            box-shadow: 0 4px 15px rgba(0, 184, 148, 0.3);
        }

        .copy-page {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 80vh;
            text-align: center;
        }

        .copy-btn-large {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--primary-color), var(--accent-color));
            color: white;
            border: none;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            gap: 10px;
            box-shadow: 0 10px 30px rgba(108, 92, 231, 0.3);
            transition: all 0.3s ease;
            margin-top: 30px;
            position: relative;
            overflow: hidden;
        }

        .copy-btn-large:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(108, 92, 231, 0.4);
        }

        .copy-btn-large:active {
            transform: scale(0.98);
        }

        .copy-btn-large i {
            font-size: 40px;
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: var(--accent-color);
            opacity: 0;
            top: 0;
            left: 0;
            z-index: 1000;
            pointer-events: none;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes ripple {
            0% {
                transform: scale(0, 0);
                opacity: 1;
            }
            20% {
                transform: scale(25, 25);
                opacity: 1;
            }
            100% {
                opacity: 0;
                transform: scale(40, 40);
            }
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        /* Responsive adjustments */
        @media (max-width: 768px) {
            .card {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.5rem;
            }
            
            .copy-btn-large {
                width: 120px;
                height: 120px;
                font-size: 16px;
            }
            
            .copy-btn-large i {
                font-size: 30px;
            }
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- صفحه اصلی برای وارد کردن متن -->
        <div id="input-page" class="container">
            <div class="card">
                <h1>اشتراک گذاری متن</h1>
                <div class="form-group">
                    <label for="text-input">متن خود را وارد کنید:</label>
                    <textarea id="text-input" placeholder="متن مورد نظر برای اشتراک گذاری را اینجا بنویسید..."></textarea>
                </div>
                <button id="submit-btn" class="btn">
                    <i class="fas fa-share-alt" style="margin-left: 8px;"></i>
                    ایجاد لینک اشتراک
                </button>
                
                <div id="result" class="result" style="display: none;">
                    <p>لینک اشتراک گذاری شما:</p>
                    <a id="share-link" href="#" class="result-link"></a>
                    <button id="copy-link-btn" class="copy-btn">
                        <i class="far fa-copy"></i>
                        کپی لینک
                    </button>
                </div>
            </div>
        </div>
        
        <!-- صفحه نمایش متن با دکمه کپی -->
        <div id="copy-page" class="container copy-page" style="display: none;">
            <div class="card">
                <h1>متن برای کپی</h1>
                <p id="text-to-copy" style="margin: 20px 0; font-size: 18px; line-height: 1.6;"></p>
                <button id="copy-text-btn" class="copy-btn-large">
                    <i class="far fa-copy"></i>
                    کپی متن
                </button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // بررسی URL برای دیدن اگر در صفحه اشتراک هستیم
            const path = window.location.pathname;
            if (path.includes('/newlinkadd')) {
                showInputPage();
            } else if (path.includes('/share/')) {
                const textId = path.split('/share/')[1];
                showCopyPage(textId);
            }
            
            // رویدادهای کلیک دکمه‌ها
            document.getElementById('submit-btn').addEventListener('click', generateLink);
            document.getElementById('copy-link-btn')?.addEventListener('click', copyLink);
            document.getElementById('copy-text-btn')?.addEventListener('click', copyText);
        });
        
        function showInputPage() {
            document.getElementById('input-page').style.display = 'block';
            document.getElementById('copy-page').style.display = 'none';
        }
        
        function showCopyPage(textId) {
            document.getElementById('input-page').style.display = 'none';
            document.getElementById('copy-page').style.display = 'block';
            
            // بازیابی متن از localStorage
            const text = localStorage.getItem(`shared-text-${textId}`);
            if (text) {
                document.getElementById('text-to-copy').textContent = text;
            } else {
                document.getElementById('text-to-copy').textContent = 'متنی یافت نشد!';
                document.getElementById('copy-text-btn').disabled = true;
            }
        }
        
        function generateLink() {
            const textInput = document.getElementById('text-input').value.trim();
            
            if (!textInput) {
                alert('لطفاً متنی برای اشتراک گذاری وارد کنید');
                return;
            }
            
            // ایجاد یک ID منحصر به فرد
            const textId = generateId();
            
            // ذخیره متن در localStorage
            localStorage.setItem(`shared-text-${textId}`, textInput);
            
            // ایجاد لینک اشتراک
            const shareLink = `${window.location.origin}/share/${textId}`;
            document.getElementById('share-link').textContent = shareLink;
            document.getElementById('share-link').href = shareLink;
            document.getElementById('result').style.display = 'block';
            
            // اسکرول به قسمت نتیجه
            document.getElementById('result').scrollIntoView({ behavior: 'smooth' });
        }
        
        function copyLink() {
            const shareLink = document.getElementById('share-link').href;
            navigator.clipboard.writeText(shareLink).then(() => {
                const btn = document.getElementById('copy-link-btn');
                btn.innerHTML = '<i class="fas fa-check"></i> لینک کپی شد!';
                btn.classList.add('copied');
                
                setTimeout(() => {
                    btn.innerHTML = '<i class="far fa-copy"></i> کپی لینک';
                    btn.classList.remove('copied');
                }, 2000);
            });
        }
        
        function copyText() {
            const textToCopy = document.getElementById('text-to-copy').textContent;
            navigator.clipboard.writeText(textToCopy).then(() => {
                const btn = document.getElementById('copy-text-btn');
                btn.innerHTML = '<i class="fas fa-check"></i> متن کپی شد!';
                btn.classList.add('copied');
                
                // ایجاد کنفتی
                createConfetti();
                
                setTimeout(() => {
                    btn.innerHTML = '<i class="far fa-copy"></i> کپی متن';
                    btn.classList.remove('copied');
                }, 2000);
            });
        }
        
        function generateId() {
            return Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15);
        }
        
        function createConfetti() {
            const colors = ['#6c5ce7', '#a29bfe', '#fd79a8', '#ff7675', '#00b894', '#55efc4'];
            
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.top = -10 + 'px';
                confetti.style.width = Math.random() * 10 + 5 + 'px';
                confetti.style.height = Math.random() * 10 + 5 + 'px';
                confetti.style.transform = 'rotate(' + Math.random() * 360 + 'deg)';
                
                document.body.appendChild(confetti);
                
                const animationDuration = Math.random() * 3 + 2;
                
                confetti.style.animation = `fall ${animationDuration}s linear forwards`;
                
                // حذف المان پس از اتمام انیمیشن
                setTimeout(() => {
                    confetti.remove();
                }, animationDuration * 1000);
            }
            
            // اضافه کردن استایل انیمیشن fall
            const style = document.createElement('style');
            style.innerHTML = `
                @keyframes fall {
                    to {
                        opacity: 1;
                        top: 100vh;
                        transform: rotate(360deg) translateX(${Math.random() > 0.5 ? '-' : ''}${Math.random() * 100}px);
                    }
                }
            `;
            document.head.appendChild(style);
        }
    </script>
</body>
</html>
