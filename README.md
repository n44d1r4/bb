<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Ucapan Ultah 🎉</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      margin-top: 100px;
      background-color: #fff0f5;
      overflow-x: hidden;
    }

    #pertanyaan2, #ucapan, #bukanUltah, #tombolHadiah {
      display: none;
      margin-top: 20px;
    }

    input, select, button {
      font-size: 18px;
      padding: 10px 20px;
      margin: 10px;
    }

    .btn-group {
      display: flex;
      justify-content: center;
      gap: 20px;
      flex-wrap: wrap;
    }

    .emoji {
      position: absolute;
      animation: jatuh 3s linear forwards;
      font-size: 30px;
    }

    @keyframes jatuh {
      0% { transform: translateY(-100px); opacity: 1; }
      100% { transform: translateY(100vh); opacity: 0; }
    }
  </style>
</head>
<body>

  <!-- Musik ulang tahun -->
  <audio id="musik" autoplay loop>
    <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mp3">
  </audio>

  <!-- Sound salah -->
  <audio id="salahSound">
    <source src="https://www.myinstants.com/media/sounds/wrong-answer.mp3" type="audio/mp3">
  </audio>

  <h2 id="pertanyaan1">Haiii kamu ulang tahun hari ini yaa? 🎉</h2>
  <div class="btn-group">
    <button onclick="jawabanUltah(true)">Iyaa 😍</button>
    <button onclick="jawabanUltah(false)">Enggak 🙄</button>
  </div>

  <div id="pertanyaan2">
    <h3>Pilih tanggal lahir kamu yuk! (Agustus)</h3>
    <select id="tanggalInput">
      <option value="">-- Pilih tanggal --</option>
      ${Array.from({ length: 31 }, (_, i) => `<option value="${i + 1}">${i + 1} Agustus</option>`).join('')}
    </select>
    <button onclick="tampilkanUcapan()">Lihat Ucapan 🎁</button>
  </div>

  <div id="ucapan"></div>
  <div id="tombolHadiah">
    <button onclick="emojiJatuh()">Klik untuk dapet hadiah 🎈</button>
  </div>
  <div id="bukanUltah"><p>Boong kamu kan ulang tahun, aku tauu 😏 Ayo ulang dan pilih <strong>Iya</strong> yaa!</p></div>

  <script>
    const ucapanList = [
      "Selamat ulang tahun!! 🎉 Hari ini, 4 Agustus, hari kamu! ✨",
      "Happy birthday yang paling spesial buat kamu 🎂💖 Semoga bahagia selalu ya!",
      "Yeeey ulang tahun kamu tiba juga! Semoga makin disayang, makin sehat, dan makin bahagia 💫",
      "Kamu itu hadiah terbaik buat dunia. Selamat ulang tahun, sayang! 🥰🎉",
      "4 Agustus jadi lebih istimewa karena itu hari kamu lahir. Happy birthday! 🎈🎂"
    ];

    function jawabanUltah(isUltah) {
      document.getElementById("pertanyaan1").style.display = "none";
      document.querySelector(".btn-group").style.display = "none";

      if (isUltah) {
        document.getElementById("pertanyaan2").style.display = "block";
      } else {
        document.getElementById("bukanUltah").style.display = "block";
      }
    }

    function tampilkanUcapan() {
      const tanggal = document.getElementById("tanggalInput").value;
      const ucapanDiv = document.getElementById("ucapan");
      const salahSound = document.getElementById("salahSound");

      if (tanggal === "") {
        alert("Pilih dulu tanggalnya yaa 😝");
        return;
      }

      if (tanggal !== "4") {
        document.getElementById("pertanyaan2").style.display = "none";
        ucapanDiv.style.display = "block";
        document.getElementById("tombolHadiah").style.display = "none";
        ucapanDiv.innerHTML = `<p>Ngapain? Aku tau kok kamu ulang tahunnya bukan di tanggal ini 😒</p>`;
        salahSound.play();
        return;
      }

      const ucapanRandom = ucapanList[Math.floor(Math.random() * ucapanList.length)];

      document.getElementById("pertanyaan2").style.display = "none";
      ucapanDiv.style.display = "block";
      document.getElementById("tombolHadiah").style.display = "block";

      ucapanDiv.innerHTML = `
        <p>${ucapanRandom}</p>
        <img src="https://media.giphy.com/media/l0MYt5jPR6QX5pnqM/giphy.gif" width="200" alt="party gif"/>
      `;
    }

    function emojiJatuh() {
      const emojiList = ['🎉', '🎁', '🎂', '🎈', '✨', '💖'];
      for (let i = 0; i < 30; i++) {
        const emoji = document.createElement('div');
        emoji.className = 'emoji';
        emoji.innerText = emojiList[Math.floor(Math.random() * emojiList.length)];
        emoji.style.left = Math.random() * window.innerWidth + 'px';
        emoji.style.top = '-50px';
        document.body.appendChild(emoji);
        setTimeout(() => emoji.remove(), 3000);
      }
    }
  </script>

</body>
</html>
