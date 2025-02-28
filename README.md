<!DOCTYPE html>
<html>
<head>
    <title>3D 动漫 动态效果</title>
</head>
<body>
    <script>
        function createAnimeGIF() {
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            
            // 设置画布尺寸
            canvas.width = 800;
            canvas.height = 400;

            // 设置颜色
            const colors = ['#FF6B6B', '#4ECDC4', '#45B7D1'];
            
            // 创建3D效果的渐变背景
            function drawBackground() {
                ctx.fillStyle = 'rgba(0, 0, 0, 0.8)';
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                // 添加3D网格效果
                const gradient = ctx.createLinearGradient(
                    0, 0,
                    canvas.width, canvas.height
                );
                
                gradient.addColorStop(0, 'rgba(255, 255, 255, 0.1)');
                gradient.addColorStop(0.5, '#4B638E');
                gradient.addColorStop(1, 'rgba(255, 255, 255, 0.1)');

                ctx.fillStyle = gradient;
                ctx.fillRect(0, 0, canvas.width, canvas.height);
            }

            // 绘制动态圆球
            function drawBall(x, y, radius) {
                ctx.beginPath();
                ctx.arc(x, y, radius, 0, Math.PI * 2);
                ctx.fillStyle = colors[Math.floor(Math.random() * colors.length)];
                ctx.fill();
                ctx.closePath();
            }

            // 动态效果函数
            function animate() {
                const time = Date.now() / 1000;
                
                // 绘制背景
                drawBackground();

                // 绘制动态圆球
                for (let i = 0; i < 5; i++) {
                    const x = Math.random() * canvas.width;
                    const y = Math.random() * canvas.height;
                    const radius = Math.random() * 100 + 50;
                    drawBall(x, y, radius);
                }

                // 更新画布
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                
                // 动态效果
                ctx.fillStyle = 'rgba(255, 255, 255, 0.1)';
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                // 绘制圆球的路径
                const gradient = ctx.createRadialGradient(
                    x,
                    y,
                    radius,
                    x + radius * Math.cos(time),
                    y + radius * Math.sin(time),
                    radius * 2,
                    radius,
                    radius * 2
                );

                gradient.addColorStop(0, 'rgba(255, 255, 255, 0.1)');
                gradient.addColorStop(1, colors[Math.floor(Math.random() * colors.length)]);

                ctx.fillStyle = gradient;
                ctx.beginPath();
                ctx.arc(x, y, radius, 0, Math.PI * 2);
                ctx.fill();

                // 显示时间
                ctx.font = '20px Arial';
                ctx.fillStyle = 'white';
                ctx.fillText('Time: ' + time, 10, 60);

                // 请求动画
                requestAnimationFrame(animate);
            }

            // 调用动画函数
            animate();

            // 设置窗口大小
            window.innerWidth = canvas.width;
            window.innerHeight = canvas.height;
        }

        // 打开测试
        function test() {
            createAnimeGIF();
            document.body.style.width = '100vw';
            document.body.style.height = '100vh';
        }

        // 在控制台打开
        window.onload = test;
    </script>
</body>
</html>

