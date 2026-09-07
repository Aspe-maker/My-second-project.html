<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    background: #08080b;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: Arial, sans-serif;
}

/* الخلفية السينمائية */
.scene {
    position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

/* زر اضغط */
.press-btn {
    position: relative;
    padding: 18px 55px;
    border: 1px solid rgba(255,255,255,.25);
    border-radius: 50px;
    background: rgba(255,255,255,.08);
    color: white;
    font-size: 22px;
    cursor: pointer;
    backdrop-filter: blur(12px);
    box-shadow: 0 10px 40px rgba(0,0,0,.5);
    transition: .5s ease;
}

.press-btn::before {
    content: "";
    position: absolute;
    inset: -2px;
    border-radius: 50px;
    background: linear-gradient(
        90deg,
        transparent,
        rgba(255,255,255,.5),
        transparent
    );
    opacity: 0;
    transition: .5s;
}

.press-btn:hover {
    transform: scale(1.08);
    box-shadow: 0 0 35px rgba(255,50,90,.25);
}

.press-btn:hover::before {
    opacity: 1;
}

/* منطقة القلب */
.heart-container {
    position: absolute;
    width: 260px;
    height: 260px;
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transform: scale(.2);
    pointer-events: none;
}

/* الهالة */
.glow {
    position: absolute;
    width: 150px;
    height: 150px;
    border-radius: 50%;
    background: rgba(255,25,75,.25);
    filter: blur(45px);
    transform: scale(.5);
}

/* القلب */
.heart {
    position: relative;
    width: 105px;
    height: 105px;
    transform: rotate(-45deg) scale(.2);
    background: #ff1744;
    filter:
        drop-shadow(0 0 12px #ff1744)
        drop-shadow(0 0 35px rgba(255,23,68,.8));
}

.heart::before,
.heart::after {
    content: "";
    position: absolute;
    width: 105px;
    height: 105px;
    border-radius: 50%;
    background: #ff1744;
}

.heart::before {
    top: -52px;
    left: 0;
}

.heart::after {
    left: 52px;
    top: 0;
}

/* الحلقة */
.ring {
    position: absolute;
    width: 80px;
    height: 80px;
    border: 2px solid rgba(255,80,110,.7);
    border-radius: 50%;
    opacity: 0;
}

/* عند التفعيل */
.active .press-btn {
    opacity: 0;
    transform: scale(.5);
    pointer-events: none;
}

.active .heart-container {
    opacity: 1;
    animation: containerIn 1s cubic-bezier(.2,1.5,.4,1) forwards;
}

.active .heart {
    animation:
        heartAppear 1.1s cubic-bezier(.17,.89,.32,1.4) forwards,
        heartbeat 1.5s 1.1s infinite;
}

.active .glow {
    animation: glowIn 1s ease forwards,
               glowPulse 1.5s 1.1s infinite;
}

.active .ring {
    animation: ringExplosion 1.2s ease-out forwards;
}

/* ظهور القلب */
@keyframes containerIn {
    0% {
        transform: scale(.2) rotate(-15deg);
    }
    60% {
        transform: scale(1.15) rotate(5deg);
    }
    100% {
        transform: scale(1) rotate(0);
    }
}

@keyframes heartAppear {
    0% {
        transform: rotate(-45deg) scale(.1);
    }
    55% {
        transform: rotate(-45deg) scale(1.25);
    }
    75% {
        transform: rotate(-45deg) scale(.85);
    }
    100% {
        transform: rotate(-45deg) scale(1);
    }
}

@keyframes heartbeat {
    0%,100% {
        transform: rotate(-45deg) scale(1);
    }
    15% {
        transform: rotate(-45deg) scale(1.12);
    }
    30% {
        transform: rotate(-45deg) scale(1);
    }
    45% {
        transform: rotate(-45deg) scale(1.08);
    }
}

@keyframes glowIn {
    from {
        transform: scale(.2);
        opacity: 0;
    }
    to {
        transform: scale(1);
        opacity: 1;
    }
}

@keyframes glowPulse {
    0%,100% {
        transform: scale(.9);
        opacity: .5;
    }
    50% {
        transform: scale(1.35);
        opacity: .9;
    }
}

@keyframes ringExplosion {
    0% {
        width: 40px;
        height: 40px;
        opacity: 1;
    }
    100% {
        width: 300px;
        height: 300px;
        opacity: 0;
    }
}

/* الجزيئات */
.particle {
    position: absolute;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #ff4065;
    opacity: 0;
}

.active .particle {
    animation: particleExplosion 1.2s ease-out forwards;
}

@keyframes particleExplosion {
    0% {
        opacity: 1;
        transform: translate(0,0) scale(1);
    }
    100% {
        opacity: 0;
        transform:
            translate(
                var(--x),
                var(--y)
            )
            scale(0);
    }
}
</style>
</head>

<body>

<div class="scene" id="scene">

    <button class="press-btn" onclick="showHeart()">
        اضغط
    </button>

    <div class="heart-container">

        <div class="glow"></div>
        <div class="ring"></div>
        <div class="heart"></div>

        <!-- جزيئات -->
        <span class="particle" style="--x:120px;--y:-80px"></span>
        <span class="particle" style="--x:-130px;--y:-70px"></span>
        <span class="particle" style="--x:150px;--y:30px"></span>
        <span class="particle" style="--x:-150px;--y:40px"></span>
        <span class="particle" style="--x:80px;--y:130px"></span>
        <span class="particle" style="--x:-90px;--y:130px"></span>
        <span class="particle" style="--x:30px;--y:-150px"></span>
        <span class="particle" style="--x:-30px;--y:150px"></span>

    </div>

</div>

<script>
function showHeart() {

    const scene = document.getElementById("scene");

    scene.classList.add("active");

}
</script>

</body>
</html>
