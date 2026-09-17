<!DOCTYPE html>
<html><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>OMUGO Admin</title><link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap" rel="stylesheet"><style>body{font-family:Inter;background:#080a0b;color:#fff;padding:20px} .card{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);border-radius:14px;padding:16px;margin:10px 0}</style></head>
<body>
<h1>OMUGO AI - Admin Dashboard 🔐</h1><p style="color:#aaa">See all who built website on OMUGO</p>
<div style="margin:16px 0"><input id="pass" placeholder="Enter admin password" style="padding:10px;border-radius:8px;border:none"><button onclick="checkPass()" style="padding:10px 16px;border-radius:8px;background:#C9A227;border:none;font-weight:800;margin-left:6px">Login</button></div>
<div id="stats" style="display:none"><h3 id="total"></h3><div id="list"></div></div>
<script>
function checkPass(){if(document.getElementById('pass').value==='omugo2026'){document.getElementById('stats').style.display='block';loadData()}else{alert('Wrong password! Use omugo2026')}}
async function loadData(){
 let data = JSON.parse(localStorage.getItem('omugo_sites')||'[]');
 // Try fetch from Puter KV if you use real backend later
 document.getElementById('total').innerText = 'Total Websites Built: ' + data.length;
 let html='';
 data.reverse().forEach((s,i)=>{
   html+=`<div class="card"><b>${i+1}. ${s.name}</b><br><small style="color:#FFD84D">${s.date}</small><br><div style="font-size:12px;color:#aaa;margin-top:6px">Prompt: ${s.prompt.substring(0,150)}...</div><div style="margin-top:8px"><button onclick="navigator.clipboard.writeText(\`${s.html.replace(/`/g,'\\`')}\`);alert('HTML copied!')" style="padding:6px 10px;border-radius:6px;background:#0D4A2E;color:#fff;border:none;font-size:11px">Copy HTML</button></div></div>`;
 });
 if(data.length===0) html='<p style="color:#888">No sites yet. When someone clicks Publish, it will appear here on their device. For global tracking, we need Firebase (I can add).</p>';
 document.getElementById('list').innerHTML=html;
}
</script>
</body></html>
