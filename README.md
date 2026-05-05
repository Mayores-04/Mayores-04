<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --bg:#0a0a0f;
    --surface:#13131a;
    --surface2:#1c1c26;
    --border:#2a2a3a;
    --accent:#7f77dd;
    --accent2:#5dcaa5;
    --accent3:#ef9f27;
    --text:#f0effe;
    --muted:#888;
    --font-display:'Syne',sans-serif;
    --font-mono:'Space Mono',monospace;
  }
  body{background:var(--bg);color:var(--text);font-family:var(--font-display);min-height:100vh;overflow-x:hidden}
  
  .noise{position:fixed;inset:0;pointer-events:none;z-index:0;opacity:.03;background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E")}
  
  .grid-bg{position:fixed;inset:0;pointer-events:none;z-index:0;background-image:linear-gradient(var(--border) 1px,transparent 1px),linear-gradient(90deg,var(--border) 1px,transparent 1px);background-size:60px 60px;opacity:.3}
  
  .wrap{position:relative;z-index:1;max-width:860px;margin:0 auto;padding:2rem 1.5rem 4rem}
  
  /* HERO */
  .hero{padding:4rem 0 3rem;border-bottom:1px solid var(--border)}
  .hero-tag{font-family:var(--font-mono);font-size:11px;color:var(--accent2);letter-spacing:.15em;text-transform:uppercase;margin-bottom:1rem;display:flex;align-items:center;gap:.5rem}
  .hero-tag::before{content:'';display:inline-block;width:24px;height:1px;background:var(--accent2)}
  .hero h1{font-size:clamp(2.4rem,6vw,4.2rem);font-weight:800;line-height:1.05;letter-spacing:-.02em;margin-bottom:1rem}
  .hero h1 span{color:var(--accent);position:relative}
  .hero h1 span::after{content:'';position:absolute;bottom:2px;left:0;right:0;height:3px;background:var(--accent);opacity:.4;border-radius:2px}
  .hero-sub{font-size:1rem;color:var(--muted);max-width:480px;line-height:1.7;margin-bottom:2rem;font-family:var(--font-mono);font-size:13px}
  .hero-links{display:flex;gap:.75rem;flex-wrap:wrap}
  .btn{display:inline-flex;align-items:center;gap:.4rem;font-family:var(--font-mono);font-size:12px;padding:.5rem 1rem;border-radius:6px;text-decoration:none;transition:all .2s;cursor:pointer;border:none}
  .btn-primary{background:var(--accent);color:#fff}
  .btn-primary:hover{background:#9d96e8;transform:translateY(-1px)}
  .btn-outline{background:transparent;color:var(--text);border:1px solid var(--border)}
  .btn-outline:hover{border-color:var(--accent);color:var(--accent);transform:translateY(-1px)}
  .btn-green{background:transparent;color:var(--accent2);border:1px solid var(--accent2)}
  .btn-green:hover{background:var(--accent2);color:#000;transform:translateY(-1px)}
  
  /* SECTION */
  section{padding:3rem 0;border-bottom:1px solid var(--border)}
  .sec-label{font-family:var(--font-mono);font-size:11px;color:var(--muted);letter-spacing:.15em;text-transform:uppercase;margin-bottom:1.5rem;display:flex;align-items:center;gap:.5rem}
  .sec-label span{color:var(--accent);margin-right:.25rem}
  
  /* STACK */
  .stack-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(90px,1fr));gap:.6rem}
  .stack-item{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:.65rem .5rem;display:flex;flex-direction:column;align-items:center;gap:.4rem;transition:all .2s;cursor:default}
  .stack-item:hover{border-color:var(--accent);transform:translateY(-2px);background:var(--surface2)}
  .stack-item img{width:28px;height:28px;object-fit:contain;filter:brightness(.9)}
  .stack-item span{font-size:10px;color:var(--muted);font-family:var(--font-mono);text-align:center;letter-spacing:.03em}
  .stack-item:hover span{color:var(--text)}
  
  /* STATS */
  .stats-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:1rem}
  .stat-card{background:var(--surface);border:1px solid var(--border);border-radius:10px;overflow:hidden}
  .stat-card img{width:100%;display:block;filter:brightness(.85) saturate(.9)}
  .stat-card-label{font-family:var(--font-mono);font-size:11px;color:var(--muted);padding:.6rem .8rem;letter-spacing:.05em}
  
  /* SOCIAL */
  .social-row{display:flex;gap:1rem;flex-wrap:wrap}
  .soc-btn{display:inline-flex;align-items:center;gap:.5rem;font-family:var(--font-mono);font-size:12px;padding:.5rem 1.1rem;border-radius:6px;text-decoration:none;border:1px solid var(--border);color:var(--muted);transition:all .2s}
  .soc-btn:hover{transform:translateY(-2px)}
  .soc-btn.li:hover{border-color:#0a77b6;color:#0a77b6}
  .soc-btn.fb:hover{border-color:#0866ff;color:#0866ff}
  .soc-btn.ig:hover{border-color:#f35369;color:#f35369}
  .soc-icon{width:14px;height:14px}
  
  /* SNAKE */
  .snake-wrap{border:1px solid var(--border);border-radius:10px;overflow:hidden;background:var(--surface)}
  .snake-wrap img{width:100%;display:block;filter:brightness(.85) saturate(.8) hue-rotate(5deg)}
  
  /* FOOTER */
  .foot{padding-top:2rem;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:.5rem}
  .foot-l{font-family:var(--font-mono);font-size:11px;color:var(--muted)}
  .foot-l strong{color:var(--accent2)}
  
  /* BLOBS */
  .blob{position:fixed;border-radius:50%;filter:blur(80px);pointer-events:none;z-index:0}
  .blob1{width:400px;height:400px;background:rgba(127,119,221,.08);top:-100px;right:-100px}
  .blob2{width:300px;height:300px;background:rgba(93,202,165,.06);bottom:100px;left:-80px}
  
  @media(max-width:600px){.hero h1{font-size:2rem}.stats-grid{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="noise"></div>
<div class="grid-bg"></div>
<div class="blob blob1"></div>
<div class="blob blob2"></div>

<div class="wrap">

  <!-- HERO -->
  <div class="hero">
    <div class="hero-tag">available for opportunities</div>
    <h1>Jake<br><span>Mayores</span></h1>
    <p class="hero-sub">// Fullstack Developer &amp; Computer Science Student<br>Building products at the intersection of web, mobile, and data.</p>
    <div class="hero-links">
      <a class="btn btn-primary" href="https://ph.linkedin.com/in/jake-mayores" target="_blank">LinkedIn ↗</a>
      <a class="btn btn-green" href="https://github.com/Mayores-04" target="_blank">GitHub ↗</a>
      <a class="btn btn-outline" href="https://www.facebook.com/jakejmayores" target="_blank">Facebook</a>
      <a class="btn btn-outline" href="https://www.instagram.com/mayoresjake" target="_blank">Instagram</a>
    </div>
  </div>

  <!-- TECH STACK -->
  <section>
    <div class="sec-label"><span>01</span> tech stack</div>
    <div class="stack-grid" id="stack"></div>
  </section>

  <!-- GITHUB STATS -->
  <section>
    <div class="sec-label"><span>02</span> github stats</div>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=Mayores-04&show_icons=true&locale=en&theme=transparent&title_color=7f77dd&text_color=888&icon_color=5dcaa5&bg_color=00000000&border_color=2a2a3a" alt="GitHub stats" />
        <div class="stat-card-label">overview</div>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs?username=Mayores-04&locale=en&layout=compact&card_width=320&langs_count=5&theme=transparent&title_color=7f77dd&text_color=888&bg_color=00000000&border_color=2a2a3a" alt="Top languages" />
        <div class="stat-card-label">top languages</div>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=Mayores-04&theme=transparent&ring=7f77dd&fire=ef9f27&currStreakLabel=5dcaa5&sideNums=888&currStreakNum=f0effe&dates=888&sideLabels=888&border=2a2a3a" alt="Streak stats" />
        <div class="stat-card-label">contribution streak</div>
      </div>
      <div class="stat-card">
        <img src="https://github-profile-trophy.vercel.app/?username=Mayores-04&theme=onedark&no-frame=true&no-bg=true&margin-w=4&column=4" alt="Trophies" />
        <div class="stat-card-label">trophies</div>
      </div>
    </div>
  </section>

  <!-- CONTRIBUTIONS SNAKE -->
  <section>
    <div class="sec-label"><span>03</span> contribution graph</div>
    <div class="snake-wrap">
      <img src="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake-dark.svg" alt="GitHub contribution snake" />
    </div>
  </section>

  <!-- FIND ME -->
  <section style="border-bottom:none">
    <div class="sec-label"><span>04</span> find me</div>
    <div class="social-row">
      <a class="soc-btn li" href="https://ph.linkedin.com/in/jake-mayores" target="_blank">
        <svg class="soc-icon" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a class="soc-btn fb" href="https://www.facebook.com/jakejmayores" target="_blank">
        <svg class="soc-icon" viewBox="0 0 24 24" fill="currentColor"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
        Facebook
      </a>
      <a class="soc-btn ig" href="https://www.instagram.com/mayoresjake" target="_blank">
        <svg class="soc-icon" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>
        Instagram
      </a>
    </div>
  </section>

  <div class="foot">
    <span class="foot-l">Jake Mayores &mdash; <strong>Quezon City, PH</strong></span>
    <span class="foot-l" id="ts"></span>
  </div>
</div>

<script>
const stack=[
  {name:'JavaScript',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg'},
  {name:'TypeScript',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-original.svg'},
  {name:'Java',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg'},
  {name:'React',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg'},
  {name:'Next.js',icon:'https://cdn.worldvectorlogo.com/logos/nextjs-2.svg'},
  {name:'HTML5',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg'},
  {name:'CSS3',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg'},
  {name:'Tailwind',icon:'https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg'},
  {name:'React Native',icon:'https://reactnative.dev/img/header_logo.svg'},
  {name:'MongoDB',icon:'https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg'},
  {name:'SQL Server',icon:'https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg'},
  {name:'Firebase',icon:'https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg'},
  {name:'Git',icon:'https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg'},
  {name:'Figma',icon:'https://www.vectorlogo.zone/logos/figma/figma-icon.svg'},
  {name:'Postman',icon:'https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg'},
  {name:'Bash',icon:'https://www.vectorlogo.zone/logos/gnu_bash/gnu_bash-icon.svg'},
  {name:'Arduino',icon:'https://cdn.worldvectorlogo.com/logos/arduino-1.svg'},
];
const g=document.getElementById('stack');
stack.forEach(t=>{
  const d=document.createElement('div');
  d.className='stack-item';
  d.innerHTML=`<img src="${t.icon}" alt="${t.name}" loading="lazy"><span>${t.name}</span>`;
  g.appendChild(d);
});
document.getElementById('ts').textContent=new Date().toLocaleDateString('en-PH',{year:'numeric',month:'long'});
</script>
</body>
</html>
