# slides-apresentacao
Slides interativos com animação
<!DOCTYPE html><html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Slides PRO Futurista</title><style>
* { margin:0; padding:0; box-sizing:border-box; }
body {
  font-family: 'Segoe UI', sans-serif;
  background: radial-gradient(circle at center, #0a0015, #000);
  color: white;
  overflow: hidden;
}

/* PARTICULAS */
canvas {
  position: fixed;
  top:0; left:0;
  z-index:0;
}

.slide {
  position:absolute;
  width:100%; height:100%;
  display:flex;
  flex-direction:column;
  justify-content:center;
  padding:80px;
  opacity:0;
  transform:scale(0.95);
  transition: all 0.6s ease;
  z-index:1;
}

.slide.active {
  opacity:1;
  transform:scale(1);
}

h1 {
  font-size:60px;
  background: linear-gradient(90deg,#00eaff,#a855f7);
  -webkit-background-clip:text;
  color:transparent;
  text-shadow:0 0 30px rgba(168,85,247,0.6);
}

.card {
  margin-top:30px;
  padding:25px;
  width:420px;
  background: rgba(255,255,255,0.05);
  border:1px solid rgba(168,85,247,0.5);
  border-radius:20px;
  backdrop-filter: blur(20px);
  box-shadow:0 0 40px rgba(168,85,247,0.3);
  animation: float 6s ease-in-out infinite;
}

@keyframes float {
  0% { transform: translateY(0px); }
  50% { transform: translateY(-15px); }
  100% { transform: translateY(0px); }
}

/* BOTÕES */
.btn {
  position:absolute;
  bottom:25px;
  padding:12px 28px;
  border-radius:30px;
  border:1px solid #a855f7;
  background: rgba(168,85,247,0.1);
  backdrop-filter: blur(10px);
  cursor:pointer;
  transition:0.3s;
}

.btn:hover {
  box-shadow:0 0 20px #a855f7;
}

.prev { left:30px; }
.next { right:30px; }

.progress {
  position:absolute;
  bottom:0;
  left:0;
  height:4px;
  background:linear-gradient(90deg,#00eaff,#a855f7);
  width:0%;
}

.counter {
  position:absolute;
  bottom:20px;
  left:50%;
  transform:translateX(-50%);
  opacity:0.7;
}

</style></head>
<body><canvas id="bg"></canvas>

<div class="slide active">
  <h1>Machismo na Sociedade</h1>
  <div class="card">Pesquisa Sociológica<br>Jovens × Adultos<br>Dados 2024</div>
</div><div class="slide">
  <h1>Introdução</h1>
  <div class="card">• Diferença geracional<br>• Percepção social<br>• Cultura influencia</div>
</div><div class="slide">
  <h1>Metodologia</h1>
  <div class="card">Grupo A: Jovens</div>
  <div class="card">Grupo B: Adultos</div>
</div><div class="slide">
  <h1>Perguntas</h1>
  <div class="card">01 - Existe machismo?</div>
  <div class="card">02 - Já presenciou?</div>
</div><div class="slide">
  <h1>Resultados</h1>
  <div class="card">Jovens: 80%</div>
  <div class="card">Adultos: 60%</div>
</div><div class="slide">
  <h1>Análise</h1>
  <div class="card">+16% diferença média</div>
</div><div class="slide">
  <h1>Interpretação</h1>
  <div class="card">Machismo estrutural</div>
</div><div class="slide">
  <h1>Conclusão</h1>
  <div class="card">Jovens percebem mais</div>
</div><div class="slide">
  <h1>Obrigado!</h1>
</div><div class="btn prev" onclick="prevSlide()">ANTERIOR</div>
<div class="btn next" onclick="nextSlide()">PRÓXIMO</div>
<div class="counter" id="counter">01 / 09</div>
<div class="progress" id="progress"></div><script>
// SLIDES
let current = 0;
const slides = document.querySelectorAll('.slide');
const progress = document.getElementById('progress');
const counter = document.getElementById('counter');

function showSlide(i) {
  slides.forEach(s => s.classList.remove('active'));
  slides[i].classList.add('active');
  progress.style.width = ((i+1)/slides.length)*100 + '%';
  counter.innerText = String(i+1).padStart(2,'0') + ' / 09';
}

function nextSlide() {
  current = (current + 1) % slides.length;
  showSlide(current);
}

function prevSlide() {
  current = (current - 1 + slides.length) % slides.length;
  showSlide(current);
}

// PARTÍCULAS
const canvas = document.getElementById('bg');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];
for(let i=0;i<80;i++){
  particles.push({
    x:Math.random()*canvas.width,
    y:Math.random()*canvas.height,
    r:Math.random()*2,
    dx:(Math.random()-0.5)*0.5,
    dy:(Math.random()-0.5)*0.5
  });
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  ctx.fillStyle = '#a855f7';
  particles.forEach(p=>{
    p.x+=p.dx; p.y+=p.dy;
    if(p.x<0||p.x>canvas.width) p.dx*=-1;
    if(p.y<0||p.y>canvas.height) p.dy*=-1;
    ctx.beginPath();
    ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fill();
  });
  requestAnimationFrame(animate);
}
animate();
</script></body>
</html>
