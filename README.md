<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>成语奇妙之旅 · 三维动画毕业设计</title>
  <meta name="description" content="《成语奇妙之旅》——以邯郸成语为核心的三维动画短片，国风奇幻，文化传承。">
  <meta name="keywords" content="成语,邯郸,三维动画,毕业设计,国风,文化传承,胡服骑射">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;600;700;900&display=swap" rel="stylesheet">
  <style>
    :root {
      --ink: #1a1a2e;
      --paper: #f5f0e6;
      --gold: #c9a84c;
      --jade: #5b8c5a;
      --crimson: #b83b3b;
      --mist: rgba(245, 240, 230, 0.1);
      --shadow: rgba(0,0,0,0.3);
    }
    
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    html {
      scroll-behavior: smooth;
      font-size: 16px;
    }
    
    body {
      font-family: 'Noto Serif SC', serif;
      background: var(--ink);
      color: var(--paper);
      line-height: 1.7;
      overflow-x: hidden;
      -webkit-tap-highlight-color: transparent;
    }
    
    /* 移动端适配 */
    @media (max-width: 768px) {
      html {
        font-size: 14px;
      }
    }
    
    /* 水墨背景 */
    .ink-bg {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at 20% 30%, rgba(30,30,50,0.8), #0f0f1a);
      z-index: -2;
    }
    
    .ink-splash {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 1200"><path fill="rgba(150,130,100,0.03)" d="M0,0 L800,0 L800,1200 L0,1200 Z M200,300 Q250,250 300,280 Q350,310 320,360 Q290,410 240,400 Q190,390 200,340 Z M500,700 Q550,650 600,680 Q650,710 630,760 Q610,810 560,800 Q510,790 500,740 Z M350,900 Q400,850 450,880 Q500,910 480,960 Q460,1010 410,1000 Q360,990 350,940 Z"/></svg>');
      background-repeat: no-repeat;
      background-position: 10% 20%;
      background-size: 80%;
      opacity: 0.4;
      pointer-events: none;
      z-index: -1;
    }
    
    /* 导航栏 */
    nav {
      position: fixed;
      top: 0;
      width: 100%;
      background: rgba(26, 26, 46, 0.95);
      backdrop-filter: blur(12px);
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.8rem 1.5rem;
      z-index: 1000;
      border-bottom: 1px solid rgba(201, 168, 76, 0.3);
      box-shadow: 0 2px 10px rgba(0,0,0,0.3);
    }
    
    .logo {
      font-size: 1.2rem;
      font-weight: 700;
      color: var(--gold);
      letter-spacing: 2px;
      text-decoration: none;
      background: linear-gradient(135deg, var(--gold), #e6c88a);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    
    .nav-links {
      display: flex;
      gap: 1.5rem;
    }
    
    .nav-links a {
      color: var(--paper);
      text-decoration: none;
      font-size: 0.9rem;
      position: relative;
      padding: 0.5rem 0;
      transition: color 0.3s;
    }
    
    .nav-links a:hover {
      color: var(--gold);
    }
    
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 2px;
      background: var(--gold);
      transition: width 0.3s;
    }
    
    .nav-links a:hover::after {
      width: 100%;
    }
    
    /* 汉堡菜单 */
    .hamburger {
      display: none;
      flex-direction: column;
      cursor: pointer;
      width: 30px;
      height: 25px;
      justify-content: space-between;
    }
    
    .hamburger span {
      display: block;
      height: 3px;
      width: 100%;
      background: var(--gold);
      border-radius: 3px;
      transition: 0.3s;
    }
    
    .hamburger.active span:nth-child(1) {
      transform: rotate(45deg) translate(5px, 5px);
    }
    
    .hamburger.active span:nth-child(2) {
      opacity: 0;
    }
    
    .hamburger.active span:nth-child(3) {
      transform: rotate(-45deg) translate(7px, -6px);
    }
    
    @media (max-width: 768px) {
      .nav-links {
        position: fixed;
        top: 60px;
        left: 0;
        width: 100%;
        background: rgba(26, 26, 46, 0.98);
        backdrop-filter: blur(15px);
        flex-direction: column;
        align-items: center;
        padding: 1rem 0;
        gap: 0;
        transform: translateY(-100%);
        opacity: 0;
        visibility: hidden;
        transition: all 0.3s;
        z-index: 999;
      }
      
      .nav-links.active {
        transform: translateY(0);
        opacity: 1;
        visibility: visible;
      }
      
      .nav-links a {
        width: 100%;
        text-align: center;
        padding: 1rem;
        border-bottom: 1px solid rgba(201,168,76,0.1);
      }
      
      .hamburger {
        display: flex;
      }
    }
    
    /* 标题区域 */
    header {
      height: 100vh;
      min-height: 600px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      position: relative;
      padding: 0 1rem;
    }
    
    .header-decoration {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at 30% 40%, rgba(201,168,76,0.08), transparent 70%);
      pointer-events: none;
    }
    
    .header-content {
      position: relative;
      z-index: 2;
      animation: fadeInUp 1.2s ease-out;
    }
    
    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(30px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    header h1 {
      font-size: clamp(2.2rem, 8vw, 4rem);
      letter-spacing: 0.1em;
      margin-bottom: 1rem;
      background: linear-gradient(135deg, var(--gold), #fff3cf);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }
    
    .subtitle {
      font-size: clamp(1rem, 4vw, 1.4rem);
      opacity: 0.9;
      margin-bottom: 0.5rem;
      font-weight: 300;
      letter-spacing: 2px;
    }
    
    .chop-seal {
      display: inline-block;
      border: 1px solid var(--crimson);
      color: var(--crimson);
      padding: 0.2rem 1rem;
      font-size: 0.8rem;
      margin-top: 1rem;
      font-family: monospace;
      letter-spacing: 1px;
      background: rgba(184, 59, 59, 0.1);
    }
    
    .scroll-indicator {
      position: absolute;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      color: var(--gold);
      font-size: 1.5rem;
      animation: bounce 2s infinite;
      cursor: pointer;
      background: rgba(0,0,0,0.3);
      width: 40px;
      height: 40px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      border: 1px solid rgba(201,168,76,0.4);
      transition: 0.3s;
    }
    
    @keyframes bounce {
      0%,100%{ transform: translateY(0) translateX(-50%); }
      50%{ transform: translateY(-10px) translateX(-50%); }
    }
    
    /* 主体内容 */
    section {
      max-width: 1200px;
      margin: 0 auto;
      padding: 4rem 1.5rem;
      position: relative;
    }
    
    @media (min-width: 768px) {
      section {
        padding: 6rem 2rem;
      }
    }
    
    section h2 {
      font-size: clamp(1.5rem, 5vw, 2.2rem);
      border-left: 4px solid var(--gold);
      padding-left: 1rem;
      margin-bottom: 2rem;
      display: inline-block;
    }
    
    .section-intro {
      font-size: 1rem;
      line-height: 1.8;
      margin-bottom: 2rem;
      text-align: justify;
    }
    
    /* 角色与场景卡片 */
    .grid-2col {
      display: grid;
      grid-template-columns: 1fr;
      gap: 2rem;
      margin-top: 2rem;
    }
    
    @media (min-width: 768px) {
      .grid-2col {
        grid-template-columns: repeat(2, 1fr);
      }
    }
    
    .info-card {
      background: rgba(245,240,230,0.05);
      border-radius: 16px;
      padding: 1.5rem;
      border: 1px solid rgba(201,168,76,0.2);
      transition: transform 0.3s, box-shadow 0.3s;
    }
    
    .info-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 15px 30px rgba(0,0,0,0.3);
      border-color: rgba(201,168,76,0.4);
    }
    
    .info-card h3 {
      color: var(--gold);
      margin-bottom: 1rem;
      font-size: 1.3rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    
    .info-card p {
      font-size: 0.95rem;
      line-height: 1.6;
      opacity: 0.9;
    }
    
    /* 分幕剧情时间线 */
    .timeline {
      position: relative;
      padding-left: 2rem;
      margin: 2rem 0;
    }
    
    .timeline::before {
      content: '';
      position: absolute;
      left: 8px;
      top: 0;
      bottom: 0;
      width: 2px;
      background: linear-gradient(to bottom, var(--gold), var(--jade));
    }
    
    .scene {
      margin-bottom: 2rem;
      position: relative;
      padding-left: 1.5rem;
    }
    
    .scene-marker {
      position: absolute;
      left: -1.8rem;
      top: 0.2rem;
      width: 12px;
      height: 12px;
      background: var(--gold);
      border-radius: 50%;
      border: 2px solid var(--ink);
    }
    
    .scene-title {
      font-weight: bold;
      color: var(--gold);
      margin-bottom: 0.5rem;
      font-size: 1.1rem;
    }
    
    .scene-desc {
      font-size: 0.9rem;
      opacity: 0.85;
      line-height: 1.6;
    }
    
    .dialogue {
      background: rgba(0,0,0,0.3);
      border-left: 3px solid var(--crimson);
      padding: 0.8rem 1rem;
      margin: 0.8rem 0;
      font-style: italic;
      font-size: 0.9rem;
      color: #e0d6c8;
    }
    
    /* 视频区域 */
    .video-container {
      margin: 2rem 0;
      background: rgba(0,0,0,0.4);
      border-radius: 16px;
      overflow: hidden;
      border: 1px solid rgba(201,168,76,0.3);
    }
    
    .video-header {
      background: rgba(26,26,46,0.8);
      padding: 1rem;
      border-bottom: 1px solid rgba(201,168,76,0.2);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    
    .video-title {
      color: var(--gold);
      display: flex;
      align-items: center;
      gap: 8px;
    }
    
    .video-controls {
      display: flex;
      gap: 0.8rem;
    }
    
    .video-controls i {
      cursor: pointer;
      width: 35px;
      height: 35px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 50%;
      background: rgba(255,255,255,0.1);
      transition: 0.3s;
    }
    
    .video-controls i:hover {
      background: var(--gold);
      color: var(--ink);
    }
    
    .video-box {
      padding: 1rem;
    }
    
    .video-player {
      width: 100%;
      border-radius: 12px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.4);
    }
    
    .video-info {
      margin-top: 1rem;
      background: rgba(0,0,0,0.3);
      padding: 1rem;
      border-radius: 12px;
      font-size: 0.9rem;
      border-left: 3px solid var(--jade);
    }
    
    /* 成语卡片 */
    .idiom-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }
    
    .idiom-card {
      background: linear-gradient(145deg, #1e1e2e, #161622);
      border-radius: 12px;
      padding: 1.5rem;
      text-align: center;
      transition: all 0.3s;
      border: 1px solid rgba(201,168,76,0.2);
    }
    
    .idiom-card:hover {
      transform: translateY(-8px);
      border-color: var(--gold);
    }
    
    .idiom-name {
      font-size: 1.5rem;
      color: var(--gold);
      margin-bottom: 0.8rem;
      font-weight: bold;
    }
    
    .idiom-char {
      font-size: 2rem;
      letter-spacing: 0.3rem;
      color: var(--jade);
      margin-bottom: 0.5rem;
    }
    
    .idiom-desc {
      font-size: 0.85rem;
      opacity: 0.8;
    }
    
    /* 结尾字幕 */
    .ending-quote {
      background: rgba(0,0,0,0.5);
      border-radius: 20px;
      padding: 2rem;
      text-align: center;
      margin: 3rem 0;
      border: 1px solid var(--gold);
    }
    
    .ending-quote p {
      font-size: 1.2rem;
      line-height: 1.8;
    }
    
    .slogan {
      margin-top: 1rem;
      font-size: 1rem;
      color: var(--gold);
      letter-spacing: 2px;
    }
    
    /* 返回顶部 */
    .back-to-top {
      position: fixed;
      bottom: 20px;
      right: 20px;
      width: 45px;
      height: 45px;
      background: rgba(201,168,76,0.2);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--gold);
      cursor: pointer;
      opacity: 0;
      visibility: hidden;
      transition: 0.3s;
      border: 1px solid var(--gold);
      z-index: 999;
    }
    
    .back-to-top.show {
      opacity: 0.8;
      visibility: visible;
    }
    
    /* 页脚 */
    footer {
      text-align: center;
      padding: 3rem 1rem;
      background: rgba(0,0,0,0.6);
      border-top: 1px solid rgba(201,168,76,0.2);
      font-size: 0.8rem;
    }
    
    /* 加载动画 */
    .loading {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: var(--ink);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
      transition: opacity 0.5s;
    }
    
    .loading.hidden {
      opacity: 0;
      pointer-events: none;
    }
    
    .brush-spinner {
      width: 60px;
      height: 60px;
      border: 3px solid rgba(201,168,76,0.3);
      border-top-color: var(--gold);
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }
    
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
  </style>
</head>
<body>
  <div class="ink-bg"></div>
  <div class="ink-splash"></div>
  
  <div class="loading" id="loading">
    <div class="brush-spinner"></div>
  </div>
  
  <nav>
    <a href="#" class="logo">成语奇妙之旅</a>
    <div class="nav-links" id="navLinks">
      <a href="#intro">项目概述</a>
      <a href="#animation">动画展示</a>
      <a href="#synopsis">剧情介绍</a>
      <a href="#characters">角色设定</a>
      <a href="#idioms">成语故事</a>
      <a href="#info">影片信息</a>
    </div>
    <div class="hamburger" id="hamburger">
      <span></span><span></span><span></span>
    </div>
  </nav>
  
  <header>
    <div class="header-decoration"></div>
    <div class="header-content">
      <h1>成语奇妙之旅</h1>
      <div class="subtitle">—— 一场穿越邯郸成语世界的奇幻之旅</div>
      <div class="chop-seal">文化传承 · 国风动画</div>
    </div>
    <div class="scroll-indicator" onclick="scrollToSection('intro')">
      <i class="fas fa-chevron-down"></i>
    </div>
  </header>
  
  <!-- 项目概述 -->
  <section id="intro">
    <h2>项目概述</h2>
    <div class="section-intro">
      <p><strong class="highlight" style="color:var(--gold);">《成语奇妙之旅》</strong> 是一部以邯郸成语为核心的三维动画短片，时长约3分钟。影片通过现代青年“小郸”的奇幻视角，带领观众走进成语诞生的历史瞬间，体验“邯郸学步”“完璧归赵”“负荆请罪”“胡服骑射”等经典成语背后的智慧与情感。作品融合国风美学、光影写意与现代动画技术，旨在以青少年喜爱的方式传承中华优秀传统文化。</p>
    </div>
    
    <div class="grid-2col">
      <div class="info-card">
        <h3><i class="fas fa-film"></i> 影片类型</h3>
        <p>文化传承 / 奇幻国风动画短片</p>
        <p>风格：国风3D动画 · 偏写意 · 光影表达</p>
        <p>时长：约3分钟</p>
      </div>
      <div class="info-card">
        <h3><i class="fas fa-bullseye"></i> 主题定位</h3>
        <p>以“邯郸成语”为核心，展现成语背后的历史智慧与现实启示。受众定位为青少年及大众观众，让传统文化在数字时代焕发新生。</p>
      </div>
    </div>
  </section>
  
  <!-- 动画展示 -->
  <section id="animation">
    <h2>动画展示</h2>
    <div class="video-container">
      <div class="video-header">
        <div class="video-title"><i class="fas fa-feather-alt"></i> 《成语奇妙之旅》完整动画</div>
        <div class="video-controls">
          <i class="fas fa-expand" onclick="toggleFullscreen()"></i>
          <i class="fas fa-volume-up" onclick="toggleMute()"></i>
          <i class="fas fa-play" onclick="togglePlay()"></i>
        </div>
      </div>
      <div class="video-box">
        <video id="mainVideo" class="video-player" controls playsinline webkit-playsinline poster="cover.jpg" preload="metadata">
          <source src="成语奇妙之旅.mp4" type="video/mp4">
          您的浏览器不支持视频播放，请升级浏览器。
        </video>
        <div class="video-info">
          <p><strong>叙事结构：</strong>现实伏笔 → 进入成语世界 → 四大成语体验 → 回归现实升华</p>
          <p><strong>技术特点：</strong>三维建模 · 国风水墨渲染 · 光影虚像 · 邯郸丛台场景复原</p>
        </div>
      </div>
    </div>
  </section>
  
  <!-- 剧情介绍（分幕） -->
  <section id="synopsis">
    <h2>剧情介绍</h2>
    <div class="timeline">
      <div class="scene">
        <div class="scene-marker"></div>
        <div class="scene-title">第一幕 · 现实伏笔 (0:00-0:35)</div>
        <div class="scene-desc">清晨书房，小郸沉浸于《邯郸成语故事》。妈妈催促吃饭，他仍不舍放下书本。书页上的“邯郸学步”微微泛光。</div>
      </div>
      <div class="scene">
        <div class="scene-marker"></div>
        <div class="scene-title">第二幕 · 进入成语世界 (0:36-1:30)</div>
        <div class="scene-desc">成语精灵从书中跃出，邀请小郸亲眼见证成语诞生的世界。书房瓦解，小郸被卷入光影流转的成语世界——邯郸丛台，文字悬浮。</div>
      </div>
      <div class="scene">
        <div class="scene-marker"></div>
        <div class="scene-title">第三幕 · 成语体验与成长 (1:30-2:50)</div>
        <div class="scene-desc">
          <strong>邯郸学步：</strong>少年模仿他人而忘记自己的步伐，小郸领悟“学不能忘本”。<br>
          <strong>完璧归赵：</strong>蔺相如持璧智斗秦王，小郸感悟“勇气与智慧并存”。<br>
          <strong>负荆请罪：</strong>廉颇负荆忏悔，小郸懂得“知错能改，比逞强更难”。<br>
          <strong>胡服骑射：</strong>赵武灵王推行胡服骑射改革，小郸理解“变革图强，不拘旧制”。
        </div>
      </div>
      <div class="scene">
        <div class="scene-marker"></div>
        <div class="scene-title">第四幕 · 回归现实与升华 (2:50-3:10)</div>
        <div class="scene-desc">成语精灵告别，小郸从梦中醒来。书页上的成语仿佛多了一层重量，邯郸城的夜色中，字幕浮现：“成语，不只是文字。它们诞生于邯郸，也指引着今天的我们。”</div>
      </div>
    </div>
  </section>
  
  <!-- 角色设定 -->
  <section id="characters">
    <h2>角色设定</h2>
    <div class="grid-2col">
      <div class="info-card">
        <h3><i class="fas fa-user"></i> 小郸</h3>
        <p><strong>年龄：</strong>22岁<br>
        <strong>身份：</strong>邯郸本地青年，成语爱好者<br>
        <strong>性格弧线：</strong>从“知道成语”到“理解成语”，最终将成语智慧与现实人生相连。</p>
      </div>
      <div class="info-card">
        <h3><i class="fas fa-magic"></i> 成语精灵</h3>
        <p>小巧灵动的半透明光影形态，作为引导者与提问者，不直接讲解结论，而是引导小郸自行领悟。</p>
      </div>
      <div class="info-card">
        <h3><i class="fas fa-user-friends"></i> 成语虚影人物</h3>
        <p>模仿少年（邯郸学步）、蔺相如（完璧归赵）、廉颇（负荆请罪）、赵武灵王（胡服骑射）。均为光影虚像，随成语显现消散。</p>
      </div>
      <div class="info-card">
        <h3><i class="fas fa-tree"></i> 场景</h3>
        <p>现实书房（现代、安静）与成语世界（邯郸丛台，成语文字悬浮），国风水墨风格。</p>
      </div>
    </div>
  </section>
  
  <!-- 核心成语故事 -->
  <section id="idioms">
    <h2>核心成语故事</h2>
    <div class="idiom-grid">
      <div class="idiom-card">
        <div class="idiom-name">邯郸学步</div>
        <div class="idiom-char">邯郸学步</div>
        <div class="idiom-desc">模仿他人不成，反失自己原有本领。启示：学习不能盲目，要保留自己的根基。</div>
      </div>
      <div class="idiom-card">
        <div class="idiom-name">完璧归赵</div>
        <div class="idiom-char">完璧归赵</div>
        <div class="idiom-desc">蔺相如凭借智慧与勇气，将和氏璧完好带回赵国。启示：智勇双全方能成事。</div>
      </div>
      <div class="idiom-card">
        <div class="idiom-name">负荆请罪</div>
        <div class="idiom-char">负荆请罪</div>
        <div class="idiom-desc">廉颇知错能改，向蔺相如请罪。启示：勇于认错，比坚持错误更需要勇气。</div>
      </div>
      <div class="idiom-card">
        <div class="idiom-name">胡服骑射</div>
        <div class="idiom-char">胡服骑射</div>
        <div class="idiom-desc">赵武灵王推行胡服骑射改革，使赵国强盛。启示：变革图强，不拘旧制，勇于创新。</div>
      </div>
    </div>
  </section>
  
  <!-- 影片信息与结尾 -->
  <section id="info">
    <h2>影片信息</h2>
    <div class="ending-quote">
      <p>“成语，不只是文字。它们诞生于邯郸，也指引着今天的我们。”</p>
      <div class="slogan">这么近那么美，周末到河北 · 玩水游山，快来邯郸</div>
    </div>
    <div class="info-card" style="text-align:center;">
      <p><strong>指导老师：</strong>李勇 &nbsp;|&nbsp; <strong>动画制作：</strong>22级动画2班 刘海鑫</p>
      <p>© 2026 美术与设计学院 毕业设计展</p>
    </div>
  </section>
  
  <div class="back-to-top" id="backToTop">
    <i class="fas fa-chevron-up"></i>
  </div>
  
  <footer>
    <p>《成语奇妙之旅》毕业设计展示网站</p>
    <p>参考典籍：《邯郸成语故事》｜ 河北博物院 ｜ 邯郸文化研究院</p>
    <p>本网站托管于 GitHub Pages</p>
  </footer>
  
  <script>
    // 加载动画
    window.addEventListener('load', function() {
      const loading = document.getElementById('loading');
      setTimeout(() => {
        loading.classList.add('hidden');
        setTimeout(() => loading.style.display = 'none', 500);
      }, 800);
    });
    
    // 移动端菜单
    const hamburger = document.getElementById('hamburger');
    const navLinks = document.getElementById('navLinks');
    hamburger.addEventListener('click', () => {
      hamburger.classList.toggle('active');
      navLinks.classList.toggle('active');
    });
    document.querySelectorAll('.nav-links a').forEach(link => {
      link.addEventListener('click', () => {
        hamburger.classList.remove('active');
        navLinks.classList.remove('active');
      });
    });
    document.addEventListener('click', (e) => {
      if (!e.target.closest('nav') && navLinks.classList.contains('active')) {
        hamburger.classList.remove('active');
        navLinks.classList.remove('active');
      }
    });
    
    // 平滑滚动
    function scrollToSection(id) {
      const el = document.getElementById(id);
      if (el) window.scrollTo({ top: el.offsetTop - 70, behavior: 'smooth' });
    }
    document.querySelectorAll('.nav-links a, .scroll-indicator').forEach(link => {
      link.addEventListener('click', function(e) {
        if (this.getAttribute('onclick')) return;
        e.preventDefault();
        const href = this.getAttribute('href');
        if (href && href.startsWith('#')) scrollToSection(href.slice(1));
      });
    });
    
    // 返回顶部
    const backBtn = document.getElementById('backToTop');
    window.addEventListener('scroll', () => {
      if (window.scrollY > 500) backBtn.classList.add('show');
      else backBtn.classList.remove('show');
    });
    backBtn.addEventListener('click', () => window.scrollTo({ top: 0, behavior: 'smooth' }));
    
    // 视频控制
    const video = document.getElementById('mainVideo');
    function toggleFullscreen() { if (video.requestFullscreen) video.requestFullscreen(); }
    function toggleMute() {
      video.muted = !video.muted;
      const icon = document.querySelector('.fa-volume-up');
      if (video.muted) {
        icon.classList.remove('fa-volume-up');
        icon.classList.add('fa-volume-mute');
      } else {
        icon.classList.remove('fa-volume-mute');
        icon.classList.add('fa-volume-up');
      }
    }
    function togglePlay() {
      if (video.paused) video.play();
      else video.pause();
      const playIcon = document.querySelector('.fa-play');
      if (video.paused) {
        playIcon.classList.remove('fa-pause');
        playIcon.classList.add('fa-play');
      } else {
        playIcon.classList.remove('fa-play');
        playIcon.classList.add('fa-pause');
      }
    }
    video.addEventListener('play', () => {
      document.querySelector('.fa-play').classList.remove('fa-play');
      document.querySelector('.fa-play').classList.add('fa-pause');
    });
    video.addEventListener('pause', () => {
      document.querySelector('.fa-pause').classList.remove('fa-pause');
      document.querySelector('.fa-pause').classList.add('fa-play');
    });
    
    // 简单提示（若视频文件不存在）
    video.addEventListener('error', () => {
      console.log('视频文件未找到，请将“成语奇妙之旅.mp4”放入同一目录');
    });
  </script>
</body>
</html>
