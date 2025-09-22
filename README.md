<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SKD Gaming Channel</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { margin: 0; font-family: Arial, sans-serif; background: #111; color: #eee; }
    header { background: #222; padding: 15px 20px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; z-index: 1000; }
    header .logo { font-size: 1.5em; font-weight: bold; color: #f39c12; }
    nav a { margin: 0 10px; color: #eee; text-decoration: none; font-weight: bold; }
    nav a:hover { color: #f39c12; }
    section { padding: 50px 20px; text-align: center; }
    .hero iframe { max-width: 560px; width: 100%; height: 315px; border-radius: 10px; }
    .btn { display: inline-block; margin-top: 15px; padding: 10px 20px; background: #f39c12; color: #111; text-decoration: none; border-radius: 5px; font-weight: bold; }
    .videos, .live, .about, .contact { background: #1a1a1a; margin: 20px auto; border-radius: 10px; max-width: 1000px; }
    .video-card { margin: 20px auto; }
    iframe { border-radius: 10px; }
    footer { background: #222; text-align: center; padding: 20px; color: #888; }
  </style>
</head>
<body>

  <!-- Header / Navigation -->
  <header>
    <div class="logo">🎮 SKD Gaming</div>
    <nav>
      <a href="#home">Home</a>
      <a href="#videos">Videos</a>
      <a href="#live">Live</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <!-- Home -->
  <section id="home" class="hero">
    <h1>Welcome to SKD Gaming!</h1>
    <iframe src="https://www.youtube.com/embed/7AAVa-6eHXA" frameborder="0" allowfullscreen></iframe>
    <p>Subscribe for the best gaming content!</p>
    <a href="https://youtube.com/@skdgamingchannel1" target="_blank" class="btn">Subscribe</a>
  </section>

  <!-- Latest Videos -->
  <section id="videos" class="videos">
    <h2>🎬 Latest Uploads</h2>
    <div id="video-list"></div>
  </section>

  <!-- Live Stream -->
  <section id="live" class="live">
    <h2>🔴 Live Stream</h2>
    <div id="live-section">
      <p>Checking live status...</p>
    </div>
  </section>

  <!-- About -->
  <section id="about" class="about">
    <h2>ℹ️ About SKD Gaming</h2>
    <p>SKD Gaming Channel brings you epic gameplay, tips, and fun live streams. Join the community and level up your skills!</p>
  </section>

  <!-- Contact -->
  <section id="contact" class="contact">
    <h2>📞 Contact & Social Links</h2>
    <p>Email: skdgaming@example.com</p>
    <p>Discord: <a href="#" target="_blank">Join Discord</a></p>
    <p>Instagram: <a href="#" target="_blank">@skdgaming</a></p>
    <p>Twitter: <a href="#" target="_blank">@skdgaming</a></p>
  </section>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 SKD Gaming • All Rights Reserved</p>
  </footer>

  <!-- Script -->
  <script>
    const API_KEY = "AIzaSyD1MZ-rVniHyfSr0hGXnW7ZJSDdu3aj2bc";
    const CHANNEL_ID = "UCip0Ls4Gx7iJvo8VmDtA2pA"; // SKD channel ka ID
    const videoList = document.getElementById("video-list");
    const liveSection = document.getElementById("live-section");

    // Fetch Latest Videos
    async function loadVideos() {
      const url = `https://www.googleapis.com/youtube/v3/search?key=${API_KEY}&channelId=${CHANNEL_ID}&part=snippet,id&order=date&maxResults=3`;
      const res = await fetch(url);
      const data = await res.json();
      videoList.innerHTML = "";
      data.items.forEach(item => {
        if (item.id.videoId) {
          const video = document.createElement("div");
          video.classList.add("video-card");
          video.innerHTML = `
            <iframe width="100%" height="250" 
              src="https://www.youtube.com/embed/${item.id.videoId}" 
              frameborder="0" allowfullscreen></iframe>
            <h3>${item.snippet.title}</h3>
          `;
          videoList.appendChild(video);
        }
      });
    }

    // Check Live Stream
    async function checkLive() {
      const url = `https://www.googleapis.com/youtube/v3/search?part=snippet&channelId=${CHANNEL_ID}&eventType=live&type=video&key=${API_KEY}`;
      const res = await fetch(url);
      const data = await res.json();
      if (data.items && data.items.length > 0) {
        const liveId = data.items[0].id.videoId;
        liveSection.innerHTML = `
          <iframe width="560" height="315" 
            src="https://www.youtube.com/embed/${liveId}" 
            frameborder="0" allowfullscreen></iframe>
        `;
      } else {
        liveSection.innerHTML = "<p>No live stream right now. Stay tuned!</p>";
      }
    }

    loadVideos();
    checkLive();
  </script>

</body>
</html>
