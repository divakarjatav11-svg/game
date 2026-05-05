# Horror Game Based on Japanese Urban Legends

This is a horror game inspired by Japanese urban legends. Experience the chilling tales that have haunted Japanese folklore for generations.

## Game Features

- Immersive horror atmosphere
- Interactive storytelling
- Based on real Japanese urban legends

## How to Play

[Instructions will be added here]

## Technologies Used

- HTML5
- CSS3
- JavaScript

## Installation

Clone the repository and open `index.html` in your browser.

## Contributing

Feel free to contribute to the development of this game.

## License

[Add license information here] 
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Japanese Urban Legend Horror Game</title>

<style>
body {
  margin: 0;
  background: black;
  color: white;
  font-family: Arial, sans-serif;
  overflow: hidden;
}

#bg {
  position: fixed;
  width: 100%;
  height: 100%;
  background: url('https://via.placeholder.com/800x600/000000/FFFFFF?text=Dark+Forest') center/cover;
  filter: brightness(0.3);
}

#box {
  position: absolute;
  bottom: 0;
  width: 100%;
  background: rgba(0,0,0,0.9);
  padding: 20px;
}

#text {
  font-size: 18px;
  margin-bottom: 10px;
}

input {
  width: 70%;
  padding: 10px;
  font-size: 16px;
}

button {
  padding: 10px;
  background: crimson;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background: darkred;
}
</style>
</head>
<body>
<div id="bg"></div>
<div id="box">
  <div id="text">You are walking alone in a dark Japanese forest at night. You hear strange whispers. What do you do? (Type 'run' or 'investigate')</div>
  <input type="text" id="input" placeholder="Enter your choice...">
  <button onclick="processInput()">Submit</button>
</div>

<script>
let gameState = 'start';

function processInput() {
  const input = document.getElementById('input').value.toLowerCase();
  const text = document.getElementById('text');
  
  if (gameState === 'start') {
    if (input === 'run') {
      text.innerHTML = 'You run away, but the whispers follow you. Suddenly, you see a woman with a slit mouth blocking your path. "Am I pretty?" she asks. (Type 'yes' or 'no')';
      gameState = 'woman';
    } else if (input === 'investigate') {
      text.innerHTML = 'You follow the whispers and find an old well. A ghostly hand reaches out. You die. Game Over.';
      gameState = 'end';
    } else {
      text.innerHTML = 'Invalid choice. You are walking alone in a dark Japanese forest at night. You hear strange whispers. What do you do? (Type \'run\' or \'investigate\')';
    }
  } else if (gameState === 'woman') {
    if (input === 'yes') {
      text.innerHTML = 'She smiles hideously and slashes you. You die. Game Over. (Inspired by Kuchisake-onna)';
      gameState = 'end';
    } else if (input === 'no') {
      text.innerHTML = 'She gets angry and chases you. You barely escape. You survived... for now.';
      gameState = 'end';
    } else {
      text.innerHTML = 'Invalid choice. "Am I pretty?" she asks. (Type \'yes\' or \'no\')';
    }
  }
  
  document.getElementById('input').value = '';
}
</script>
</body>
</html>

</style>
</head>

<body>

<div id="bg"></div>

<div id="box">
  <div id="text">Game Start...</div>
  <input id="input" placeholder="Type your answer...">
  <button onclick="send()">Send</button>
</div>

<!-- Optional sounds -->
<audio id="whisper" src="" ></audio>

<script>

let step = 0;
let fear = 0;

let text = document.getElementById("text");
let input = document.getElementById("input");
let bg = document.getElementById("bg");

function show(t){
  text.innerText = t;
}

function setBG(url){
  bg.style.background = `url('${url}') center/cover`;
}

function wrong(){
  fear++;
  document.body.style.filter = "blur(" + fear + "px)";
  show("Something feels wrong...");
  
  if(fear >= 3){
    show("She is behind you...");
    setTimeout(()=>{ alert("GAME OVER"); location.reload(); },2000);
  }
}

function send(){
  let ans = input.value.toLowerCase().trim();
  input.value = "";

  // INTRO
  if(step === 0){
    show("School: They talk about ghosts... Takashi laughs...");
    step++;
  }

  // TAKASHI PATH
  else if(step === 1){
    show("Old lady: Take another path today...");
    step++;
  }

  else if(step === 2){
    show("Type: left OR right");
    step++;
  }

  else if(step === 3){
    if(ans === "right"){
      show("Kuchisake Onna: Let's play a game...");
      step = 10;
    } else {
      show("You safely reach home... but something feels off...");
      step = 20;
    }
  }

  // RIDDLES TAKASHI
  else if(step === 10){
    show("I speak without a mouth...");
    if(ans === "echo"){
      step++;
    } else wrong();
  }

  else if(step === 11){
    show("I have keys but no locks...");
    if(ans === "keyboard"){
      step++;
    } else wrong();
  }

  else if(step === 12){
    show("How many hairs do you have?");
    if(ans.includes("15")){
      show("She smiles... you survived...");
      step = 20;
    } else wrong();
  }

  // AKI LEVEL
  else if(step === 20){
    setBG("https://via.placeholder.com/800x600/222"); // replace with kitchen image
    show("Aki is cooking... Doorbell rings...");
    step++;
  }

  else if(step === 21){
    show("I have a face and two hands...");
    if(ans === "clock"){
      step++;
    } else wrong();
  }

  else if(step === 22){
    show("The more you use me, the sharper I become...");
    if(ans === "brain"){
      step++;
    } else wrong();
  }

  else if(step === 23){
    show("I make things hot...");
    if(ans.includes("stove")){
      show("She disappears...");
      step = 30;
    } else wrong();
  }

  // FINAL YUKI
  else if(step === 30){
    show("Should a woman be beautiful?");
    if(ans === "yes"){
      step++;
    } else wrong();
  }

  else if(step === 31){
    show("Am I beautiful?");
    if(ans === "yes"){
      step++;
    } else wrong();
  }

  else if(step === 32){
    show("Am I beautiful?");
    if(ans.includes("beautiful")){
      show("She steps aside... You survived.");
    } else {
      wrong();
    }
  }

}

</script>

</body>
</html>