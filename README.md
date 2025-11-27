# Domino
Untuk menghitung poin batu DOMINO
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<title>Domino 101</title>

<!-- MATERIAL DESIGN COLORS -->
<style>
    :root {
        --primary: #1976D2;
        --primary-dark: #0D47A1;
        --accent: #FFCA28;
        --surface: #FFFFFF;
        --bg: #F1F1F1;
        --text: #333;
    }

    body {
        margin: 0;
        font-family: "Roboto", Arial, sans-serif;
        background: var(--bg);
    }

    /* TOP APP BAR */
    .appbar {
        background: var(--primary);
        color: white;
        padding: 18px;
        font-size: 22px;
        font-weight: bold;
        text-align: center;
        box-shadow: 0 3px 8px rgba(0,0,0,0.3);
    }

    .container {
        max-width: 480px;
        margin: auto;
        padding: 15px;
    }

    /* CARD STYLE */
    .card {
        background: var(--surface);
        padding: 18px;
        border-radius: 12px;
        margin-top: 15px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }

    label {
        font-weight: bold;
        display: block;
        margin-top: 12px;
        color: var(--text);
    }

    input {
        width: 100%;
        padding: 14px;
        border-radius: 8px;
        font-size: 16px;
        border: 1px solid #aaa;
        margin-top: 5px;
    }

    .btn {
        width: 100%;
        padding: 15px;
        margin-top: 15px;
        background: var(--primary);
        border-radius: 10px;
        border: none;
        color: white;
        font-size: 17px;
        font-weight: bold;
        cursor: pointer;
        position: relative;
        overflow: hidden;
    }

    /* Ripple effect */
    .btn:active::after {
        content: "";
        position: absolute;
        width: 200%;
        height: 200%;
        background: rgba(255,255,255,0.4);
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%) scale(0);
        border-radius: 50%;
        animation: ripple 0.4s forwards;
    }

    @keyframes ripple {
        to { transform: translate(-50%, -50%) scale(1); opacity: 0; }
    }

    .btn-red {
        background: #D32F2F;
    }

    .result {
        background: var(--accent);
        padding: 12px;
        border-radius: 10px;
        margin-top: 10px;
        font-size: 18px;
        font-weight: bold;
        text-align: center;
    }

    /* Floating button */
    .fab {
        position: fixed;
        bottom: 20px;
        right: 20px;
        background: var(--primary);
        width: 60px;
        height: 60px;
        border-radius: 50%;
        color: white;
        font-size: 28px;
        border: none;
        box-shadow: 0 4px 10px rgba(0,0,0,0.25);
        cursor: pointer;
    }
</style>
</head>
<body>

<div class="appbar">Domino 101</div>

<div class="container">

    <!-- INPUT CARD -->
    <div class="card">
        <h3 style="margin-top:0;">Input Nilai Pemain</h3>

        <label>Pemain 1 (Tim A)</label>
        <input type="number" id="p1">

        <label>Pemain 2 (Tim A)</label>
        <input type="number" id="p2">

        <label>Pemain 3 (Tim B)</label>
        <input type="number" id="p3">

        <label>Pemain 4 (Tim B)</label>
        <input type="number" id="p4">

        <button class="btn" onclick="hitung()">Hitung Nilai</button>
        <button class="btn btn-red" onclick="resetGame()">Reset Total</button>
    </div>

    <!-- RESULT CARD -->
    <div class="card">
        <h3>Hasil Ronde</h3>
        <div class="result" id="hasil">-</div>

        <h3>Total Skor Tim</h3>
        <div class="result" id="totalA">Tim A: 0</div>
        <div class="result" id="totalB">Tim B: 0</div>

        <h3>Pemenang</h3>
        <div class="result" id="winner">-</div>
    </div>
</div>

<button class="fab" onclick="resetGame()">⟳</button>

<script>
    let totalA = 0;
    let totalB = 0;

    function hitung() {
        let p1 = parseInt(document.getElementById("p1").value) || 0;
        let p2 = parseInt(document.getElementById("p2").value) || 0;
        let p3 = parseInt(document.getElementById("p3").value) || 0;
        let p4 = parseInt(document.getElementById("p4").value) || 0;

        let timA = p1 + p2;
        let timB = p3 + p4;

        // aturan nilai 0–10 tidak dihitung
        if (timA <= 10) timA = 0;
        if (timB <= 10) timB = 0;

        totalA += timA;
        totalB += timB;

        document.getElementById("hasil").innerHTML =
            "Tim A: " + timA + " | Tim B: " + timB;

        document.getElementById("totalA").innerHTML = "Tim A: " + totalA;
        document.getElementById("totalB").innerHTML = "Tim B: " + totalB;

        // sistem kalah 101
        if (totalA >= 101 && totalB < 101)
            document.getElementById("winner").innerHTML = "TIM B MENANG 🎉";

        else if (totalB >= 101 && totalA < 101)
            document.getElementById("winner").innerHTML = "TIM A MENANG 🎉";
    }

    function resetGame() {
        totalA = 0;
        totalB = 0;
        document.getElementById("totalA").innerHTML = "Tim A: 0";
        document.getElementById("totalB").innerHTML = "Tim B: 0";
        document.getElementById("hasil").innerHTML = "-";
        document.getElementById("winner").innerHTML = "-";
    }
</script>

</body>
</html>
