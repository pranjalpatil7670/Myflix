# Myflix
Welcome to myflix .
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MyFlix</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: #141414; color: #fff; font-family: 'Segoe UI', sans-serif; }
    nav {
      padding: 16px 40px;
      background: #000;
      position: sticky;
      top: 0;
      z-index: 999;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .nav-left { display: flex; align-items: center; gap: 30px; }
    .logo { font-size: 26px; font-weight: 900; color: #e50914; }
    nav a { color: #ccc; text-decoration: none; font-size: 14px; cursor: pointer; }
    nav a:hover { color: #fff; }
    nav a.active { color: #fff; font-weight: 600; }
    .search-bar {
      display: flex; align-items: center;
      background: #1f1f1f; border: 1px solid #333;
      border-radius: 6px; padding: 6px 14px; gap: 8px;
    }
    .search-bar input {
      background: none; border: none; outline: none;
      color: #fff; font-size: 14px; width: 200px;
    }
    .search-bar input::placeholder { color: #666; }
    .hero {
      background: linear-gradient(to right, #000 30%, transparent),
                  linear-gradient(to top, #141414 0%, transparent 60%),
                  url('https://images.unsplash.com/photo-1489599849927-2ee91cede3ba?w=1400') center/cover no-repeat;
      min-height: 420px; display: flex; align-items: center; padding: 60px 40px;
    }
    .hero h1 { font-size: 44px; font-weight: 900; margin-bottom: 12px; }
    .hero p { font-size: 15px; color: #ccc; margin-bottom: 24px; max-width: 420px; line-height: 1.6; }
    .btn-play {
      background: #fff; color: #000; border: none;
      padding: 12px 28px; border-radius: 6px;
      font-size: 15px; font-weight: 700; cursor: pointer;
    }
    .filter-tabs { display: flex; gap: 10px; padding: 24px 40px 0; flex-wrap: wrap; }
    .tab {
      padding: 8px 20px; border-radius: 20px; background: #2a2a2a;
      color: #ccc; font-size: 13px; cursor: pointer; border: none; transition: all 0.2s;
    }
    .tab:hover { background: #444; color: #fff; }
    .tab.active { background: #e50914; color: #fff; font-weight: 600; }
    .no-results { text-align: center; padding: 60px; color: #666; font-size: 16px; display: none; }
    .section { padding: 28px 40px; }
    .section h2 { font-size: 18px; font-weight: 700; margin-bottom: 14px; color: #e5e5e5; }
    .video-row { display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap: 14px; }
    .video-card { border-radius: 8px; overflow: hidden; background: #1f1f1f; transition: transform 0.2s; }
    .video-card:hover { transform: scale(1.04); }
    .video-card iframe { width: 100%; height: 160px; border: none; display: block; }
    .card-thumb { width: 100%; height: 160px; object-fit: cover; display: block; cursor: pointer; }
    .play-overlay { position: relative; cursor: pointer; }
    .play-overlay::after {
      content: '▶'; position: absolute; top: 50%; left: 50%;
      transform: translate(-50%, -50%); font-size: 40px;
      color: rgba(255,255,255,0.85); text-shadow: 0 0 20px #000; pointer-events: none;
    }
    .card-info { padding: 10px 14px 14px; }
    .card-title { font-size: 13px; font-weight: 600; color: #fff; }
    .card-meta { font-size: 11px; color: #888; margin-top: 3px; }
    .card-category { display: inline-block; font-size: 10px; padding: 2px 8px; border-radius: 10px; margin-top: 5px; font-weight: 600; }
    .cat-kids { background: #1a6b3c; color: #4ade80; }
    .cat-music { background: #4a1d96; color: #c4b5fd; }
    .cat-movies { background: #7c2d12; color: #fb923c; }
    .cat-popular { background: #7f1d1d; color: #f87171; }
    .cat-nature { background: #14532d; color: #86efac; }
    footer { text-align: center; padding: 30px; color: #444; font-size: 12px; border-top: 1px solid #222; margin-top: 30px; }
    @media (max-width: 650px) {
      nav { padding: 12px 16px; flex-wrap: wrap; gap: 10px; }
      .search-bar input { width: 130px; }
      .hero { padding: 30px 16px; min-height: 300px; }
      .hero h1 { font-size: 26px; }
      .section { padding: 20px 16px; }
      .filter-tabs { padding: 16px 16px 0; }
    }
  </style>
</head>
<body>

<nav>
  <div class="nav-left">
    <div class="logo">▶ MyFlix</div>
    <a class="active" onclick="filterCategory('all')">Home</a>
    <a onclick="filterCategory('kids')">Kids</a>
    <a onclick="filterCategory('music')">Music</a>
    <a onclick="filterCategory('movies')">Movies</a>
  </div>
  <div class="search-bar">
    <span>🔍</span>
    <input type="text" id="searchInput" placeholder="Search videos..." oninput="searchVideos()"/>
  </div>
</nav>

<div class="hero">
  <div>
    <h1>Welcome to MyFlix 🎬</h1>
    <p>Apni pasand ki videos dekho — Kids, Music, Movies aur bahut kuch!</p>
    <button class="btn-play" onclick="document.querySelector('.filter-tabs').scrollIntoView({behavior:'smooth'})">▶ Watch Now</button>
  </div>
</div>

<div class="filter-tabs">
  <button class="tab active" onclick="filterCategory('all')">🎬 All</button>
  <button class="tab" onclick="filterCategory('popular')">🔥 Popular</button>
  <button class="tab" onclick="filterCategory('kids')">🧒 Kids</button>
  <button class="tab" onclick="filterCategory('music')">🎵 Music</button>
  <button class="tab" onclick="filterCategory('movies')">🎥 Movies</button>
  <button class="tab" onclick="filterCategory('nature')">🌿 Nature</button>
</div>

<div class="no-results" id="noResults">😕 Koi video nahi mili!</div>
<div id="videos-container"></div>

<footer>© 2024 MyFlix — Made with ❤️</footer>

<script>
const videos = [
  { id: "xvFZjo5PgG0", title: "Popular Video 1", meta: "Trending", category: "popular" },
  { id: "V-_O7nl0Ii0", title: "Popular Video 2", meta: "Trending", category: "popular" },
  { id: "JGwWNGJdvx8", title: "Popular Video 3", meta: "Trending", category: "popular" },
  { id: "hZ4bFMnEsHY", title: "Baby Shark Dance", meta: "Kids Song", category: "kids" },
  { id: "yCjJyiqpAuU", title: "Wheels on the Bus", meta: "Nursery Rhyme", category: "kids" },
  { id: "XqZsoesa55w", title: "Happy Birthday Song", meta: "Kids Song", category: "kids" },
  { id: "0ZNIQOO2sfA", title: "Johny Johny Yes Papa", meta: "Nursery Rhyme", category: "kids" },
  { id: "tntOCGkgt98", title: "Twinkle Twinkle Little Star", meta: "Kids Song", category: "kids" },
  { id: "kffacxfA7G4", title: "Believer - Imagine Dragons", meta: "English Song", category: "music" },
  { id: "hT_nvWreIhg", title: "Counting Stars - OneRepublic", meta: "English Song", category: "music" },
  { id: "09R8_2nJtjg", title: "Sugar - Maroon 5", meta: "English Song", category: "music" },
  { id: "fRh_vgS2dFE", title: "Sorry - Justin Bieber", meta: "English Song", category: "music" },
  { id: "ByXuk9QqQkk", title: "Movie Trailer 1", meta: "Hollywood", category: "movies" },
  { id: "8g18jFHCLXk", title: "Movie Trailer 2", meta: "Bollywood", category: "movies" },
  { id: "giXco2jaZ_4", title: "Movie Trailer 3", meta: "Action", category: "movies" },
  { id: "aqz-KE-bpKQ", title: "Amazing Nature Documentary", meta: "Wildlife", category: "nature" },
  { id: "LXb3EKWsInQ", title: "Relaxing Ocean Waves", meta: "Nature Sounds", category: "nature" },
  { id: "1ZYbU82uhe8", title: "Beautiful Landscapes", meta: "Nature", category: "nature" },
];

const catLabels = {
  kids: ["cat-kids","🧒 Kids"], music: ["cat-music","🎵 Music"],
  movies: ["cat-movies","🎥 Movies"], popular: ["cat-popular","🔥 Popular"], nature: ["cat-nature","🌿 Nature"],
};
const sectionTitles = {
  popular: "🔥 Popular Videos", kids: "🧒 Kids Videos",
  music: "🎵 Music", movies: "🎥 Movies", nature: "🌿 Nature",
};

let currentCategory = "all";
let currentSearch = "";

function makeCard(v) {
  const [catClass, catLabel] = catLabels[v.category] || ["cat-popular", v.category];
  return `<div class="video-card" data-cat="${v.category}">
    <div class="play-overlay" onclick="playVideo(this,'${v.id}')">
      <img class="card-thumb" src="https://img.youtube.com/vi/${v.id}/mqdefault.jpg" alt="${v.title}" loading="lazy"/>
    </div>
    <div class="card-info">
      <div class="card-title">${v.title}</div>
      <div class="card-meta">${v.meta}</div>
      <span class="card-category ${catClass}">${catLabel}</span>
    </div>
  </div>`;
}

function playVideo(el, id) {
  el.outerHTML = `<iframe src="https://www.youtube.com/embed/${id}?autoplay=1" allowfullscreen allow="autoplay; encrypted-media"></iframe>`;
}

function renderVideos(list) {
  const container = document.getElementById('videos-container');
  const noResults = document.getElementById('noResults');
  if (list.length === 0) { container.innerHTML=''; noResults.style.display='block'; return; }
  noResults.style.display = 'none';
  if (currentCategory === 'all' && !currentSearch) {
    const groups = {};
    list.forEach(v => { if (!groups[v.category]) groups[v.category]=[]; groups[v.category].push(v); });
    const order = ['popular','kids','music','movies','nature'];
    container.innerHTML = order.filter(c=>groups[c]).map(c=>`
      <div class="section">
        <h2>${sectionTitles[c]}</h2>
        <div class="video-row">${groups[c].map(makeCard).join('')}</div>
      </div>`).join('');
  } else {
    container.innerHTML = `<div class="section">
      <h2>${currentSearch ? '🔍 "'+currentSearch+'"' : sectionTitles[currentCategory]||''}</h2>
      <div class="video-row">${list.map(makeCard).join('')}</div>
    </div>`;
  }
}

function filterCategory(cat) {
  currentCategory = cat; currentSearch = '';
  document.getElementById('searchInput').value = '';
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  event.target.classList.add('active');
  renderVideos(cat==='all' ? videos : videos.filter(v=>v.category===cat));
}

function searchVideos() {
  const q = document.getElementById('searchInput').value.toLowerCase().trim();
  currentSearch = q;
  if (!q) { filterCategory2(currentCategory); return; }
  renderVideos(videos.filter(v => v.title.toLowerCase().includes(q) || v.meta.toLowerCase().includes(q) || v.category.includes(q)));
}

function filterCategory2(cat) {
  renderVideos(cat==='all' ? videos : videos.filter(v=>v.category===cat));
}

renderVideos(videos);
</script>
</body>
</html>
