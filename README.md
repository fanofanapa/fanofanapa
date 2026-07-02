<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Tech Ecosystem Graph</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  
  body {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: radial-gradient(ellipse at top, #1a1a2e 0%, #0f0f1e 50%, #050510 100%);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    padding: 20px;
  }
  
  .container {
    position: relative;
    width: 100%;
    max-width: 1400px;
  }
  
  .title {
    text-align: center;
    margin-bottom: 10px;
    font-size: 32px;
    font-weight: 700;
    background: linear-gradient(135deg, #00d4ff 0%, #b967ff 50%, #ff6bcb 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    letter-spacing: -0.5px;
  }
  
  .subtitle {
    text-align: center;
    color: #8a8aa3;
    font-size: 14px;
    margin-bottom: 40px;
  }
  
  .graph-wrapper {
    position: relative;
    background: rgba(20, 20, 35, 0.4);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 24px;
    padding: 30px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
  }
  
  .graph {
    position: relative;
    width: 100%;
    height: 560px;
    overflow: visible;
  }
  
  .graph svg {
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
  }
  
  .edge {
    fill: none;
    stroke-width: 2;
    stroke-linecap: round;
    opacity: 0;
    animation: drawLine 1.2s ease-out forwards;
  }
  
  .edge-glow {
    fill: none;
    stroke-width: 8;
    stroke-linecap: round;
    opacity: 0;
    filter: blur(4px);
    animation: drawLine 1.2s ease-out forwards;
  }
  
  @keyframes drawLine {
    from { stroke-dasharray: 1000; stroke-dashoffset: 1000; opacity: 0; }
    to   { stroke-dasharray: 1000; stroke-dashoffset: 0;    opacity: 0.8; }
  }
  
  .node {
    position: absolute;
    background: linear-gradient(135deg, rgba(40, 40, 60, 0.7) 0%, rgba(25, 25, 45, 0.7) 100%);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    padding: 16px 20px;
    min-width: 200px;
    opacity: 0;
    transform: translateY(10px) scale(0.95);
    animation: nodeAppear 0.6s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
    cursor: pointer;
    z-index: 2;
  }
  
  .node::before {
    content: '';
    position: absolute;
    inset: 0;
    border-radius: 16px;
    padding: 1px;
    background: linear-gradient(135deg, var(--accent) 0%, transparent 60%);
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    -webkit-mask-composite: xor;
            mask-composite: exclude;
    pointer-events: none;
    opacity: 0.6;
  }
  
  .node:hover {
    transform: translateY(-4px) scale(1.02);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3), 0 0 30px var(--accent-dim);
    border-color: var(--accent);
  }
  
  .node:hover::before { opacity: 1; }
  
  @keyframes nodeAppear {
    to { opacity: 1; transform: translateY(0) scale(1); }
  }
  
  .node-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 12px;
    padding-bottom: 10px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  }
  
  .node-icon {
    width: 32px; height: 32px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    font-weight: 700;
    color: #fff;
    background: linear-gradient(135deg, var(--accent), var(--accent-dim));
    box-shadow: 0 4px 12px var(--accent-dim);
  }
  
  .node-title {
    font-size: 16px;
    font-weight: 600;
    letter-spacing: -0.2px;
    color: #fff;
  }
  
  .node-items {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }
  
  .node-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12.5px;
    color: #a8a8c0;
    font-weight: 400;
  }
  
  .node-item::before {
    content: '';
    width: 5px; height: 5px;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 8px var(--accent);
  }
  
  .node-python { --accent: #3776ab; --accent-dim: rgba(55, 118, 171, 0.3); }
  .node-web    { --accent: #10b981; --accent-dim: rgba(16, 185, 129, 0.3); }
  .node-data   { --accent: #f59e0b; --accent-dim: rgba(245, 158, 11, 0.3); }
  .node-ml     { --accent: #b967ff; --accent-dim: rgba(185, 103, 255, 0.3); }
  .node-dl     { --accent: #ff6bcb; --accent-dim: rgba(255, 107, 203, 0.3); }
  .node-api    { --accent: #00d4ff; --accent-dim: rgba(0, 212, 255, 0.3); }
  
  .legend {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 24px;
    flex-wrap: wrap;
  }
  
  .legend-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    color: #8a8aa3;
  }
  
  .legend-dot {
    width: 10px; height: 10px;
    border-radius: 50%;
    box-shadow: 0 0 6px currentColor;
  }
  
  .particle {
    position: absolute;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.15);
    pointer-events: none;
    animation: float 10s infinite ease-in-out;
  }
  
  @keyframes float {
    0%, 100% { transform: translateY(0) translateX(0); }
    50%      { transform: translateY(-20px) translateX(10px); }
  }
</style>
</head>
<body>

<div class="container">
  <h1 class="title">Python Technology Ecosystem</h1>
  <p class="subtitle">Interactive visualization of technologies and their relationships</p>
  
  <div class="graph-wrapper">
    <div class="graph" id="graph">
      <svg id="edges-svg" viewBox="0 0 1400 560" preserveAspectRatio="xMidYMid meet">
        <defs>
          <marker id="arrow-green"  viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#10b981"/></marker>
          <marker id="arrow-orange" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#f59e0b"/></marker>
          <marker id="arrow-blue"   viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00d4ff"/></marker>
          <marker id="arrow-purple" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#b967ff"/></marker>
          <marker id="arrow-pink"   viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#ff6bcb"/></marker>
        </defs>
      </svg>
      
      <div class="node node-python" style="left: 40px; top: 240px; animation-delay: 0s;">
        <div class="node-header">
          <div class="node-icon">Py</div>
          <div class="node-title">Python</div>
        </div>
        <div class="node-items">
          <div class="node-item">Core Language</div>
          <div class="node-item">Standard Library</div>
          <div class="node-item">Type System</div>
        </div>
      </div>
      
      <div class="node node-web" style="left: 380px; top: 80px; animation-delay: 0.3s;">
        <div class="node-header">
          <div class="node-icon">⚡</div>
          <div class="node-title">Web Development</div>
        </div>
        <div class="node-items">
          <div class="node-item">Django</div>
          <div class="node-item">Flask</div>
          <div class="node-item">FastAPI</div>
          <div class="node-item">SQLAlchemy</div>
        </div>
      </div>
      
      <div class="node node-api" style="left: 720px; top: 20px; animation-delay: 0.6s;">
        <div class="node-header">
          <div class="node-icon">🌐</div>
          <div class="node-title">API Services</div>
        </div>
        <div class="node-items">
          <div class="node-item">REST APIs</div>
          <div class="node-item">GraphQL</div>
          <div class="node-item">WebSockets</div>
        </div>
      </div>
      
      <div class="node node-api" style="left: 720px; top: 180px; animation-delay: 0.6s;">
        <div class="node-header">
          <div class="node-icon">🎨</div>
          <div class="node-title">Full-Stack</div>
        </div>
        <div class="node-items">
          <div class="node-item">HTMX</div>
          <div class="node-item">Jinja2</div>
          <div class="node-item">TailwindCSS</div>
        </div>
      </div>
      
      <div class="node node-data" style="left: 380px; top: 360px; animation-delay: 0.3s;">
        <div class="node-header">
          <div class="node-icon">📊</div>
          <div class="node-title">Data Science</div>
        </div>
        <div class="node-items">
          <div class="node-item">NumPy</div>
          <div class="node-item">Pandas</div>
          <div class="node-item">Matplotlib</div>
          <div class="node-item">Jupyter</div>
        </div>
      </div>
      
      <div class="node node-ml" style="left: 720px; top: 330px; animation-delay: 0.6s;">
        <div class="node-header">
          <div class="node-icon">🧠</div>
          <div class="node-title">Machine Learning</div>
        </div>
        <div class="node-items">
          <div class="node-item">scikit-learn</div>
          <div class="node-item">XGBoost</div>
          <div class="node-item">LightGBM</div>
        </div>
      </div>
      
      <div class="node node-dl" style="left: 1060px; top: 300px; animation-delay: 0.9s;">
        <div class="node-header">
          <div class="node-icon">🔥</div>
          <div class="node-title">Deep Learning</div>
        </div>
        <div class="node-items">
          <div class="node-item">PyTorch</div>
          <div class="node-item">TensorFlow</div>
          <div class="node-item">Keras</div>
          <div class="node-item">JAX</div>
        </div>
      </div>
      
      <div class="node node-dl" style="left: 1060px; top: 460px; animation-delay: 0.9s;">
        <div class="node-header">
          <div class="node-icon">⚙️</div>
          <div class="node-title">MLOps</div>
        </div>
        <div class="node-items">
          <div class="node-item">MLflow</div>
          <div class="node-item">Weights & Biases</div>
          <div class="node-item">Kubeflow</div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="legend">
    <div class="legend-item"><div class="legend-dot" style="background: #3776ab; color: #3776ab;"></div>Core</div>
    <div class="legend-item"><div class="legend-dot" style="background: #10b981; color: #10b981;"></div>Web</div>
    <div class="legend-item"><div class="legend-dot" style="background: #f59e0b; color: #f59e0b;"></div>Data</div>
    <div class="legend-item"><div class="legend-dot" style="background: #b967ff; color: #b967ff;"></div>ML</div>
    <div class="legend-item"><div class="legend-dot" style="background: #ff6bcb; color: #ff6bcb;"></div>Deep Learning</div>
    <div class="legend-item"><div class="legend-dot" style="background: #00d4ff; color: #00d4ff;"></div>Stack</div>
  </div>
</div>

<script>
  const nodes = [
    { id: 'python', left: 40,   top: 240, w: 200, h: 130 },
    { id: 'web',    left: 380,  top: 80,  w: 200, h: 150 },
    { id: 'api',    left: 720,  top: 20,  w: 200, h: 130 },
    { id: 'stack',  left: 720,  top: 180, w: 200, h: 130 },
    { id: 'data',   left: 380,  top: 360, w: 200, h: 150 },
    { id: 'ml',     left: 720,  top: 330, w: 200, h: 130 },
    { id: 'dl',     left: 1060, top: 300, w: 200, h: 150 },
    { id: 'mlops',  left: 1060, top: 460, w: 200, h: 130 },
  ];
  
  const edges = [
    { from: 'python', to: 'web',   delay: 0.3, color: '#10b981', marker: 'arrow-green'  },
    { from: 'python', to: 'data',  delay: 0.3, color: '#f59e0b', marker: 'arrow-orange' },
    { from: 'web',    to: 'api',   delay: 0.6, color: '#00d4ff', marker: 'arrow-blue'   },
    { from: 'web',    to: 'stack', delay: 0.6, color: '#00d4ff', marker: 'arrow-blue'   },
    { from: 'data',   to: 'ml',    delay: 0.6, color: '#b967ff', marker: 'arrow-purple' },
    { from: 'ml',     to: 'dl',    delay: 0.9, color: '#ff6bcb', marker: 'arrow-pink'   },
    { from: 'ml',     to: 'mlops', delay: 0.9, color: '#ff6bcb', marker: 'arrow-pink'   },
  ];
  
  const svg = document.getElementById('edges-svg');
  const svgNS = 'http://www.w3.org/2000/svg';
  
  edges.forEach(edge => {
    const fromNode = nodes.find(n => n.id === edge.from);
    const toNode   = nodes.find(n => n.id === edge.to);
    
    const start = { x: fromNode.left + fromNode.w,    y: fromNode.top + fromNode.h / 2 };
    const end   = { x: toNode.left,                   y: toNode.top   + toNode.h   / 2 };
    const midX  = (start.x + end.x) / 2;
    const pathData = `M ${start.x} ${start.y} C ${midX} ${start.y}, ${midX} ${end.y}, ${end.x} ${end.y}`;
    
    const glow = document.createElementNS(svgNS, 'path');
    glow.setAttribute('d', pathData);
    glow.setAttribute('class', 'edge-glow');
    glow.setAttribute('stroke', edge.color);
    glow.style.animationDelay = edge.delay + 's';
    svg.appendChild(glow);
    
    const path = document.createElementNS(svgNS, 'path');
    path.setAttribute('d', pathData);
    path.setAttribute('class', 'edge');
    path.setAttribute('stroke', edge.color);
    path.setAttribute('marker-end', `url(#${edge.marker})`);
    path.style.animationDelay = edge.delay + 's';
    svg.appendChild(path);
  });
  
  // Частицы фона
  for (let i = 0; i < 40; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    const size = Math.random() * 3 + 1;
    p.style.width  = size + 'px';
    p.style.height = size + 'px';
    p.style.left = Math.random() * 100 + '%';
    p.style.top  = Math.random() * 100 + '%';
    p.style.opacity = Math.random() * 0.5;
    p.style.animationDelay = Math.random() * 10 + 's';
    p.style.animationDuration = (Math.random() * 8 + 6) + 's';
    document.body.appendChild(p);
  }
</script>

</body>
</html>

[![GitHub Streak](https://streak-stats.demolab.com/?user=fanofanapa)](https://git.io/streak-stats)

