<!DOCTYPE html>
<html lang="ar">
<head>
<style>
button {
    font-size: 40px;
    background: none;
    border: none;
    cursor: pointer;
}

.heart {
    color: red;
    transform: scale(1.2);
}
</style>
</head>

<body>

<button id="heartBtn" onclick="makeHeart()">♡</button>

<script>
function makeHeart() {
    const btn = document.getElementById("heartBtn");
    btn.innerHTML = "♥";
    btn.classList.add("heart");
}
</script>

</body>
</html>
