<html lang="tr">
<head>
<meta charset="UTF-8">
<title>Dual Sync Video Switch</title>
<style>
  body{
    margin:0;background:#000;height:100vh;color:#ff0000;
    display:flex;justify-content:center;align-items:center;
    font-family:Arial;
  }
  #wrap{ position:relative;width:90%;max-width:600pxaspect-ratio:16 / 9; }
  video{
    position:absolute;top:0;left:0;width:100%;border-radius:10px;
    transition:opacity .4s;
  }
  #videoB{opacity:0;} /* ilk A görünecek */
  #label{
    position:absolute;top:20px;background:rgba(0,0,0,.6);
    padding:10px 18px;border-radius:8px;font-size:18px;
  }
  #startBtn{padding:12px 24px;font-size:18px;margin-bottom:20px;cursor:pointer;}
</style>
</head>
<body>

<button id="startBtn"> Videoyu Oynat </button>

<div id="wrap">
    <div id="label"> A Aktif</div>
    <video id="videoA" src="video1.mp4"></video>
    <video id="videoB" src="video2.mp4"></video>
</div>

<p>A ve B</p>

<script>
const A = document.getElementById("videoA");
const B = document.getElementById("videoB");
const label = document.getElementById("label");
const startBtn = document.getElementById("startBtn");

let running = false;


startBtn.onclick = ()=>{
    A.play(); B.play();
    A.muted=false; B.muted=true; // sadece A sesi açık
    running = true;
    startBtn.style.display="none";
}

// Kamera geçiş fonksiyonu
function switchCam(cam){
    if(!running) return alert("Önce ▶ Başlat'a bas.");
    
    const t = A.currentTime; // ortak zaman
    A.currentTime = t;
    B.currentTime = t;

    if(cam==="A"){
        A.style.opacity=1; B.style.opacity=0;
        A.muted=false; B.muted=true;
        label.innerText="Kamera A Aktif";
    }else{
        A.style.opacity=0; B.style.opacity=1;
        A.muted=true; B.muted=false;
        label.innerText="Kamera B Aktif";
    }
}


document.addEventListener("keydown",(e)=>{
    if(e.key==="1") switchCam("A");
    if(e.key==="2") switchCam("B");
});
</script>

</body>
</html>
