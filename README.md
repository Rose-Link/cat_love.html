# cat_love.html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            background: #ffe6f2;
            overflow: hidden;
            position: relative;
            font-family: 'Comic Sans MS', cursive;
            transition: 2s;
        }

        #cat-emoji {
            font-size: 8rem;
            margin: 2rem 0;
            transition: 0.5s;
            animation: bounce 2s infinite;
            text-shadow: 0 0 20px rgba(255,105,180,0.5);
        }

        .buttons {
            display: flex;
            gap: 20px;
            transition: 0.3s;
        }

        button {
            padding: 15px 40px;
            border: none;
            border-radius: 30px;
            font-size: 20px;
            cursor: pointer;
            transition: 0.5s;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        #like-btn {
            background: linear-gradient(45deg, #ff69b4, #ff1493);
            color: white;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }

        #dislike-btn {
            background: linear-gradient(45deg, #666, #444);
            color: white;
        }

        .apocalypse {
            animation: quake 0.3s infinite, redAlert 1s infinite;
            background: #2c0d2c !important;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        @keyframes quake {
            0% { transform: translateX(0); }
            25% { transform: translateX(10px); }
            50% { transform: translateX(-10px); }
            75% { transform: translateX(5px); }
            100% { transform: translateX(0); }
        }

        @keyframes redAlert {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }
    </style>
</head>
<body>
    <div id="cat-emoji">(=^･ω･^=)♡</div>
    <div class="buttons">
        <button id="like-btn">超喜欢！</button>
        <button id="dislike-btn">才没有</button>
    </div>

    <script>
        let dislikeCount = 0;
        const catEmoji = document.getElementById('cat-emoji');
        const likeBtn = document.getElementById('like-btn');
        const dislikeBtn = document.getElementById('dislike-btn');

        // 强化版点击特效
        document.addEventListener('click', (e) => {
            // 创建破碎爱心
            const brokenHeart = document.createElement('div');
            brokenHeart.style = `
                position: absolute;
                font-size: 2rem;
                animation: fall 2s linear;
                left: ${e.clientX}px;
                top: ${e.clientY}px;
            `;
            brokenHeart.innerHTML = Math.random() > 0.5 ? '💔' : '💔';
            document.body.appendChild(brokenHeart);
            setTimeout(() => brokenHeart.remove(), 2000);
        });

        // 喜欢按钮
        likeBtn.addEventListener('click', () => {
            catEmoji.innerHTML = "(=^◕ᴥ◕^=)ฅ❤️(=◕ᴥ◕^=)";
            catEmoji.style.transform = 'scale(2)';
            likeBtn.textContent = '要永远喜欢哦！';
            document.body.classList.remove('apocalypse');
            document.body.style.background = '#ffb3d9';
        });

        // 不喜欢按钮
        dislikeBtn.addEventListener('click', () => {
            dislikeCount++;
            
            if(dislikeCount <= 4) {
                catEmoji.innerHTML = ["ฅ(•́‸•̀ฅ)","(；ω；)","(つ﹏⊂)","(╥﹏╥)"][dislikeCount-1];
                likeBtn.style.transform = `scale(${1 + dislikeCount*0.2})`;
                dislikeBtn.style.transform = `scale(${1 - dislikeCount*0.1})`;
                document.body.style.background = `hsl(240, ${dislikeCount*20}%, 90%)`;
            }
            else if(dislikeCount === 5) {
                catEmoji.innerHTML = "(ﾟДﾟ≡ﾟДﾟ)";
                catEmoji.style.fontSize = '15rem';
                likeBtn.style.fontSize = '40px';
                likeBtn.style.transform = 'scale(3)';
                dislikeBtn.style.transform = 'scale(0.3)';
                document.body.style.background = '#b3b3ff';
            }
            else if(dislikeCount >= 6) {
                // 进入末日模式
                dislikeBtn.remove();
                catEmoji.innerHTML = "˚‧º·(˃̣̣̥᷄⌓˂̣̣̥᷅)‧º·˚";
                catEmoji.style.fontSize = '25rem';
                catEmoji.style.animation = 'none';
                document.body.classList.add('apocalypse');
                likeBtn.style.transform = 'scale(5)';
                likeBtn.style.position = 'fixed';
                likeBtn.style.bottom = '20%';
                
                // 添加末日特效
                setInterval(() => {
                    const meteor = document.createElement('div');
                    meteor.innerHTML = '☄️';
                    meteor.style = `
                        position: fixed;
                        font-size: 3rem;
                        left: ${Math.random()*100}vw;
                        animation: meteorFall 2s linear;
                    `;
                    document.body.appendChild(meteor);
                    setTimeout(() => meteor.remove(), 2000);
                }, 500);
            }
        });

        // 动态添加CSS
        const style = document.createElement('style');
        style.textContent = `
            @keyframes meteorFall {
                from { transform: translateY(-100vh) rotate(45deg); }
                to { transform: translateY(100vh) rotate(135deg); }
            }
            @keyframes fall {
                to { transform: translateY(100vh) rotate(360deg); }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
