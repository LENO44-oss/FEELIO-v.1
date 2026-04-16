<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>FEELIO</title>

  <script src="https://js.stripe.com/v3/"></script>

  <style>
    body {
      font-family: Arial;
      text-align: center;
      background: #0f0f10;
      color: white;
      padding: 40px;
    }

    button {
      padding: 15px;
      margin: 10px;
      font-size: 18px;
      border-radius: 10px;
      border: none;
      cursor: pointer;
    }

    .mood {
      font-size: 40px;
      margin: 10px;
    }

    .card {
      background: #1c1c1e;
      padding: 20px;
      border-radius: 15px;
      margin-top: 20px;
    }

    .primary {
      background: #ffffff;
      color: black;
    }

    .paywall {
      margin-top: 30px;
      padding: 20px;
      background: #222;
      border-radius: 15px;
    }
  </style>
</head>

<body>

  <h1>FEELIO</h1>
  <p>Comment tu te sens ?</p>

  <div id="step1">
    <div class="mood">😢 😐 🙂 😄 🔥</div>

    <button onclick="selectMood(1)">😢</button>
    <button onclick="selectMood(2)">😐</button>
    <button onclick="selectMood(3)">🙂</button>
    <button onclick="selectMood(4)">😄</button>
    <button onclick="selectMood(5)">🔥</button>
  </div>

  <div id="step2" style="display:none;">
    <div class="card">
      <h2>Ton reset en 60 secondes</h2>
      <p id="actionText"></p>

      <button onclick="startTimer()" class="primary">
        Commencer
      </button>
    </div>
  </div>

  <div id="step3" style="display:none;">
    <h2>Respire...</h2>
    <h1 id="timer">60</h1>
  </div>

  <div id="paywall" class="paywall" style="display:none;">
    <h2>Limite gratuite atteinte</h2>
    <p>Débloque FEELIO+ pour un usage illimité et des insights personnalisés</p>

    <button class="primary" onclick="upgrade()">
      Passer à FEELIO+
    </button>
  </div>

<script>
let mood = null;
let time = 60;
let used = false;

// SIMULATION FREEMIUM (1 usage gratuit)
function canUse() {
  return !used;
}

function selectMood(m) {
  if (!canUse()) {
    document.getElementById("paywall").style.display = "block";
    return;
  }

  mood = m;
  used = true;

  document.getElementById("step1").style.display = "none";
  document.getElementById("step2").style.display = "block";

  const actions = {
    1: "Respire lentement pendant 60 secondes",
    2: "Recentre ton esprit",
    3: "Pense à 1 chose positive",
    4: "Continue ton énergie",
    5: "Transforme ton énergie en action"
  };

  document.getElementById("actionText").innerText = actions[m];
}

function startTimer() {
  document.getElementById("step2").style.display = "none";
  document.getElementById("step3").style.display = "block";

  let interval = setInterval(() => {
    time--;
    document.getElementById("timer").innerText = time;

    if (time <= 0) {
      clearInterval(interval);
      document.getElementById("step3").style.display = "none";
      document.getElementById("paywall").style.display = "block";
    }
  }, 1000);
}

// STRIPE (À CONFIGURER)
const stripe = Stripe("VOTRE_STRIPE_PUBLIC_KEY");

function upgrade() {
  alert("Connecte Stripe ici (mode test)");

  // VERSION SIMPLE REDIRECT (à remplacer)
  // window.location.href = "https://buy.stripe.com/xxxx";
}
</script>

</body>
</html>
