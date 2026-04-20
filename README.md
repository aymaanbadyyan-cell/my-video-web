<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>看一看幸运视频</title>
    <style>
        body { display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100vh; background: #1a1a1a; color: white; margin: 0; font-family: sans-serif; }
        
        /* 跑马灯动画样式 */
        #loader { width: 100px; height: 100px; border: 10px solid #333; border-top: 10px solid #ff4757; border-radius: 50%; display: none; }
        .spin { animation: spin 0.8s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* 视频层 */
        #video-container { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: black; }
        video { width: 100%; height: 100%; }

        #action-btn { padding: 15px 40px; font-size: 20px; cursor: pointer; background: #ff4757; color: white; border: none; border-radius: 30px; transition: 0.3s; }
        #action-btn:hover { transform: scale(1.1); background: #ff6b81; }
    </style>
</head>
<body>

    <div id="main-ui">
        <button id="action-btn" onclick="startLottery()">👀 看一看</button>
        <div id="loader"></div>
    </div>

    <div id="video-container">
        <video id="lucky-video" playsinline></video>
    </div>

    <script>
        // 1. 配置你的视频路径（假设存放在 videos 文件夹下）
        const videoFiles = [
            'videos/1.mp4', 'videos/2.mp4', 'videos/3.mp4', 'videos/4.mp4',
            'videos/5.mp4', 'videos/6.mp4', 'videos/7.mp4', 'videos/8.mp4',
            'videos/9.mp4', 'videos/10.mp4', 'videos/11.mp4', 'videos/12.mp4'
        ];

        const btn = document.getElementById('action-btn');
        const loader = document.getElementById('loader');
        const videoContainer = document.getElementById('video-container');
        const videoPlayer = document.getElementById('lucky-video');

        function startLottery() {
            // 隐藏按钮，显示动画
            btn.style.display = 'none';
            loader.style.display = 'block';
            loader.classList.add('spin');

            // 2. 运行3秒钟后停止
            setTimeout(() => {
                loader.classList.remove('spin');
                loader.style.display = 'none';
                playRandomVideo();
            }, 3000);
        }

        function playRandomVideo() {
            // 3. 随机选择一个视频
            const randomIndex = Math.floor(Math.random() * videoFiles.length);
            videoPlayer.src = videoFiles[randomIndex];

            // 显示播放器并播放
            videoContainer.style.display = 'block';
            videoPlayer.play();

            // 4. 播放结束后回到“看一看”界面
            videoPlayer.onended = () => {
                videoContainer.style.display = 'none';
                btn.style.display = 'block';
                videoPlayer.src = ""; // 清空资源
            };
        }
    </script>
</body>
</html>
