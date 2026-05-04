<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Animated Link Hub</title>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial;
}

body {
  height: 100vh;
  background: linear-gradient(270deg, #ff6ec4, #7873f5, #4facfe, #43e97b);
  background-size: 800% 800%;
  animation: gradientMove 10s ease infinite;
  display: flex;
  align-items: center;
  justify-content: center;
}

@keyframes gradientMove {
  0% {background-position: 0% 50%;}
  50% {background-position: 100% 50%;}
  100% {background-position: 0% 50%;}
}

/* FLOATING CARD */
.container {
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(12px);
  padding: 25px;
  border-radius: 20px;
  width: 90%;
  max-width: 500px;
  text-align: center;
  color: white;
  box-shadow: 0 0 25px rgba(0,0,0,0.3);
  animation: float 4s ease-in-out infinite;
}

@keyframes float {
  0% { transform: translateY(0px);}
  50% { transform: translateY(-10px);}
  100% { transform: translateY(0px);}
}

h2 {
  margin-bottom: 15px;
}

input, textarea {
  width: 90%;
  padding: 10px;
  margin: 10px;
  border-radius: 10px;
  border: none;
  outline: none;
}

/* BUTTON STYLE */
button {
  position: relative;
  overflow: hidden;
  padding: 12px 20px;
  border: none;
  border-radius: 12px;
  margin: 8px;
  cursor: pointer;
  font-weight: bold;
  transition: 0.3s;
}

button:hover {
  transform: scale(1.1);
  box-shadow: 0 0 15px rgba(255,255,255,0.8);
}

/* RIPPLE EFFECT */
button::after {
  content: "";
  position: absolute;
  width: 5px;
  height: 5px;
  background: white;
  opacity: 0;
  border-radius: 100%;
  transform: scale(1);
  pointer-events: none;
}

button:active::after {
  animation: ripple 0.6s linear;
}

@keyframes ripple {
  0% {
    opacity: 0.8;
    transform: scale(1);
  }
  100% {
    opacity: 0;
    transform: scale(20);
  }
}

/* BUTTON COLORS */
.create-btn { background: #ffcc00; color: black; }
.visit { background: #00c6ff; }
.youtube { background: #ff0000; }
.discord { background: #5865F2; }

/* PREVIEW ANIMATION */
.preview {
  margin-top: 20px;
  animation: fadeIn 0.8s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

iframe {
  width: 100%;
  height: 220px;
  border-radius: 15px;
  margin-top: 10px;
}
</style>
</head>

<body>

<div class="container">
  <h2>🚀 Animated Link Hub</h2>

  <input id="link" placeholder="Paste your link here">
  <textarea id="desc" placeholder="Write description..."></textarea>

  <button class="create-btn" onclick="generate()">✨ Create Link</button>

  <div id="preview" class="preview"></div>
</div>

<script>
function generate() {
  let link = document.getElementById("link").value;
  let desc = document.getElementById("desc").value;

  let youtubeEmbed = "";

  if(link.includes("youtube.com") || link.includes("youtu.be")){
    let videoId = link.split("v=")[1] || link.split("/").pop();
    youtubeEmbed = `<iframe src="https://www.youtube.com/embed/${videoId}"></iframe>`;
  }

  let page = `
    <div class="preview">
      <h3>📌 Your Link Page</h3>
      <p>${desc}</p>

      ${youtubeEmbed}

      <br>
      <a href="${link}" target="_blank">
        <button class="visit">🔗 Visit</button>
      </a>

      <a href="https://www.youtube.com/" target="_blank">
        <button class="youtube">▶ Subscribe</button>
      </a>

      <a href="https://discord.com/" target="_blank">
        <button class="discord">💬 Discord</button>
      </a>
    </div>
  `;

  document.getElementById("preview").innerHTML = page;
}
</script>

</body>
</html>
