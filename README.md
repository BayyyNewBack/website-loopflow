<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>LoopFlow System</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');
    *{margin:0;padding:0;box-sizing:border-box;font-family:'Orbitron',sans-serif;}
    body{overflow:hidden;height:100vh;display:flex;justify-content:center;align-items:center;color:#00ffff;background:black;}
    video#bg-video{position:fixed;top:0;left:0;width:100%;height:100%;object-fit:cover;z-index:-2;}
    audio#bg-sound{display:none;}
    .login-container{background:rgba(0,0,0,.75);border:2px solid #00ffff;border-radius:15px;padding:30px;width:320px;text-align:center;box-shadow:0 0 30px #00ffff88;z-index:2;}
    .login-container h1{font-size:22px;margin-bottom:5px;color:#00ffff;text-shadow:0 0 15px #00ffff;}
    .login-container p{font-size:12px;color:#ffffffcc;margin-bottom:20px;}
    .input-group{text-align:left;margin-bottom:15px;}
    .input-group label{display:block;color:#00ffff;font-size:12px;margin-bottom:5px;}
    .input-group input{width:100%;padding:8px;border:1px solid #00ffff;border-radius:5px;background:transparent;color:#00ffff;outline:none;}
    .login-btn{background:linear-gradient(90deg,#00ffff,#ff00ff);border:none;padding:10px 20px;width:100%;border-radius:8px;font-weight:bold;cursor:pointer;color:#000;transition:.2s;}
    .login-btn:hover{transform:scale(1.05);box-shadow:0 0 20px #00ffffaa;}
    .error{color:#ff6666;font-size:12px;margin-top:10px;}
    .home-container{display:none;background:rgba(0,0,0,.75);border:2px solid #00ffff;border-radius:20px;width:340px;text-align:center;padding:25px;box-shadow:0 0 30px #00ffff77;z-index:2;}
    .home-container img{width:100%;border-radius:10px;}
    .title{font-size:20px;color:#ff00ff;margin-top:15px;text-shadow:0 0 15px #ff00ff;}
    .logged-user{font-size:13px;color:#00ff88;margin-top:8px;}
    table{margin:20px auto;border-collapse:collapse;width:90%;font-size:13px;}
    td{border:1px solid #00ffff;padding:8px;}
    td:first-child{color:#00ffff;text-align:left;}
    td:last-child{color:#fff;text-align:right;}
    .btn{display:block;margin:10px auto;padding:10px 15px;border-radius:10px;font-weight:bold;border:1px solid #ff00ff;color:white;width:80%;text-decoration:none;transition:.3s;}
    .btn:hover{background:#00ffff33;transform:scale(1.05);}
    .menu{display:flex;justify-content:space-around;margin-top:20px;flex-wrap:wrap;}
    .menu button{background:rgba(0,0,0,.6);border:1px solid #00ffff;border-radius:10px;color:#fff;width:90px;padding:8px;font-size:12px;cursor:pointer;transition:.3s;}
    .menu button:hover{background:#00ffff22;transform:scale(1.1);}
    .bug-container,.ddos-container{display:none;background:rgba(0,0,0,.75);border:2px solid #00ffff;border-radius:20px;width:340px;text-align:center;padding:25px;box-shadow:0 0 30px #00ffff77;z-index:2;}
    .bug-header,.ddos-header{display:flex;align-items:center;justify-content:center;margin-bottom:20px;}
    .bug-header img,.ddos-header img{width:40px;height:40px;margin-right:10px;}
    .bug-header h2,.ddos-header h2{color:#ff00ff;font-size:20px;text-shadow:0 0 15px #ff00ff;}
    .send-btn,.ddos-send-btn{background:linear-gradient(90deg,#00ffff,#0088ff);border:none;padding:12px 20px;width:100%;border-radius:8px;font-weight:bold;cursor:pointer;color:#000;margin-top:15px;transition:.2s;}
    .send-btn:hover,.ddos-send-btn:hover{transform:scale(1.05);box-shadow:0 0 20px #0088ffaa;}
    .success-message,.ddos-success-message{color:#00ff88;font-size:12px;margin-top:10px;display:none;}

    /* popup peraturan */
    .rules-popup{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.8);z-index:99;justify-content:center;align-items:center;}
    .rules-box{background:rgba(0,0,0,.9);border:2px solid #00ffff;border-radius:15px;width:320px;max-width:90%;padding:20px;text-align:left;box-shadow:0 0 30px #00ffff88;color:#00ffff;}
    .rules-box h3{text-align:center;margin-bottom:10px;color:#ff00ff;text-shadow:0 0 10px #ff00ff;}
    .rules-box ul{list-style:disc;margin-left:20px;margin-bottom:10px;}
    .rules-box p{font-size:12px;color:#fff;margin-top:8px;}
    .close-btn{display:block;margin:10px auto 0 auto;padding:6px 15px;border:none;border-radius:8px;background:linear-gradient(90deg,#00ffff,#ff00ff);color:#000;font-weight:bold;cursor:pointer;}
  </style>
</head>
<body>

  <video autoplay loop muted id="bg-video">
    <source src="https://files.catbox.moe/itnih5.mp4" type="video/mp4">
  </video>

  <audio id="bg-sound" autoplay>
    <source src="https://files.catbox.moe/kqgbks.mp4" type="audio/mp4">
  </audio>

  <!-- LOGIN -->
  <div class="login-container" id="login-page">
    <h1>LOOPFLOW Version WA </h1>
    <p> By Bayyy×Kizz</p>

    <div class="input-group">
      <label>Username</label>
      <input type="text" id="username" placeholder="Masukkan Username">
    </div>
    <div class="input-group">
      <label>Password</label>
      <input type="password" id="password" placeholder="Masukkan Password">
    </div>

    <button class="login-btn" onclick="login()">LOGIN</button>
    <p class="error" id="error-message"></p>
  </div>

  <!-- HOME -->
  <div class="home-container" id="home-page">
    <img src="https://files.catbox.moe/64r94h.jpg" alt="Header Image">
    <h2 class="title">LoopFlow Version</h2>
    <div class="logged-user" id="logged-user">Logged in as: -</div>

    <table>
      <tr><td>Informasi</td><td>LoopFlow</td></tr>
      <tr><td>Version</td><td>1.10.0 New Gen</td></tr>
      <tr><td>Status</td><td>Buy VIP Cr Justin</td></tr>
    </table>

    <a href="https://bayyyynewbackofficial.vercel.app" target="_blank" class="btn tiktok">🔴 Join TikTok Channel</a>
    <a href="https://whatsapp.com/channel/0029Vb6JZS4Gk1FrmiP0Jw3u" target="_blank" class="btn whatsapp">💚 Join WhatsApp Channel</a>

    <div class="menu">
      <button onclick="showHomePage()">🏠 Home</button>
      <button onclick="showRules()">📜 Peraturan</button>
      <button onclick="showBugPage()">💥 Bug WhatsApp</button>
      <button onclick="showDDoSPage()">👾 DDoS</button>
    </div>
  </div>

  <!-- POPUP PERATURAN -->
  <div class="rules-popup" id="rules-popup">
    <div class="rules-box">
      <h3>📜 Peraturan</h3>
      <ul>
        <li>Jeda 40 Menit</li>
        <li>No Spam</li>
        <li>No Coba fitur lain</li>
        <li>No mainin Bot</li>
        <li>No add ke grub</li>
        <li>No Spam Bug</li>
      </ul>
      <p><b>Disclaimer:</b> Jika pas kirim pesan tidak keluar prosesnya berarti WA kenon / tidak ada panel.</p>
      <p>Buy Res/mods/PT <br> Pv @BayyyNewBack</p>
      <button class="close-btn" onclick="closeRules()">Tutup</button>
    </div>
  </div>

  <!-- BUG PAGE -->
  <div class="bug-container" id="bug-page">
    <div class="bug-header">
      <img src="https://z-cdn-media.chatglm.cn/files/364e7d5f-c1ea-4fc8-a55f-8ff94177e387_Screenshot_2025-10-26-18-22-24-09_44c2167a04bb56a48929b7d3d4f2f46e.jpg" alt="Bug WhatsApp Icon">
      <h2>BUG WHATSAPP</h2>
    </div>

    <div class="bug-form">
      <div class="input-group">
        <label>Nomor Target</label>
        <input type="text" id="target-number" placeholder="628xxx (tanpa +/spasi)">
      </div>
      <div class="input-group">
        <label>Pilihan Bug</label>
        <select id="bug-type">
          <option value="">-- Pilih Bug --</option>
          <option value="bug-stiker">Bug Stiker</option>
          <option value="andro-fc">AndroFc</option>
          <option value="crash-ui">Crash Ui</option>
          <option value="loopflow-crash">LoopFlowCrasherrGen</option>
          <option value="delay-invis">Delayinvis</option>
          <option value="freeze-delay">Freeze×Delay</option>
        </select>
      </div>
      <button class="send-btn" onclick="sendBug()">SEND BUG</button>
      <p class="success-message" id="success-message">Mempersiapkan pesan WhatsApp...</p>
    </div>

    <div class="menu">
      <button onclick="showHomePage()">🏠 Home</button>
      <button onclick="showBugPage()">💥 Bug WhatsApp</button>
      <button onclick="showDDoSPage()">👾 DDoS</button>
    </div>
  </div>

  <!-- DDOS PAGE -->
  <div class="ddos-container" id="ddos-page">
    <div class="ddos-header">
      <img src="https://z-cdn-media.chatglm.cn/files/1d3b4634-4ccd-4e47-a143-10d3094db545_Screenshot_2025-10-26-18-22-30-95_44c2167a04bb56a48929b7d3d4f2f46e.jpg" alt="DDoS Icon">
      <h2>DDoS ATTACK</h2>
    </div>

    <div class="ddos-form">
      <div class="input-group">
        <label>Target URL</label>
        <input type="text" id="target-url" placeholder="https://example.com">
      </div>
      <div class="input-group">
        <label>Pilihan DDoos</label>
        <select id="ddos-type">
          <option value="">-- Pilih Layer --</option>
          <option value="physical">Physical Layer</option>
          <option value="data-link">Data Link Layer</option>
          <option value="network">Network Layer</option>
          <option value="transport">Transport Layer</option>
          <option value="session">Session Layer</option>
          <option value="presentation">Presentation Layer</option>
          <option value="application">Application Layer</option>
        </select>
      </div>
      <button class="ddos-send-btn" onclick="sendDDoS()">> SEND DDoS</button>
      <p class="ddos-success-message" id="ddos-success-message">DDoS Attack Terkirim</p>
    </div>

    <div class="menu">
      <button onclick="showHomePage()">🏠 Home</button>
      <button onclick="showBugPage()">💥 Bug WhatsApp</button>
      <button onclick="showDDoSPage()">👾 DDoS</button>
    </div>
  </div>

  <script>
    const validUsers={"bay":"bay123","buyer":"buyer123","admin":"admin123"};

    function login(){
      const user=document.getElementById("username").value.trim();
      const pass=document.getElementById("password").value.trim();
      const error=document.getElementById("error-message");
      if(user in validUsers && validUsers[user]===pass){
        document.getElementById("login-page").style.display="none";
        document.getElementById("home-page").style.display="block";
        document.getElementById("logged-user").textContent="Logged in as: "+user;
        const s=document.getElementById("bg-sound");if(s.paused)s.play();
        error.textContent="";
      }else{error.textContent="Username atau Password salah!";}
    }

    function showHomePage(){hideAll();document.getElementById("home-page").style.display="block";}
    function showBugPage(){hideAll();document.getElementById("bug-page").style.display="block";}
    function showDDoSPage(){hideAll();document.getElementById("ddos-page").style.display="block";}
    function hideAll(){["home-page","bug-page","ddos-page"].forEach(id=>document.getElementById(id).style.display="none");}

    const bugCommandMap={
      "bug-stiker":".bugstiker",
      "andro-fc":".forcexfrezee",
      "crash-ui":".crashui",
      "loopflow-crash":".crashxfrezee",
      "delay-invis":".delayinvis",
      "freeze-delay":".frezeexdelay"
    };

    function sendBug(){
      const raw=document.getElementById("target-number").value.trim();
      const bugType=document.getElementById("bug-type").value;
      const msg=document.getElementById("success-message");
      const fixedRecipient="6282254176446";
      if(!raw){alert("Isi nomor target!");return;}
      if(!bugType){alert("Pilih jenis bug!");return;}
      const num=raw.replace(/\D/g,"");
      if(!/^\d{6,15}$/.test(num)){alert("Nomor tidak valid!");return;}
      const cmd=bugCommandMap[bugType]||bugType;
      const text=`${cmd} ${num}`;
      const wa=`https://wa.me/${fixedRecipient}?text=${encodeURIComponent(text)}`;
      msg.textContent="Membuka WhatsApp...";
      msg.style.display="block";
      window.open(wa,"_blank");
      setTimeout(()=>msg.style.display="none",1200);
    }

    function sendDDoS(){
      const t=document.getElementById("target-url").value.trim();
      const d=document.getElementById("ddos-type").value;
      const m=document.getElementById("ddos-success-message");
      if(t&&d){m.style.display="block";setTimeout(()=>m.style.display="none",3000);}
      else{alert("Isi URL dan pilih layer!");}
    }

    function showRules(){
      document.getElementById("rules-popup").style.display="flex";
    }
    function closeRules(){
      document.getElementById("rules-popup").style.display="none";
    }

    document.addEventListener('click',()=>{
      const s=document.getElementById("bg-sound");
      if(s.paused)s.play();
    });
  </script>
</body>
</html>
