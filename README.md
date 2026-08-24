# birthday-wishes-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1, user-scalable=no" />
<title>A Surprise for Srushti 🌸</title>

<!-- Lightweight Google Fonts (display + body) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,500;0,600;0,700;1,600&family=Quicksand:wght@400;500;600;700&display=swap" rel="stylesheet">

<style>
/* ==========================================================================
   1. CSS CUSTOM PROPERTIES  (theme colors are pushed here at runtime by JS
      from CONFIG.theme, but sensible defaults live here too)
   ========================================================================== */
:root{
  --bg-deep:      #0a0618;
  --bg-mid:       #170b33;
  --bg-glow:      #2c1052;
  --accent-pink:  #ff6fa5;
  --accent-gold:  #ffd88a;
  --accent-violet:#a685ff;
  --text-soft:    #efe6ff;
  --text-dim:     #b9a9e0;
  --glass:        rgba(255,255,255,0.06);
  --glass-border: rgba(255,255,255,0.14);
  --shadow-glow:  0 0 40px rgba(255,111,165,0.35);

  --font-display: 'Cormorant Garamond', serif;
  --font-body:    'Quicksand', sans-serif;
}

*{ box-sizing:border-box; margin:0; padding:0; -webkit-tap-highlight-color:transparent; }

html,body{
  height:100%;
  overflow:hidden; /* the surprise plays screen-by-screen, not by scrolling */
  background:var(--bg-deep);
  color:var(--text-soft);
  font-family:var(--font-body);
  touch-action: manipulation;
}

body{ position:relative; }

button{
  font-family:var(--font-body);
  cursor:pointer;
  border:none;
  outline:none;
  background:none;
  color:inherit;
}
button:focus-visible, a:focus-visible{
  outline:2px solid var(--accent-gold);
  outline-offset:3px;
}

img{ max-width:100%; display:block; }

/* ==========================================================================
   2. BACKGROUND LAYERS — night sky canvas + soft aurora glow
   ========================================================================== */
#bg-glow{
  position:fixed; inset:0; z-index:0; pointer-events:none;
  background:
    radial-gradient(circle at 18% 12%, rgba(166,133,255,0.20), transparent 45%),
    radial-gradient(circle at 82% 78%, rgba(255,111,165,0.18), transparent 50%),
    linear-gradient(160deg, var(--bg-deep) 0%, var(--bg-mid) 55%, var(--bg-glow) 100%);
  transition: filter 1.2s ease, opacity 1.2s ease;
}
body.lit #bg-glow{ filter:saturate(1.35) brightness(1.15); }

#star-canvas{ position:fixed; inset:0; z-index:1; pointer-events:none; }

/* ==========================================================================
   3. SIGNATURE ELEMENT — the fairy-light garland thread
   Strung across the very top of the viewport; each bulb lights up as the
   surprise advances, echoing the "lights turning on" idea through every
   later stage (mirrored faintly behind the cake + final card).
   ========================================================================== */
#garland{
  position:fixed; top:0; left:0; width:100%; height:46px; z-index:40;
  pointer-events:none;
}
#garland svg{ width:100%; height:100%; overflow:visible; }
#garland-path{
  fill:none;
  stroke: rgba(255,255,255,0.12);
  stroke-width:1.5;
}
.bulb{
  transform-origin:center;
  fill: rgba(255,255,255,0.18);
  transition: fill .5s ease, filter .5s ease, transform .4s ease;
}
.bulb.on{
  fill: var(--accent-gold);
  filter: drop-shadow(0 0 6px var(--accent-gold)) drop-shadow(0 0 12px var(--accent-pink));
  animation: bulb-flicker 2.6s ease-in-out infinite;
}
.bulb.on:nth-child(odd){ animation-delay:.6s; }
@keyframes bulb-flicker{
  0%,100%{ opacity:1; transform:scale(1); }
  50%{ opacity:.75; transform:scale(.9); }
}

/* ==========================================================================
   4. PROGRESS INDICATOR
   ========================================================================== */
#progress{
  position:fixed; z-index:50;
  display:flex; gap:9px;
  right:18px; top:50%; transform:translateY(-50%);
  flex-direction:column;
}
@media (max-width:680px){
  #progress{
    right:auto; left:50%; top:auto; bottom:14px;
    transform:translateX(-50%);
    flex-direction:row;
  }
}
.dot{
  width:8px; height:8px; border-radius:50%;
  background: rgba(255,255,255,0.18);
  border:1px solid rgba(255,255,255,0.25);
  transition: all .4s ease;
}
.dot.active{
  background: var(--accent-pink);
  box-shadow:0 0 8px var(--accent-pink), 0 0 16px var(--accent-pink);
  transform:scale(1.3);
}
.dot.done{ background: var(--accent-violet); border-color:transparent; }

/* ==========================================================================
   5. SCREENS — one full-viewport stage at a time
   ========================================================================== */
.screen{
  position:fixed; inset:0; z-index:10;
  display:flex; align-items:center; justify-content:center;
  flex-direction:column;
  text-align:center;
  padding: 90px 22px 70px;
  opacity:0; visibility:hidden;
  transform: scale(1.03);
  transition: opacity .8s ease, transform .9s ease, visibility 0s linear .8s;
  overflow-y:auto;
}
.screen.active{
  opacity:1; visibility:visible; transform:scale(1);
  transition: opacity .8s ease, transform .9s ease, visibility 0s linear 0s;
}
.screen::-webkit-scrollbar{ width:0; }

.eyebrow{
  font-family:var(--font-body);
  letter-spacing:.32em;
  text-transform:uppercase;
  font-size:.68rem;
  color:var(--accent-gold);
  margin-bottom:18px;
  opacity:.9;
}

.headline{
  font-family:var(--font-display);
  font-weight:600;
  font-size:clamp(1.9rem, 6vw, 3.4rem);
  line-height:1.15;
  color:var(--text-soft);
  text-shadow:0 0 30px rgba(166,133,255,0.35);
  max-width:820px;
}
.headline em{
  font-style:italic;
  color:var(--accent-pink);
}

.subtext{
  margin-top:18px;
  font-size:1rem;
  color:var(--text-dim);
  max-width:520px;
  line-height:1.7;
}

.cta{
  margin-top:44px;
  padding:16px 38px;
  border-radius:999px;
  font-size:1rem;
  font-weight:600;
  letter-spacing:.02em;
  color:#1a0f2e;
  background: linear-gradient(120deg, var(--accent-gold), var(--accent-pink));
  box-shadow: var(--shadow-glow);
  position:relative;
  transition: transform .25s ease, box-shadow .25s ease;
}
.cta:hover{ transform:translateY(-3px) scale(1.03); box-shadow:0 0 55px rgba(255,111,165,0.5); }
.cta:active{ transform:translateY(0) scale(.98); }

.cta.ghost{
  color:var(--text-soft);
  background: var(--glass);
  border:1px solid var(--glass-border);
  box-shadow:none;
  backdrop-filter: blur(8px);
}
.cta.ghost:hover{ border-color: var(--accent-gold); }

.cta-row{ display:flex; gap:16px; flex-wrap:wrap; justify-content:center; margin-top:40px; }

/* Glass card, reused across stages */
.glass-card{
  background: var(--glass);
  border:1px solid var(--glass-border);
  border-radius:26px;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 20px 60px rgba(0,0,0,0.35);
  padding: 40px clamp(20px, 5vw, 52px);
}

/* ==========================================================================
   6. STAGE 1 — OPENING
   ========================================================================== */
#screen-opening .headline{ font-size:clamp(1.7rem, 5.6vw, 2.7rem); }
.gift-icon{
  font-size:2.4rem;
  display:inline-block;
  animation: float-bob 3.2s ease-in-out infinite;
}
@keyframes float-bob{
  0%,100%{ transform:translateY(0) rotate(0deg); }
  50%{ transform:translateY(-10px) rotate(-4deg); }
}

/* ==========================================================================
   7. STAGE 2 — LIGHTS / REVEAL PRELUDE
   ========================================================================== */
#bulb-field{
  position:absolute; inset:0; z-index:0; pointer-events:none; overflow:hidden;
}
.floaty-bulb{
  position:absolute;
  width:10px; height:14px;
  border-radius:50% 50% 50% 50% / 60% 60% 40% 40%;
  background: var(--accent-gold);
  opacity:0;
  filter: drop-shadow(0 0 8px var(--accent-gold));
  animation: bulb-rise 4.5s ease-in forwards;
}
@keyframes bulb-rise{
  0%{ opacity:0; transform:translateY(40px) scale(.4); }
  15%{ opacity:1; }
  100%{ opacity:0; transform:translateY(-260px) scale(1); }
}

/* ==========================================================================
   8. STAGE 3 — BIRTHDAY REVEAL
   ========================================================================== */
.big-title{
  font-family:var(--font-display);
  font-weight:700;
  line-height:1;
  letter-spacing:.02em;
}
.big-title .line1{
  display:block;
  font-size:clamp(1.6rem, 6vw, 2.6rem);
  color:var(--text-dim);
  letter-spacing:.3em;
  text-transform:uppercase;
  margin-bottom:6px;
}
.big-title .line2{
  display:block;
  font-size:clamp(3.2rem, 13vw, 7rem);
  background: linear-gradient(100deg, var(--accent-gold), var(--accent-pink) 55%, var(--accent-violet));
  -webkit-background-clip:text;
  background-clip:text;
  color:transparent;
  filter: drop-shadow(0 0 30px rgba(255,111,165,0.45));
  animation: title-pulse 3.5s ease-in-out infinite;
}
@keyframes title-pulse{
  0%,100%{ filter: drop-shadow(0 0 24px rgba(255,111,165,0.4)); }
  50%{ filter: drop-shadow(0 0 44px rgba(255,216,138,0.55)); }
}

.fx-layer{ position:fixed; inset:0; z-index:30; pointer-events:none; overflow:hidden; }

.balloon{
  position:absolute; bottom:-140px;
  width:46px; height:58px;
  border-radius:50% 50% 50% 50% / 58% 58% 42% 42%;
  opacity:.9;
  animation: balloon-float linear forwards;
}
.balloon::after{
  content:''; position:absolute; left:50%; top:100%; width:1px; height:60px;
  background: rgba(255,255,255,0.35); transform:translateX(-50%);
}
@keyframes balloon-float{
  0%{ transform:translateY(0) translateX(0) rotate(0deg); opacity:.95; }
  100%{ transform:translateY(-115vh) translateX(var(--drift,20px)) rotate(var(--rot,6deg)); opacity:0; }
}

.heart-particle{
  position:absolute;
  font-size:1.2rem;
  animation: heart-rise 2.6s ease-out forwards;
  pointer-events:none;
}
@keyframes heart-rise{
  0%{ transform:translateY(0) scale(.6); opacity:1; }
  100%{ transform:translateY(-160px) scale(1.1); opacity:0; }
}

.sparkle-particle{
  position:fixed; pointer-events:none; z-index:60;
  width:6px; height:6px; border-radius:50%;
  background: var(--accent-gold);
  box-shadow:0 0 8px var(--accent-gold), 0 0 14px var(--accent-pink);
  animation: sparkle-fade .8s ease-out forwards;
}
@keyframes sparkle-fade{
  0%{ opacity:1; transform:scale(1); }
  100%{ opacity:0; transform:scale(0) translateY(-14px); }
}

/* ==========================================================================
   9. STAGE 4 — PHOTO MEMORIES
   ========================================================================== */
.photo-strip{
  display:flex; gap:16px; flex-wrap:wrap; justify-content:center;
  max-width:900px; margin-top:30px;
}
.photo-card{
  width:150px; height:190px;
  border-radius:18px;
  overflow:hidden;
  position:relative;
  background: linear-gradient(160deg, rgba(255,255,255,0.08), rgba(255,255,255,0.02));
  border:1px solid var(--glass-border);
  box-shadow:0 14px 34px rgba(0,0,0,0.4);
  transform: rotate(var(--tilt,0deg));
  transition: transform .35s ease, box-shadow .35s ease;
}
.photo-card:hover{ transform: rotate(0deg) translateY(-6px) scale(1.04); box-shadow:0 20px 44px rgba(255,111,165,0.25); }
.photo-card img{ width:100%; height:100%; object-fit:cover; }
.photo-placeholder{
  width:100%; height:100%;
  display:flex; align-items:center; justify-content:center; flex-direction:column;
  gap:8px; color:var(--text-dim); font-size:.72rem; text-align:center; padding:10px;
}
.photo-placeholder .ph-icon{ font-size:1.6rem; opacity:.7; }
.photo-caption{
  margin-top:22px; font-family:var(--font-display); font-style:italic;
  font-size:1.05rem; color:var(--text-dim);
}

/* ==========================================================================
   10. STAGE 5 — MESSAGE
   ========================================================================== */
#message-card{ max-width:640px; }
#typed-message{
  font-family:var(--font-display);
  font-size:clamp(1.05rem, 2.6vw, 1.35rem);
  line-height:1.85;
  color:var(--text-soft);
  white-space:pre-wrap;
  min-height:220px;
  text-align:left;
}
.caret{
  display:inline-block; width:2px; height:1.1em; background:var(--accent-gold);
  margin-left:2px; vertical-align:middle;
  animation: caret-blink 1s steps(1) infinite;
}
@keyframes caret-blink{ 50%{ opacity:0; } }
.signature{
  margin-top:24px; text-align:right; font-family:var(--font-display);
  font-style:italic; color:var(--accent-pink); font-size:1.1rem;
}

/* ==========================================================================
   11. STAGE 6 — MUSIC
   ========================================================================== */
.player-card{ width:min(420px, 90vw); }
.player-title{ font-family:var(--font-display); font-size:1.3rem; margin-bottom:4px; }
.player-sub{ color:var(--text-dim); font-size:.82rem; margin-bottom:26px; }

.play-btn{
  width:74px; height:74px; border-radius:50%;
  background: linear-gradient(135deg, var(--accent-pink), var(--accent-violet));
  display:flex; align-items:center; justify-content:center;
  font-size:1.5rem; color:#fff;
  box-shadow: var(--shadow-glow);
  margin:0 auto 26px;
  transition: transform .2s ease;
}
.play-btn:hover{ transform:scale(1.06); }
.play-btn:active{ transform:scale(.95); }

.equalizer{
  display:flex; align-items:flex-end; justify-content:center;
  gap:5px; height:54px; margin-bottom:8px;
}
.eq-bar{
  width:6px; border-radius:4px;
  background: linear-gradient(180deg, var(--accent-gold), var(--accent-pink));
  height:6px;
  transition: height .12s ease;
}

.no-audio-note{
  margin-top:14px; font-size:.72rem; color:var(--text-dim); line-height:1.6;
}

/* ==========================================================================
   12. STAGE 7 — CAKE
   ========================================================================== */
.cake-wrap{ position:relative; margin: 10px 0 12px; }
.cake{
  --cake-w: 190px;
  width:var(--cake-w);
  position:relative;
}
.tier{
  width:100%;
  border-radius:10px;
  background: linear-gradient(180deg, #ffe3ee, #ffc4dd);
  box-shadow: inset 0 -8px 0 rgba(0,0,0,0.06), 0 10px 24px rgba(0,0,0,0.35);
  position:relative;
}
.tier.top{ height:52px; width:70%; margin:0 auto; background:linear-gradient(180deg, #fff2c9, #ffdf9e); }
.tier.bottom{ height:64px; margin-top:6px; }
.drip{
  position:absolute; top:-8px; left:0; right:0; height:16px;
  background-repeat:repeat-x; background-size:22px 16px;
  background-image: radial-gradient(circle at 50% 0%, var(--accent-pink) 0 7px, transparent 8px);
  opacity:.85;
}
.plate{
  width:120%; height:12px; margin-left:-10%;
  background: linear-gradient(180deg, rgba(255,255,255,0.5), rgba(255,255,255,0.1));
  border-radius:50%; margin-top:4px;
  box-shadow:0 12px 24px rgba(0,0,0,0.4);
}
.candles{
  position:absolute; top:-40px; left:0; right:0;
  display:flex; justify-content:center; gap:14px;
}
.candle{ width:5px; height:34px; background: linear-gradient(180deg, #fff, #d8c9ff); border-radius:2px; position:relative; }
.flame{
  position:absolute; left:50%; top:-16px; transform:translateX(-50%);
  width:9px; height:16px; border-radius:50% 50% 50% 50% / 60% 60% 40% 40%;
  background: radial-gradient(circle at 50% 30%, #fff6c8, var(--accent-gold) 55%, #ff9d4d);
  box-shadow:0 0 10px var(--accent-gold), 0 0 18px rgba(255,157,77,.7);
  animation: flame-flicker 1.1s ease-in-out infinite alternate;
  transition: opacity .4s ease, transform .4s ease;
}
@keyframes flame-flicker{
  0%{ transform:translateX(-50%) scale(1) rotate(-2deg); }
  100%{ transform:translateX(-50%) scale(1.12) rotate(3deg); }
}
.candle.blown .flame{ opacity:0; transform:translateX(-50%) scale(.2); }
.smoke{
  position:absolute; left:50%; top:-18px; transform:translateX(-50%);
  width:3px; height:0; background:rgba(255,255,255,0.5); border-radius:2px;
  opacity:0;
}
.candle.blown .smoke{ animation: smoke-rise 1.4s ease-out forwards; }
@keyframes smoke-rise{
  0%{ height:0; opacity:.6; transform:translateX(-50%) translateY(0); }
  100%{ height:26px; opacity:0; transform:translateX(-50%) translateY(-22px); }
}

.slice-line{
  position:absolute; inset:0; pointer-events:none;
  opacity:0;
}
.cake.cut .tier{ filter:none; }
.cake.cut::after{
  content:''; position:absolute; top:-4px; bottom:0; left:47%; width:2px;
  background: rgba(255,255,255,0.6);
  box-shadow:0 0 10px rgba(255,255,255,0.7);
}

/* ==========================================================================
   13. STAGE 8 — FINAL WISH
   ========================================================================== */
#screen-final .glass-card{ max-width:600px; }
.floating-hearts-bg{ position:absolute; inset:0; overflow:hidden; pointer-events:none; z-index:0; }
.bg-heart{
  position:absolute; bottom:-40px; color: var(--accent-pink);
  opacity:.5; animation: bg-heart-float linear infinite;
}
@keyframes bg-heart-float{
  0%{ transform:translateY(0) scale(.8); opacity:0; }
  10%{ opacity:.55; }
  100%{ transform:translateY(-115vh) scale(1.1); opacity:0; }
}

/* tap-for-sparkles hint (mobile) */
#tap-hint{
  position:fixed; bottom:14px; left:50%; transform:translateX(-50%);
  font-size:.72rem; color:var(--text-dim); z-index:45;
  background:var(--glass); border:1px solid var(--glass-border);
  padding:7px 14px; border-radius:999px; backdrop-filter:blur(10px);
  opacity:0; transition:opacity .6s ease;
  pointer-events:none;
}
#tap-hint.show{ opacity:.9; }
@media (min-width:681px){ #tap-hint{ display:none; } }

/* small screens fine-tuning */
@media (max-width:420px){
  .screen{ padding:70px 16px 90px; }
  .glass-card{ padding:28px 18px; }
  .photo-card{ width:118px; height:150px; }
}

@media (prefers-reduced-motion: reduce){
  *{ animation-duration:.001ms !important; animation-iteration-count:1 !important; transition-duration:.001ms !important; }
}
</style>
</head>
<body>

<!-- background layers -->
<div id="bg-glow"></div>
<canvas id="star-canvas"></canvas>

<!-- signature fairy-light garland -->
<div id="garland" aria-hidden="true">
  <svg viewBox="0 0 1000 46" preserveAspectRatio="none">
    <path id="garland-path" d="M0,6 Q125,42 250,10 T500,10 T750,10 T1000,6"></path>
  </svg>
</div>

<!-- progress dots -->
<div id="progress" aria-hidden="true"></div>

<div id="tap-hint">✨ Tap anywhere for sparkles</div>

<!-- effects layer for confetti / fireworks / floating hearts -->
<canvas id="fx-canvas" class="fx-layer"></canvas>
<div id="fx-dom" class="fx-layer"></div>

<audio id="bday-audio" loop preload="none"></audio>

<!-- ======================= STAGE 1 : OPENING ======================= -->
<section class="screen active" id="screen-opening" data-stage="1">
  <div class="eyebrow">a little something is waiting</div>
  <h1 class="headline">Someone Special Has A <em>Surprise</em> For You <span class="gift-icon">✨</span></h1>
  <p class="subtext">Before you do anything else today, take one quiet minute for this.</p>
  <div class="cta-row">
    <button class="cta" id="btn-open">Open Your Surprise 🎁</button>
  </div>
</section>

<!-- ======================= STAGE 2 : LIGHTS ======================= -->
<section class="screen" id="screen-lights" data-stage="2">
  <div id="bulb-field"></div>
  <div class="eyebrow" id="lights-eyebrow">the lights are coming on</div>
  <h1 class="headline" id="lights-headline"></h1>
  <div class="cta-row">
    <button class="cta" id="btn-begin">Let's Begin ✨</button>
  </div>
</section>

<!-- ======================= STAGE 3 : BIRTHDAY REVEAL ======================= -->
<section class="screen" id="screen-reveal" data-stage="3">
  <h1 class="big-title">
    <span class="line1">Happy Birthday</span>
    <span class="line2" id="reveal-name"></span>
  </h1>
  <p class="subtext" id="reveal-sub"></p>
  <div class="cta-row">
    <button class="cta" id="btn-to-photos">Continue the surprise →</button>
  </div>
</section>

<!-- ======================= STAGE 4 : PHOTOS ======================= -->
<section class="screen" id="screen-photos" data-stage="4">
  <div class="eyebrow">a little memory...</div>
  <h1 class="headline" style="font-size:clamp(1.5rem,4.4vw,2.2rem);">Moments Worth Keeping</h1>
  <div class="photo-strip" id="photo-strip"></div>
  <p class="photo-caption" id="photo-caption"></p>
  <div class="cta-row">
    <button class="cta" id="btn-to-message">Read your message →</button>
  </div>
</section>

<!-- ======================= STAGE 5 : MESSAGE ======================= -->
<section class="screen" id="screen-message" data-stage="5">
  <div class="glass-card" id="message-card">
    <div class="eyebrow" style="margin-bottom:22px;">from the heart</div>
    <p id="typed-message"><span class="caret"></span></p>
    <p class="signature" id="message-signature"></p>
  </div>
  <div class="cta-row">
    <button class="cta" id="btn-to-music">Play a song for you 🎵</button>
  </div>
</section>

<!-- ======================= STAGE 6 : MUSIC ======================= -->
<section class="screen" id="screen-music" data-stage="6">
  <div class="eyebrow">a little tune</div>
  <div class="glass-card player-card">
    <div class="player-title" id="song-title"></div>
    <div class="player-sub">tap play — sound stays off until you say so</div>
    <button class="play-btn" id="btn-play" aria-label="Play song">▶</button>
    <div class="equalizer" id="equalizer"></div>
    <p class="no-audio-note" id="audio-note" style="display:none;">Couldn't find the song file — drop your track at the path set in CONFIG.song.file and refresh.</p>
  </div>
  <div class="cta-row">
    <button class="cta" id="btn-to-cake">On to the cake 🎂</button>
  </div>
</section>

<!-- ======================= STAGE 7 : CAKE ======================= -->
<section class="screen" id="screen-cake" data-stage="7">
  <div class="eyebrow">one wish, then we cut it</div>
  <div class="cake-wrap">
    <div class="cake" id="cake">
      <div class="candles" id="candles"></div>
      <div class="tier top"><div class="drip"></div></div>
      <div class="tier bottom"><div class="drip"></div></div>
      <div class="plate"></div>
    </div>
  </div>
  <h2 class="headline" style="font-size:clamp(1.2rem,3.4vw,1.7rem); margin-top:26px;" id="cake-line">Make your wish, <span id="cake-name"></span> ✨</h2>
  <div class="cta-row">
    <button class="cta" id="btn-wish">Make A Wish ✨</button>
    <button class="cta ghost" id="btn-cut" style="display:none;">Cut The Cake 🎂</button>
  </div>
  <div class="cta-row" id="cake-continue-row" style="display:none;">
    <button class="cta" id="btn-to-final">See your final wish →</button>
  </div>
</section>

<!-- ======================= STAGE 8 : FINAL ======================= -->
<section class="screen" id="screen-final" data-stage="8">
  <div class="floating-hearts-bg" id="final-hearts-bg"></div>
  <div class="glass-card">
    <h2 class="headline" style="font-size:clamp(1.4rem,4vw,2rem);" id="final-heading"></h2>
    <p class="subtext" id="final-message" style="max-width:520px; text-align:left; line-height:1.85; margin-top:20px;"></p>
    <p class="signature" id="final-signature"></p>
    <div class="cta-row">
      <button class="cta ghost" id="btn-replay">Replay The Surprise 🔄</button>
    </div>
  </div>
</section>

<script>
/* ============================================================================
   ✨ CUSTOMIZE YOUR WEBSITE HERE ✨
   Everything you'd want to change lives in this one object.
   Nothing below this block needs to be touched for a basic re-skin.
   ============================================================================ */
const CONFIG = {
  // The birthday person's name — used everywhere on the site
  birthdayName: "Srushti",

  // Who this surprise is from
  senderName: "Your Name",

  // Shown on the reveal screen, under the big "HAPPY BIRTHDAY" title
  revealSubtext: "Today is all about celebrating you, {name}.",

  // The heart of the site — typed out on the message screen.
  // Use {name} anywhere you want the birthday name inserted.
  birthdayMessage:
`{name}, I just wanted to take a moment today to say how genuinely glad I am
that you're in my life.

You bring a kind of warmth into every ordinary day that turns it into
something worth remembering — and I don't say that lightly.

I hope this year brings you all the happiness you keep giving to everyone
else, real success in the things you're working toward, and a few more
beautiful memories for us to look back on someday.

Thank you for being part of the good ones so far. Keep smiling the way you
do — it genuinely makes things better.

Happy birthday, {name}. Here's to you. 🎂`,

  // Caption under the photo strip
  photoCaption: "a little memory...",

  // Background music
  song: {
    title: "A Song For You 🎵",
    file: "assets/birthday-song.mp3"
  },

  // Photo slots — add or remove as many as you like (3–5 recommended)
  photos: [
    { src: "assets/srushti.jpg",  alt: "Srushti", tilt: -4 },
    { src: "assets/memory2.jpg",  alt: "A memory", tilt: 3 },
    { src: "assets/memory3.jpg",  alt: "A memory", tilt: -2 },
    { src: "assets/memory4.jpg",  alt: "A memory", tilt: 5 }
  ],

  // Final closing card
  finalHeading: "Once Again, Happy Birthday {name}! 💖",

  // Theme colors — change these to re-skin the whole site instantly
  theme: {
    bgDeep:      "#0a0618",
    bgMid:       "#170b33",
    bgGlow:      "#2c1052",
    accentPink:  "#ff6fa5",
    accentGold:  "#ffd88a",
    accentViolet:"#a685ff",
    textSoft:    "#efe6ff",
    textDim:     "#b9a9e0"
  }
};
/* ============================================================================
   END CUSTOMIZE HERE — everything below is site logic
   ============================================================================ */

const fill = (str) => String(str).replaceAll("{name}", CONFIG.birthdayName);

/* ---------------------------------------------------------------------------
   THEME — push CONFIG.theme into CSS custom properties
--------------------------------------------------------------------------- */
function applyTheme(){
  const r = document.documentElement.style;
  const t = CONFIG.theme;
  r.setProperty('--bg-deep', t.bgDeep);
  r.setProperty('--bg-mid', t.bgMid);
  r.setProperty('--bg-glow', t.bgGlow);
  r.setProperty('--accent-pink', t.accentPink);
  r.setProperty('--accent-gold', t.accentGold);
  r.setProperty('--accent-violet', t.accentViolet);
  r.setProperty('--text-soft', t.textSoft);
  r.setProperty('--text-dim', t.textDim);
}

/* ---------------------------------------------------------------------------
   STAGE / SCREEN NAVIGATION
--------------------------------------------------------------------------- */
const screens = Array.from(document.querySelectorAll('.screen'));
const progressEl = document.getElementById('progress');
let currentStage = 1;

screens.forEach((s, i) => {
  const dot = document.createElement('span');
  dot.className = 'dot';
  dot.dataset.stage = i + 1;
  progressEl.appendChild(dot);
});
const dots = Array.from(progressEl.children);

function lightGarlandUpTo(stage){
  const bulbs = document.querySelectorAll('.bulb');
  bulbs.forEach(b => {
    const idx = Number(b.dataset.index);
    const threshold = Math.ceil((idx / (bulbs.length - 1)) * screens.length);
    b.classList.toggle('on', stage >= 2 && threshold <= stage);
  });
}

function goToStage(stage){
  currentStage = stage;
  screens.forEach(s => s.classList.toggle('active', Number(s.dataset.stage) === stage));
  dots.forEach((d, i) => {
    d.classList.toggle('active', i + 1 === stage);
    d.classList.toggle('done', i + 1 < stage);
  });
  lightGarlandUpTo(stage);
  document.body.classList.toggle('lit', stage >= 2);

  // stage-specific triggers
  if(stage === 2) startLightsAnimation();
  if(stage === 3) revealBirthday();
  if(stage === 4) buildPhotoStrip();
  if(stage === 5) startTyping();
  if(stage === 6) setupMusicScreen();
  if(stage === 7) buildCake();
  if(stage === 8) finalWish();

  const hint = document.getElementById('tap-hint');
  if('ontouchstart' in window){
    hint.classList.add('show');
    setTimeout(() => hint.classList.remove('show'), 4200);
  }
}

/* ---------------------------------------------------------------------------
   GARLAND — build bulbs along the SVG path
--------------------------------------------------------------------------- */
function buildGarland(){
  const svg = document.querySelector('#garland svg');
  const path = document.getElementById('garland-path');
  const len = path.getTotalLength();
  const count = window.innerWidth < 500 ? 11 : 17;
  for(let i = 0; i < count; i++){
    const pt = path.getPointAtLength((len / (count - 1)) * i);
    const c = document.createElementNS('http://www.w3.org/2000/svg','circle');
    c.setAttribute('cx', pt.x);
    c.setAttribute('cy', pt.y);
    c.setAttribute('r', 4.2);
    c.classList.add('bulb');
    c.dataset.index = i;
    svg.appendChild(c);
  }
}

/* ---------------------------------------------------------------------------
   STARFIELD — ambient drifting particles on canvas
--------------------------------------------------------------------------- */
const starCanvas = document.getElementById('star-canvas');
const sctx = starCanvas.getContext('2d');
let stars = [];
function sizeCanvas(){
  starCanvas.width = window.innerWidth * devicePixelRatio;
  starCanvas.height = window.innerHeight * devicePixelRatio;
  starCanvas.style.width = window.innerWidth + 'px';
  starCanvas.style.height = window.innerHeight + 'px';
  sctx.setTransform(devicePixelRatio,0,0,devicePixelRatio,0,0);
}
function initStars(){
  sizeCanvas();
  const count = Math.min(120, Math.floor(window.innerWidth / 8));
  stars = Array.from({length: count}, () => ({
    x: Math.random() * window.innerWidth,
    y: Math.random() * window.innerHeight,
    r: Math.random() * 1.4 + 0.3,
    speed: Math.random() * 0.15 + 0.02,
    twinkle: Math.random() * Math.PI * 2,
    twinkleSpeed: Math.random() * 0.02 + 0.01
  }));
}
function drawStars(){
  sctx.clearRect(0,0,window.innerWidth, window.innerHeight);
  stars.forEach(s => {
    s.twinkle += s.twinkleSpeed;
    s.y -= s.speed;
    if(s.y < -4) s.y = window.innerHeight + 4;
    const alpha = 0.4 + Math.sin(s.twinkle) * 0.35;
    sctx.beginPath();
    sctx.fillStyle = `rgba(240, 230, 255, ${Math.max(0, alpha)})`;
    sctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    sctx.fill();
  });
  requestAnimationFrame(drawStars);
}

/* ---------------------------------------------------------------------------
   STAGE 2 — LIGHTS: floating bulbs + copy
--------------------------------------------------------------------------- */
function startLightsAnimation(){
  document.getElementById('lights-headline').textContent = fill(`${CONFIG.birthdayName}, this little surprise is just for you 💖`);
  const field = document.getElementById('bulb-field');
  field.innerHTML = '';
  const n = 22;
  for(let i = 0; i < n; i++){
    const b = document.createElement('div');
    b.className = 'floaty-bulb';
    b.style.left = Math.random() * 100 + '%';
    b.style.bottom = (Math.random() * 20) + 'px';
    b.style.animationDelay = (Math.random() * 3) + 's';
    b.style.animationDuration = (3.5 + Math.random() * 2.5) + 's';
    field.appendChild(b);
  }
}

/* ---------------------------------------------------------------------------
   STAGE 3 — BIRTHDAY REVEAL: title, balloons, confetti, hearts
--------------------------------------------------------------------------- */
function revealBirthday(){
  document.getElementById('reveal-name').textContent = `${CONFIG.birthdayName.toUpperCase()} 🌸`;
  document.getElementById('reveal-sub').textContent = fill(CONFIG.revealSubtext);
  launchBalloons(10);
  confettiBurst(140);
}

function launchBalloons(n){
  const colors = [getVar('--accent-pink'), getVar('--accent-gold'), getVar('--accent-violet')];
  const layer = document.getElementById('fx-dom');
  for(let i = 0; i < n; i++){
    const el = document.createElement('div');
    el.className = 'balloon';
    el.style.left = (Math.random() * 92) + 'vw';
    el.style.background = `radial-gradient(circle at 35% 30%, #fff8, ${colors[i % colors.length]})`;
    el.style.setProperty('--drift', (Math.random() * 120 - 60) + 'px');
    el.style.setProperty('--rot', (Math.random() * 30 - 15) + 'deg');
    el.style.animationDuration = (7 + Math.random() * 4) + 's';
    el.style.animationDelay = (Math.random() * 1.2) + 's';
    layer.appendChild(el);
    setTimeout(() => el.remove(), 13000);
  }
}

function getVar(name){ return getComputedStyle(document.documentElement).getPropertyValue(name).trim(); }

/* ---------------------------------------------------------------------------
   CONFETTI + FIREWORKS — canvas particle bursts
--------------------------------------------------------------------------- */
const fxCanvas = document.getElementById('fx-canvas');
const fctx = fxCanvas.getContext('2d');
let fxParticles = [];
function sizeFxCanvas(){
  fxCanvas.width = window.innerWidth * devicePixelRatio;
  fxCanvas.height = window.innerHeight * devicePixelRatio;
  fxCanvas.style.width = window.innerWidth + 'px';
  fxCanvas.style.height = window.innerHeight + 'px';
  fctx.setTransform(devicePixelRatio,0,0,devicePixelRatio,0,0);
}
function confettiBurst(count = 100, originX, originY){
  const colors = [getVar('--accent-pink'), getVar('--accent-gold'), getVar('--accent-violet'), '#ffffff'];
  const ox = originX ?? window.innerWidth / 2;
  const oy = originY ?? window.innerHeight * 0.25;
  for(let i = 0; i < count; i++){
    const angle = Math.random() * Math.PI * 2;
    const speed = 2 + Math.random() * 6;
    fxParticles.push({
      x: ox, y: oy,
      vx: Math.cos(angle) * speed * (Math.random() * 1.4),
      vy: Math.sin(angle) * speed - 3,
      g: 0.12 + Math.random() * 0.06,
      size: 4 + Math.random() * 4,
      color: colors[Math.floor(Math.random() * colors.length)],
      rot: Math.random() * Math.PI,
      vr: (Math.random() - 0.5) * 0.3,
      life: 0,
      maxLife: 90 + Math.random() * 50,
      shape: Math.random() > 0.5 ? 'rect' : 'circle'
    });
  }
}
function fireworks(bursts = 4){
  for(let b = 0; b < bursts; b++){
    setTimeout(() => {
      const x = window.innerWidth * (0.2 + Math.random() * 0.6);
      const y = window.innerHeight * (0.15 + Math.random() * 0.35);
      const color = [getVar('--accent-pink'), getVar('--accent-gold'), getVar('--accent-violet')][b % 3];
      for(let i = 0; i < 60; i++){
        const angle = (Math.PI * 2 * i) / 60;
        const speed = 2.5 + Math.random() * 2.5;
        fxParticles.push({
          x, y,
          vx: Math.cos(angle) * speed,
          vy: Math.sin(angle) * speed,
          g: 0.05,
          size: 3,
          color,
          rot: 0, vr: 0,
          life: 0, maxLife: 60 + Math.random() * 30,
          shape: 'circle', fade: true
        });
      }
    }, b * 380);
  }
}
function animateFx(){
  fctx.clearRect(0, 0, window.innerWidth, window.innerHeight);
  fxParticles.forEach(p => {
    p.life++;
    p.vy += p.g;
    p.x += p.vx;
    p.y += p.vy;
    p.rot += p.vr;
    const alpha = Math.max(0, 1 - p.life / p.maxLife);
    fctx.save();
    fctx.globalAlpha = alpha;
    fctx.translate(p.x, p.y);
    fctx.rotate(p.rot);
    fctx.fillStyle = p.color;
    if(p.shape === 'rect'){
      fctx.fillRect(-p.size/2, -p.size/2, p.size, p.size * 0.6);
    } else {
      fctx.beginPath();
      fctx.arc(0, 0, p.size/2, 0, Math.PI * 2);
      fctx.fill();
    }
    fctx.restore();
  });
  fxParticles = fxParticles.filter(p => p.life < p.maxLife && p.y < window.innerHeight + 40);
  requestAnimationFrame(animateFx);
}

function heartBurst(x, y, n = 8){
  const layer = document.getElementById('fx-dom');
  for(let i = 0; i < n; i++){
    const el = document.createElement('div');
    el.className = 'heart-particle';
    el.textContent = ['💖','💕','✨','🌸'][Math.floor(Math.random() * 4)];
    el.style.left = (x + (Math.random() * 40 - 20)) + 'px';
    el.style.top = (y + (Math.random() * 20 - 10)) + 'px';
    el.style.animationDelay = (Math.random() * 0.2) + 's';
    layer.appendChild(el);
    setTimeout(() => el.remove(), 2800);
  }
}

/* sparkle cursor / tap trail */
function spawnSparkle(x, y){
  const s = document.createElement('div');
  s.className = 'sparkle-particle';
  s.style.left = x + 'px';
  s.style.top = y + 'px';
  document.body.appendChild(s);
  setTimeout(() => s.remove(), 850);
}
let lastSparkle = 0;
function pointerSparkleHandler(e){
  const now = Date.now();
  if(now - lastSparkle < 55) return;
  lastSparkle = now;
  const pt = e.touches ? e.touches[0] : e;
  spawnSparkle(pt.clientX, pt.clientY);
}
window.addEventListener('pointermove', pointerSparkleHandler);
window.addEventListener('touchstart', (e) => {
  const pt = e.touches[0];
  for(let i = 0; i < 6; i++){
    setTimeout(() => spawnSparkle(pt.clientX + (Math.random()*20-10), pt.clientY + (Math.random()*20-10)), i * 40);
  }
});

/* every .cta button also throws a small heart burst on click */
document.addEventListener('click', (e) => {
  if(e.target.closest('.cta')){
    const r = e.target.closest('.cta').getBoundingClientRect();
    heartBurst(r.left + r.width/2, r.top, 6);
  }
});

/* ---------------------------------------------------------------------------
   STAGE 4 — PHOTO MEMORIES
--------------------------------------------------------------------------- */
function buildPhotoStrip(){
  const strip = document.getElementById('photo-strip');
  strip.innerHTML = '';
  CONFIG.photos.forEach(p => {
    const card = document.createElement('div');
    card.className = 'photo-card';
    card.style.setProperty('--tilt', (p.tilt ?? 0) + 'deg');

    const img = document.createElement('img');
    img.src = p.src;
    img.alt = fill(p.alt || CONFIG.birthdayName);
    img.loading = 'lazy';
    img.onerror = () => {
      card.innerHTML = `<div class="photo-placeholder"><span class="ph-icon">🌸</span><span>photo coming soon</span></div>`;
    };
    card.appendChild(img);
    strip.appendChild(card);
  });
  document.getElementById('photo-caption').textContent = fill(CONFIG.photoCaption);
}

/* ---------------------------------------------------------------------------
   STAGE 5 — MESSAGE: typewriter effect
--------------------------------------------------------------------------- */
let typingTimer = null;
function startTyping(){
  const el = document.getElementById('typed-message');
  const full = fill(CONFIG.birthdayMessage);
  document.getElementById('message-signature').textContent = `— ${CONFIG.senderName}`;
  clearInterval(typingTimer);
  el.innerHTML = '<span class="caret"></span>';
  let i = 0;
  typingTimer = setInterval(() => {
    i++;
    el.innerHTML = full.slice(0, i).replaceAll('\n','<br>') + '<span class="caret"></span>';
    if(i >= full.length) clearInterval(typingTimer);
  }, 16);
}

/* ---------------------------------------------------------------------------
   STAGE 6 — MUSIC PLAYER + equalizer via Web Audio API
--------------------------------------------------------------------------- */
const audioEl = document.getElementById('bday-audio');
let audioCtx, analyser, sourceNode, eqBars = [];
let audioReady = false;

function setupMusicScreen(){
  document.getElementById('song-title').textContent = CONFIG.song.title;
  audioEl.src = CONFIG.song.file;

  const eq = document.getElementById('equalizer');
  if(eq.children.length === 0){
    for(let i = 0; i < 22; i++){
      const bar = document.createElement('div');
      bar.className = 'eq-bar';
      eq.appendChild(bar);
      eqBars.push(bar);
    }
  }

  audioEl.onerror = () => {
    document.getElementById('audio-note').style.display = 'block';
  };
}

function initAudioGraph(){
  if(audioCtx) return;
  try{
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    sourceNode = audioCtx.createMediaElementSource(audioEl);
    analyser = audioCtx.createAnalyser();
    analyser.fftSize = 64;
    sourceNode.connect(analyser);
    analyser.connect(audioCtx.destination);
    audioReady = true;
  }catch(err){
    audioReady = false;
  }
}

function drawEqualizer(){
  requestAnimationFrame(drawEqualizer);
  if(!analyser || audioEl.paused){
    eqBars.forEach(b => b.style.height = '5px');
    return;
  }
  const data = new Uint8Array(analyser.frequencyBinCount);
  analyser.getByteFrequencyData(data);
  eqBars.forEach((bar, i) => {
    const v = data[i % data.length] || 0;
    bar.style.height = Math.max(5, (v / 255) * 54) + 'px';
  });
}

document.getElementById('btn-play').addEventListener('click', function(){
  initAudioGraph();
  if(audioCtx && audioCtx.state === 'suspended') audioCtx.resume();
  if(audioEl.paused){
    audioEl.play().catch(() => document.getElementById('audio-note').style.display = 'block');
    this.textContent = '❚❚';
  } else {
    audioEl.pause();
    this.textContent = '▶';
  }
});

/* ---------------------------------------------------------------------------
   STAGE 7 — CAKE: candles, wish, cut
--------------------------------------------------------------------------- */
let cakeBuilt = false;
function buildCake(){
  document.getElementById('cake-name').textContent = CONFIG.birthdayName;
  if(cakeBuilt) return;
  cakeBuilt = true;
  const candlesEl = document.getElementById('candles');
  const n = 5;
  for(let i = 0; i < n; i++){
    const c = document.createElement('div');
    c.className = 'candle';
    c.innerHTML = `<span class="flame"></span><span class="smoke"></span>`;
    candlesEl.appendChild(c);
  }
}

document.getElementById('btn-wish').addEventListener('click', function(){
  document.querySelectorAll('.candle').forEach((c, i) => {
    setTimeout(() => c.classList.add('blown'), i * 160);
  });
  document.getElementById('cake-line').textContent = fill(`Wish made, ${CONFIG.birthdayName} ✨ — now for the fun part.`);
  this.style.display = 'none';
  document.getElementById('btn-cut').style.display = 'inline-block';
  confettiBurst(90, window.innerWidth/2, window.innerHeight * 0.55);
});

document.getElementById('btn-cut').addEventListener('click', function(){
  document.getElementById('cake').classList.add('cut');
  this.style.display = 'none';
  document.getElementById('cake-line').textContent = fill(`Sweetest slice for you, ${CONFIG.birthdayName} 🍰`);
  fireworks(4);
  document.getElementById('cake-continue-row').style.display = 'flex';
});

/* ---------------------------------------------------------------------------
   STAGE 8 — FINAL WISH
--------------------------------------------------------------------------- */
let finalHeartsInterval = null;
function finalWish(){
  document.getElementById('final-heading').textContent = fill(CONFIG.finalHeading);
  document.getElementById('final-message').textContent = fill(CONFIG.birthdayMessage).split('\n\n')[0] + '\n\n' + fill(CONFIG.birthdayMessage).split('\n\n').slice(-1)[0];
  document.getElementById('final-signature').textContent = `— ${CONFIG.senderName}`;

  const bg = document.getElementById('final-hearts-bg');
  bg.innerHTML = '';
  clearInterval(finalHeartsInterval);
  const spawn = () => {
    const h = document.createElement('div');
    h.className = 'bg-heart';
    h.textContent = ['💖','🌸','✨'][Math.floor(Math.random()*3)];
    h.style.left = Math.random() * 100 + '%';
    h.style.fontSize = (0.9 + Math.random()*1.2) + 'rem';
    h.style.animationDuration = (6 + Math.random()*5) + 's';
    bg.appendChild(h);
    setTimeout(() => h.remove(), 12000);
  };
  for(let i = 0; i < 10; i++) setTimeout(spawn, i * 220);
  finalHeartsInterval = setInterval(spawn, 900);

  confettiBurst(110);
}

/* ---------------------------------------------------------------------------
   NAVIGATION WIRING
--------------------------------------------------------------------------- */
document.getElementById('btn-open').addEventListener('click', () => goToStage(2));
document.getElementById('btn-begin').addEventListener('click', () => goToStage(3));
document.getElementById('btn-to-photos').addEventListener('click', () => goToStage(4));
document.getElementById('btn-to-message').addEventListener('click', () => goToStage(5));
document.getElementById('btn-to-music').addEventListener('click', () => goToStage(6));
document.getElementById('btn-to-cake').addEventListener('click', () => goToStage(7));
document.getElementById('btn-to-final').addEventListener('click', () => goToStage(8));
document.getElementById('btn-replay').addEventListener('click', () => {
  clearInterval(finalHeartsInterval);
  if(!audioEl.paused){ audioEl.pause(); document.getElementById('btn-play').textContent = '▶'; }
  document.getElementById('btn-wish').style.display = 'inline-block';
  document.getElementById('btn-cut').style.display = 'none';
  document.getElementById('cake-continue-row').style.display = 'none';
  document.getElementById('cake').classList.remove('cut');
  document.querySelectorAll('.candle').forEach(c => c.classList.remove('blown'));
  goToStage(1);
});

/* ---------------------------------------------------------------------------
   INIT
--------------------------------------------------------------------------- */
window.addEventListener('resize', () => { sizeCanvas(); sizeFxCanvas(); });

applyTheme();
buildGarland();
initStars();
sizeFxCanvas();
drawStars();
animateFx();
drawEqualizer();
goToStage(1);
</script>
</body>
</html>
