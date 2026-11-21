# Weekly-Report-Generator
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Weekly Report Generator</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
:root{color-scheme:light;--bg:#eef1f5;--surface:#fff;--ink:#16202e;--muted:#5d6b7e;--line:#d6dce5;--accent:#23467a;--field:#f7f9fb;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){color-scheme:dark;--bg:#0f1520;--surface:#18202e;--ink:#e8edf5;--muted:#9aa8bb;--line:#2b3547;--accent:#7fa7e6;--field:#121a27}}
:root[data-theme="dark"]{color-scheme:dark;--bg:#0f1520;--surface:#18202e;--ink:#e8edf5;--muted:#9aa8bb;--line:#2b3547;--accent:#7fa7e6;--field:#121a27}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:15px/1.5 "IBM Plex Sans",system-ui,-apple-system,"Segoe UI",sans-serif}
header{padding:20px 24px 4px;max-width:1280px;margin:auto}
h1{font-size:22px;margin:0;font-weight:600}
header p{margin:2px 0 0;color:var(--muted)}
.steps{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
.steps span{font-size:13px;background:var(--surface);border:1px solid var(--line);border-radius:99px;padding:3px 12px;color:var(--muted)}
.steps b{color:var(--accent)}
.wrap{display:grid;grid-template-columns:minmax(0,1fr) minmax(0,1.1fr);gap:20px;padding:16px 24px 40px;max-width:1280px;margin:auto}
@media(max-width:900px){.wrap{grid-template-columns:1fr;padding:12px}header{padding:16px 12px 0}}
.panel{background:var(--surface);border:1px solid var(--line);border-radius:10px;padding:16px}
.panel h2{font-size:15px;margin:0 0 10px;font-weight:600}
label{display:block;font-size:13px;color:var(--muted);margin:8px 0 3px}
input,select{width:100%;font:inherit;color:var(--ink);background:var(--field);border:1px solid var(--line);border-radius:6px;padding:9px 10px}
input:focus-visible,select:focus-visible,button:focus-visible{outline:2px solid var(--accent);outline-offset:1px}
.row{display:flex;gap:10px}.row>div{flex:1}
.proj{background:var(--surface);border:1px solid var(--line);border-radius:10px;padding:14px;margin-top:12px}
.proj-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:6px}
.proj-head h3{margin:0;font-size:17px;font-weight:600}
button{font:inherit;cursor:pointer;border:1px solid var(--line);background:var(--surface);color:var(--ink);border-radius:6px;padding:8px 14px;min-height:38px}
button.primary{background:var(--accent);border-color:var(--accent);color:var(--surface);font-weight:500}
button.ghost{color:var(--muted);background:transparent}
.task{display:flex;gap:6px;margin-top:6px;align-items:center}
.task select{flex:0 0 128px;font-size:13px;padding:8px 6px}
.task input{flex:1;min-width:0}
.task button{flex:none;padding:6px 10px}
.task .ck{color:#1f9d62;font-weight:700}
.task.add{margin-top:10px;padding-top:10px;border-top:1px dashed var(--line)}
.tag{display:inline-block;font-size:12px;font-weight:600;padding:1px 8px;border-radius:99px;color:color-mix(in srgb,var(--c,#5b5f9a) 72%,var(--ink));background:color-mix(in srgb,var(--c,#5b5f9a) 16%,transparent)}
.t-init{--c:#3b82c4}.t-prog{--c:#d98a1a}.t-pend{--c:#8a8f98}.t-rev{--c:#7c5cc4}.t-esc{--c:#d6453d}.t-hold{--c:#b0883a}.t-done{--c:#1f9d62}
.hint{font-size:12.5px;color:var(--muted);margin:8px 0 0}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.sticky{position:sticky;top:12px;align-self:start}
@media(max-width:900px){.sticky{position:static}}
.report{background:var(--surface);border:1px solid var(--line);border-radius:10px;padding:28px 30px}
.report h3{margin:0;font-size:24px;font-weight:600}
.period{color:var(--muted);margin:2px 0 14px}
.stats{display:flex;gap:8px;flex-wrap:wrap}
.rproj{border-top:1px solid var(--line);padding-top:12px;margin-top:16px;break-inside:avoid}
.rproj h4{margin:0 0 4px;font-size:17px;font-weight:600}
.sec{margin:8px 0 0}.sec ul{margin:5px 0 0;padding-left:20px}.sec li{margin:2px 0}
.empty{color:var(--muted);padding:14px 0}
.start{text-align:center;padding:26px 12px;border:2px dashed var(--line);border-radius:10px;margin-top:12px;color:var(--muted)}
.start button{margin-top:8px}
@media(max-width:600px){.report{padding:18px}.task select{flex-basis:104px}}
dialog{border:1px solid var(--line);border-radius:12px;background:var(--surface);color:var(--ink);padding:18px;width:min(460px,92vw);max-height:80vh}
dialog::backdrop{background:rgba(10,15,25,.55)}
dialog h2{margin:0 0 10px;font-size:17px}
.plist{max-height:42vh;overflow:auto;margin:10px 0;display:flex;flex-direction:column;gap:4px}
.plist button{text-align:left;border-color:transparent;background:var(--field)}
.plist button:hover{border-color:var(--accent)}
.plist .new{color:var(--accent);font-weight:500}
.toast{position:fixed;left:50%;bottom:calc(20px + env(safe-area-inset-bottom,0px));transform:translateX(-50%);background:var(--ink);color:var(--bg);padding:8px 14px;border-radius:8px;opacity:0;pointer-events:none;transition:opacity .2s;z-index:50;width:max-content;max-width:92vw}
.toast.on{opacity:1;pointer-events:auto}
.toast button{margin-left:8px;padding:2px 10px;min-height:0;background:transparent;color:inherit;border-color:currentColor}
@media print{body{background:#fff}header,.edit,.actions,.tg,.toast{display:none}.wrap{display:block;padding:0}.report{border:0;padding:0}:root{--ink:#000;--muted:#444;--line:#bbb;--surface:#fff}}
</style>
</head>
<body>
<header>
<h1>Weekly report generator</h1>
<p>Everything saves automatically on this device.</p>
<div class="steps"><span><b>1</b> Add a project</span><span><b>2</b> Type your tasks</span><span><b>3</b> Send to Telegram</span></div>
</header>
<div class="wrap">
<div class="edit">
<div class="panel">
<h2>Report details</h2>
<label for="title">Title</label><input id="title">
<div class="row"><div><label for="from">From</label><input id="from" type="date"></div><div><label for="to">To</label><input id="to" type="date"></div></div>
</div>
<div id="projects"></div>
<div class="actions" style="margin-top:12px"><button class="primary" id="addProj">+ Add project</button><button id="newWeek" title="Keeps unfinished tasks, removes completed ones">Start new week</button><button class="ghost" id="reset">Clear all</button></div>
</div>
<div class="sticky">
<div class="actions"><button class="primary" id="tg">Send to Telegram</button><button id="copyText">Copy report</button><button id="print">Print / Save PDF</button></div>
<div class="report" id="report"></div>
<div class="panel tg" style="margin-top:12px">
<h2>Telegram topic (optional)</h2>
<label for="topic">Topic link</label>
<input id="topic" placeholder="https://t.me/c/1234567890/12">
<p class="hint">With a link, “Send to Telegram” copies the report and opens your topic: just paste and press Send. Without one, Telegram opens with the report filled in and you choose the chat. To get the link, long-press a message in the topic and choose Copy Link.</p>
</div>
</div>
</div>
<dialog id="dlg">
<h2>Add project</h2>
<input id="q" placeholder="Search, or type a new project name" aria-label="Search or add project" autocomplete="off">
<div class="plist" id="plist"></div>
<div class="actions" style="margin:6px 0 0"><button id="close">Cancel</button></div>
</dialog>
<div class="toast" id="toast"></div>
<script>
const ST=[["init","Initiated","t-init"],["prog","In Progress","t-prog"],["pend","Pending","t-pend"],["rev","Under Review","t-rev"],["esc","Escalated","t-esc"],["hold","On Hold","t-hold"],["done","Completed","t-done"]];
const CAT=["Kaldis","Lucy","Nur-keir","Celavie","Bloom Healthy Eating","Celavie Chicken 2018","Coffee Cology Cafe And Breakfast Service","Elfign Cafe And Restaurant Plc","Emmas Industrial Trading Plc","Etete Business Group Plc","Eton Trading Plc (Eton Foods And Pastry)","Gusto Trattoria Restaurant Plc","J And K Restaurant","Kaldis Coffee 2018","Kategna Bar And Restaurant 2018","Lucy Bar","Michael Girma Taye","Romina Plc","Top Table Trading Plc","Nur Keir"];
const iso=d=>d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0")+"-"+String(d.getDate()).padStart(2,"0");
function blank(cat){const n=new Date(),m=new Date(n);m.setDate(n.getDate()-((n.getDay()+6)%7));const s=new Date(m);s.setDate(m.getDate()+5);return{title:"Weekly Report",from:iso(m),to:iso(s),catalog:cat||CAT.slice(),topic:"",projects:[]}}
let S;try{S=JSON.parse(localStorage.getItem("wr2-state"))}catch(e){}
if(!S||!S.projects)S=blank();S.projects.forEach(p=>p.tasks.forEach(t=>{if(t.s==="other")t.s="pend"}));
let U=null,tt;
const $=id=>document.getElementById(id);
const esc=s=>String(s).replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
const save=()=>{try{localStorage.setItem("wr2-state",JSON.stringify(S))}catch(e){}};
const snap=()=>{U=JSON.stringify(S)};
const renderAll=()=>{renderForm();renderReport()};
const fmt=d=>{const[y,m,a]=d.split("-").map(Number);return new Date(y,m-1,a).toLocaleDateString("en-US",{month:"short",day:"2-digit"})};
const period=()=>S.from&&S.to?`${fmt(S.from)} – ${fmt(S.to)}, ${S.to.slice(0,4)}`:S.from?fmt(S.from):"";
const stOpts=cur=>ST.map(([k,n])=>`<option value="${k}"${k===cur?" selected":""}>${n}</option>`).join("");
function renderForm(){
$("title").value=S.title;$("from").value=S.from;$("to").value=S.to;$("topic").value=S.topic||"";
$("projects").innerHTML=S.projects.length?S.projects.map((p,i)=>`<div class="proj"><div class="proj-head"><h3>${esc(p.name)}</h3><button class="ghost" data-del="${i}">Remove</button></div>`+
p.tasks.map((t,j)=>`<div class="task"><select data-i="${i}" data-j="${j}" data-f="s" aria-label="Status">${stOpts(t.s)}</select><input data-i="${i}" data-j="${j}" data-f="t" value="${esc(t.t)}" aria-label="Task"><button class="ck" data-ck="${i}.${j}" aria-label="Mark completed" title="Mark completed">✓</button><button class="ghost" data-dt="${i}.${j}" aria-label="Delete task">✕</button></div>`).join("")+
`<div class="task add"><select data-ns="${i}" aria-label="Status for new task">${stOpts(p.ns||"prog")}</select><input id="nt${i}" data-add="${i}" placeholder="Write a task, press Enter" aria-label="New task"><button class="primary" data-addt="${i}">Add</button></div></div>`).join(""):`<div class="start">No projects yet.<br><button class="primary" data-open="1">+ Add your first project</button></div>`}
function renderReport(){
let tot=Object.fromEntries(ST.map(s=>[s[0],0]));
const body=S.projects.map(p=>{const secs=ST.map(([k,n,c])=>{const it=p.tasks.filter(t=>t.s===k&&t.t.trim());tot[k]+=it.length;return it.length?`<div class="sec"><span class="tag ${c}">${n}</span><ul>${it.map(t=>`<li>${esc(t.t)}</li>`).join("")}</ul></div>`:""}).join("");
return `<div class="rproj"><h4>${esc(p.name)}</h4>${secs||'<div class="empty">No tasks yet.</div>'}</div>`}).join("");
$("report").innerHTML=`<h3>${esc(S.title||"Weekly Report")}</h3><div class="period">${period()?"Period: "+period():""}</div><div class="stats">${ST.map(([k,n,c])=>tot[k]?`<span class="tag ${c}">${tot[k]} ${n.toLowerCase()}</span>`:"").join("")}</div>${body||'<div class="empty">Your report will appear here as you type.</div>'}`}
function toText(){let o=(S.title||"Weekly Report")+"\n"+(period()?"Period: "+period()+"\n":"");
S.projects.forEach(p=>{o+=`\nProject: ${p.name}\n`;ST.forEach(([k,n])=>{const it=p.tasks.filter(t=>t.s===k&&t.t.trim());if(!it.length)return;o+=n+"\n";it.forEach(t=>o+="- "+t.t.trim()+"\n")})});return o.trim()+"\n"}
function toast(m,undo){const t=$("toast");t.innerHTML=esc(m)+(undo?' <button id="undo">Undo</button>':"");t.classList.add("on");clearTimeout(tt);tt=setTimeout(()=>t.classList.remove("on"),undo?7000:2600);if(undo)$("undo").onclick=()=>{S=JSON.parse(U);save();renderAll();t.classList.remove("on")}}
function copy(t,msg){return(navigator.clipboard?navigator.clipboard.writeText(t):Promise.reject()).catch(()=>{const a=document.createElement("textarea");a.value=t;document.body.appendChild(a);a.select();try{document.execCommand("copy")}catch(e){}a.remove()}).then(()=>{if(msg)toast(msg)})}
function addTask(i){const inp=$("nt"+i),v=inp.value.trim();if(!v)return;const p=S.projects[i];p.tasks.push({t:v,s:p.ns||"prog"});save();renderAll();$("nt"+i).focus()}
function list(){const raw=$("q").value.trim(),q=raw.toLowerCase(),used=S.projects.map(p=>p.name);
const l=S.catalog.filter(n=>!used.includes(n)&&n.toLowerCase().includes(q));
const exists=S.catalog.some(n=>n.toLowerCase()===q);
let h=l.map(n=>`<button data-pick="${esc(n)}">${esc(n)}</button>`).join("");
if(raw&&!exists)h+=`<button class="new" data-pick="${esc(raw)}">+ Add “${esc(raw)}” as a new project</button>`;
$("plist").innerHTML=h||'<div class="empty">Type a name to add a project.</div>'}
function addProject(n){n=n.trim();if(!n||S.projects.some(p=>p.name===n))return;if(!S.catalog.includes(n))S.catalog.push(n);S.projects.push({name:n,tasks:[],ns:"prog"});save();$("dlg").close();renderAll();$("nt"+(S.projects.length-1)).focus()}
function openDlg(){$("q").value="";list();$("dlg").showModal();$("q").focus()}
function fresh(keepUnfinished){const n=blank(S.catalog);n.topic=S.topic;n.title=S.title;if(keepUnfinished)n.projects=S.projects.map(p=>({name:p.name,ns:p.ns,tasks:p.tasks.filter(t=>t.s!=="done"&&t.t.trim())})).filter(p=>p.tasks.length);return n}
document.addEventListener("input",e=>{const t=e.target;
if(t.id==="title")S.title=t.value;else if(t.id==="from")S.from=t.value;else if(t.id==="to")S.to=t.value;else if(t.id==="topic")S.topic=t.value;
else if(t.id==="q"){list();return}
else if(t.dataset.f){S.projects[t.dataset.i].tasks[t.dataset.j][t.dataset.f]=t.value}
else if(t.dataset.ns!==undefined){S.projects[t.dataset.ns].ns=t.value}else return;save();renderReport()});
document.addEventListener("keydown",e=>{const t=e.target;if(e.key!=="Enter")return;
if(t.dataset.add!==undefined){e.preventDefault();addTask(t.dataset.add)}
else if(t.id==="q"){e.preventDefault();const b=$("plist").querySelector("button");if(b)addProject(b.dataset.pick)}});
document.addEventListener("click",e=>{const b=e.target.closest("button");if(!b)return;const d=b.dataset;
if(d.del!==undefined){snap();S.projects.splice(+d.del,1);save();renderAll();toast("Project removed",1)}
else if(d.dt){const[i,j]=d.dt.split(".");snap();S.projects[i].tasks.splice(+j,1);save();renderAll();toast("Task deleted",1)}
else if(d.ck){const[i,j]=d.ck.split(".");S.projects[i].tasks[j].s="done";save();renderAll();toast("Marked as completed")}
else if(d.addt!==undefined)addTask(d.addt);
else if(d.open)openDlg();
else if(d.pick!==undefined)addProject(d.pick)});
$("addProj").onclick=openDlg;
$("close").onclick=()=>$("dlg").close();
$("dlg").addEventListener("click",e=>{if(e.target===$("dlg"))$("dlg").close()});
$("newWeek").onclick=()=>{snap();S=fresh(true);save();renderAll();toast("New week started. Unfinished tasks were kept.",1)};
$("reset").onclick=()=>{snap();S=fresh(false);save();renderAll();toast("Report cleared",1)};
$("copyText").onclick=()=>copy(toText(),"Report copied");
$("print").onclick=()=>window.print();
$("tg").onclick=()=>{const link=(S.topic||"").trim(),txt=toText();
if(link){copy(txt,"Copied. Paste it in the topic and press Send.");window.open(link,"_blank","noopener")}
else{window.open("https://t.me/share/url?url=%20&text="+encodeURIComponent(txt),"_blank","noopener")}};
renderAll();
</script>
</body>
</html>
