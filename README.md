<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>OMUGO AI - Admin</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap" rel="stylesheet">
<style>body{font-family:Inter;background:#080a0b;color:#fff;padding:20px}.card{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);border-radius:14px;padding:16px;margin:10px 0}.btn{padding:8px 14px;border-radius:8px;border:none;font-weight:800;cursor:pointer}</style>
</head>
<body>
<h1 style="font-size:24px">OMUGO AI - Admin Dashboard 🔐</h1>
<p style="color:#aaa;font-size:13px">See all websites built on this device. For global tracking, we will add Google Sheet later (free).</p>
<div style="margin:16px 0"><input id="pass" placeholder="Enter password" style="padding:10px;border-radius:8px;border:none;width:200px"><button onclick="checkPass()" class="btn" style="background:#C9A227;margin-left:6px">Login</button></div>
<div id="stats" style="display:none">
<h3 id="total"></h3>
<div style="margin:10px 0"><button onclick="clearAll()" style="background:#ff3b3b;color:#fff" class="btn">Clear All Data</button> <button onclick="location.reload()" class="btn" style="background:#333;color:#fff">Refresh</button></div>
<div id="list"></div>
</div>
<script>
function checkPass(){
 if(document.getElementById('pass').value==='omugo2026'){
  document.getElementById('stats').style.display='block'; loadData();
 }else{alert('Wrong password! Use: omugo2026')}
}
function loadData(){
 let data = JSON.parse(localStorage.getItem('omugo_sites')||'[]');
 document.getElementById('total').innerText = 'Total Websites Built on this device: ' + data.length;
 let html='';
 if(data.length===0){html='<p style="color:#888;margin-top:20px">No sites yet. Build a website and click Publish - it will appear here. <br><br>NOTE: This shows only sites built on THIS phone/computer. To see ALL users worldwide, we need to connect free Google Sheet - I can do that for you next, no cost.</p>'}
 data.slice().reverse().forEach((s,i)=>{
  html+=`<div class="card"><b>${data.length-i}. ${s.name}</b><br><small style="color:#FFD84D">${s.date}</small><br><div style="font-size:12px;color:#aaa;margin-top:8px;background:rgba(0,0,0,.3);padding:8px;border-radius:8px;max-height:80px;overflow:auto">Prompt: ${s.prompt}</div><div style="margin-top:10px;display:flex;gap:6px"><button onclick="viewSite(${data.length-1-i})" class="btn" style="background:#0D4A2E;color:#fff;font-size:11px">View Site</button><button onclick="copyHtml(${data.length-1-i})" class="btn" style="background:#C9A227;font-size:11px">Copy HTML</button></div></div>`;
 });
 document.getElementById('list').innerHTML=html;
}
function viewSite(idx){
 let data = JSON.parse(localStorage.getItem('omugo_sites')||'[]');
 let w = window.open(); w.document.write(data[idx].html);
}
function copyHtml(idx){
 let data = JSON.parse(localStorage.getItem('omugo_sites')||'[]');
 navigator.clipboard.writeText(data[idx].html); alert('HTML copied!');
}
function clearAll(){if(confirm('Delete all?')){localStorage.removeItem('omugo_sites'); loadData();}}
</script>
</body>
</html>
