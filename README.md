<!DOCTYPE html>
<html lang="fa">
<head>
<meta charset="UTF-8">
<title>🔵 NASA / ESA Ion Engine</title>
<style>
  html,body{
    margin:0;
    overflow:hidden;
    background:#00060f;
    font-family:system-ui,sans-serif;
  }
  #info{
    position:absolute;
    top:12px;
    left:12px;
    padding:8px 14px;
    border-radius:10px;
    background:rgba(255,255,255,0.06);
    color:#cfefff;
    backdrop-filter: blur(8px);
    box-shadow:0 0 20px rgba(120,200,255,0.15);
  }
</style>
</head>
<body>
<canvas id="c"></canvas>
<div id="info">🔵 NASA / ESA Ion Thruster — Hold Mouse</div>

<script>
const canvas = document.getElementById("c");
const ctx = canvas.getContext("2d");
let w,h;
function resize(){
  w = canvas.width = innerWidth;
  h = canvas.height = innerHeight;
}
resize();
addEventListener("resize", resize);

let ions = [];
let active = false;
let mouse = {x:w/2, y:h/2};

addEventListener("mousemove", e=>{
  mouse.x = e.clientX;
  mouse.y = e.clientY;
});
addEventListener("mousedown", ()=> active = true);
addEventListener("mouseup", ()=> active = false);

function emitIons(){
  if(!active) return;

  for(let i=0;i<7;i++){
    ions.push({
      x: mouse.x,
      y: mouse.y,
      vx: -2.2 - Math.random()*1.2,
      vy: (Math.random()-0.5)*0.6,
      life: 180,
