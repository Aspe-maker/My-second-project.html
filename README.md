<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">

<style>
body {
    background: #111;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

/* زر القلب */
.heart-btn {
    width: 80px;
    height: 80px;
    border: none;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.08);
    backdrop-filter: blur(10px);
    color: #aaa;
    font-size: 38px;
    cursor: pointer;
    transition: 0.3s ease;
    box-shadow: 0 8px 25px rgba(0,0,0,0.3);
}

/* عند مرور الماوس */
.heart-btn:hover {
    transform: scale(1.1);
    background: rgba(255, 50, 80, 0.12);
    color: #ff4966;
}

/* القلب بعد الضغط */
.heart-btn.liked {
    color: #ff1744;
    background: rgba(255, 23, 68, 0.12);
    box-shadow: 
        0 0 20px rgba(255, 23, 68, 0.35),
        0 8px 30px rgba(0,0,0,0.3);
    animation: heartBeat 0.5s ease;
}

/* النبضة */
@keyframes heartBeat {
    0%   { transform: scale(1); }
    30%  { transform: scale(1.35); }
    60%  { transform: scale(0.9); }
    100% { transform: scale(1); }
}
</style>
</head>

<body>

<button class="heart-btn" id="heartBtn" onclick="like()">
    ♡
</button>

<script>
function like() {
    const button = document.getElementById("heartBtn");

    button.classList.toggle("liked");

    if (button.classList.contains("liked")) {
        button.innerHTML = "♥";
    } else {
        button.innerHTML = "♡";
    }
}
</script>

</body>
</html>
