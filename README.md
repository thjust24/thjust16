<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>HSC-24 | BGC</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background: #000;
      padding: 2rem;
      margin: 0;
      position: relative;
      min-height: 100vh;
      color: #fff;
      overflow-x: hidden;
    }
    .watermark-container {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 500px;
      height: 500px;
      z-index: -1;
    }
    .watermark {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 500px;
      height: auto;
      opacity: 0.1;
    }
    .bubble {
      position: absolute;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(255,255,255,0.3), rgba(255,255,255,0));
      box-shadow: 0 0 10px rgba(255,255,255,0.5);
      cursor: pointer;
      animation: grow 10s linear forwards;
    }
    @keyframes grow {
      0% {
        transform: translate(-50%, -50%) scale(0.1);
        opacity: 0.8;
      }
      100% {
        transform: translate(-50%, -50%) scale(3);
        opacity: 0.5;
      }
    }
    .water-particle {
      position: absolute;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      animation: splash 1s ease-out forwards;
    }
    @keyframes splash {
      0% {
        transform: translate(-50%, -50%) scale(1);
        opacity: 1;
      }
      100% {
        transform: translate(-50%, -50%) scale(0);
        opacity: 0;
      }
    }
    .particle {
      position: absolute;
      width: 2px;
      height: 2px;
      background: #fff;
      border-radius: 50%;
      opacity: 0.5;
      animation: particleMove 15s infinite linear;
    }
    @keyframes particleMove {
      0% {
        transform: translateY(0);
        opacity: 0.5;
      }
      100% {
        transform: translateY(100vh);
        opacity: 0;
      }
    }
    h1 {
      text-align: center;
      color: #00b7eb;
      animation: fadeIn 2s ease-in;
    }
    @keyframes fadeIn {
      0% { opacity: 0; }
      100% { opacity: 1; }
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
      max-width: 1200px;
      margin-left: auto;
      margin-right: auto;
    }
    .card {
      background: linear-gradient(135deg, #1a1a40, #2a2a60);
      padding: 1rem;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(255,255,255,0.1);
      text-align: center;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      opacity: 0;
      transform: translateY(20px);
      animation: fadeInCard 0.5s forwards;
    }
    .card.matched {
      border: 2px solid #00b7eb;
      box-shadow: 0 0 15px rgba(0, 183, 235, 0.5);
    }
    .card:hover {
      transform: scale(1.05);
      box-shadow: 0 0 15px rgba(0, 183, 235, 0.5);
    }
    @keyframes fadeInCard {
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    .image-container {
      position: relative;
      display: inline-block;
    }
    .card a img {
      width: 100%;
      max-height: 220px;
      object-fit: cover;
      border-radius: 10px;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .card a img:hover {
      transform: scale(1.05);
      box-shadow: 0 0 10px #00b7eb;
    }
    .author-label {
      position: absolute;
      top: 10px;
      right: 10px;
      background: rgba(0, 0, 0, 0.7);
      color: #fff;
      padding: 5px 10px;
      border-radius: 5px;
      font-size: 0.8rem;
      font-weight: bold;
    }
    .name {
      font-size: 1.2rem;
      color: #00b7eb;
      font-weight: bold;
      margin-top: 0.6rem;
    }
    .bio {
      color: #ddd;
      font-size: 1rem;
      margin-top: 0.4rem;
    }
    .versity, .subject, .gmail {
      position: relative;
      display: flex;
      align-items: center;
      background: radial-gradient(circle, rgba(255,255,255,0.1), rgba(255,255,255,0.05));
      border: 1px solid transparent;
      border-image: linear-gradient(45deg, #00b7eb, #90ee90) 1;
      border-radius: 5px;
      padding: 8px 10px;
      margin-top: 0.5rem;
      transition: border-image 0.3s ease, box-shadow 0.3s ease;
      opacity: 0;
      transform: translateX(-20px);
      animation: slideIn 0.5s forwards;
    }
    .versity:hover, .subject:hover, .gmail:hover {
      border-image: linear-gradient(45deg, #90ee90, #00b7eb) 1;
      box-shadow: 0 0 10px rgba(0, 183, 235, 0.3);
    }
    .versity::before, .subject::before, .gmail::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle, rgba(0, 183, 235, 0.1), transparent);
      opacity: 0;
      transition: opacity 0.3s ease;
    }
    .versity:hover::before, .subject:hover::before, .gmail:hover::before {
      opacity: 1;
    }
    @keyframes slideIn {
      to {
        opacity: 1;
        transform: translateX(0);
      }
    }
    .versity {
      font-size: 0.95rem;
    }
    .subject {
      font-size: 0.9rem;
    }
    .gmail {
      font-size: 0.85rem;
    }
    .versity .icon, .subject .icon, .gmail .icon {
      margin-right: 8px;
      width: 18px;
      height: 18px;
      fill: #00b7eb;
      transition: transform 0.3s ease;
    }
    .versity .icon:hover, .subject .icon:hover, .gmail .icon:hover {
      transform: scale(1.2);
      animation: pulse 1s infinite;
    }
    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.2); }
      100% { transform: scale(1); }
    }
    .versity .value, .subject .value, .gmail .value {
      color: #00b7eb;
      font-style: italic;
      font-weight: 500;
      position: relative;
      transition: all 0.3s ease;
      text-shadow: 0 0 5px rgba(0, 183, 235, 0.5);
    }
    .versity .value:hover, .subject .value:hover, .gmail .value:hover {
      background: linear-gradient(90deg, #00b7eb, #90ee90);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 0 10px rgba(0, 183, 235, 0.8), 0 0 20px rgba(144, 238, 144, 0.5);
    }
    .versity .value::after, .subject .value::after, .gmail .value::after {
      content: '';
      position: absolute;
      width: 0;
      height: 1px;
      background: linear-gradient(90deg, #00b7eb, #90ee90);
      bottom: -2px;
      left: 0;
      transition: width 0.3s ease;
    }
    .versity .value:hover::after, .subject .value:hover::after, .gmail .value:hover::after {
      width: 100%;
    }
    /* Search bar styles */
    .search-container {
      display: flex;
      justify-content: center;
      margin: 1.5rem 0;
      position: relative;
    }
    .search-bar {
      width: 100%;
      max-width: 500px;
      padding: 12px 40px 12px 40px;
      background: linear-gradient(135deg, #1a1a40, #2a2a60);
      border: 1px solid #00b7eb;
      border-radius: 8px;
      color: #fff;
      font-size: 1rem;
      font-family: 'Poppins', sans-serif;
      transition: all 0.3s ease;
      box-shadow: 0 0 10px rgba(0, 183, 235, 0.3);
    }
    .search-bar:focus {
      outline: none;
      transform: scale(1.05);
      box-shadow: 0 0 15px rgba(0, 183, 235, 0.5);
      border-color: #90ee90;
    }
    .search-icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-50%);
      width: 20px;
      height: 20px;
      fill: #00b7eb;
      transition: transform 0.3s ease;
    }
    .search-icon:hover {
      transform: translateY(-50%) scale(1.2);
    }
    .clear-btn {
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
      background: none;
      border: none;
      color: #90ee90;
      font-size: 1.2rem;
      cursor: pointer;
      display: none;
      transition: transform 0.3s ease;
    }
    .clear-btn:hover {
      transform: translateY(-50%) scale(1.2);
    }
    .suggestions {
      position: absolute;
      top: 100%;
      left: 50%;
      transform: translateX(-50%);
      width: 100%;
      max-width: 500px;
      background: linear-gradient(135deg, #1a1a40, #2a2a60);
      border-radius: 8px;
      box-shadow: 0 4px 15px rgba(0, 183, 235, 0.3);
      max-height: 200px;
      overflow-y: auto;
      z-index: 10;
      display: none;
    }
    .suggestion-item {
      padding: 10px;
      color: #ddd;
      cursor: pointer;
      display: flex;
      align-items: center;
      transition: background 0.2s ease;
    }
    .suggestion-item:hover {
      background: rgba(0, 183, 235, 0.2);
    }
    .suggestion-icon {
      width: 16px;
      height: 16px;
      margin-right: 10px;
      fill: #00b7eb;
    }
    .highlight {
      background: linear-gradient(90deg, #00b7eb, #90ee90);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
    .no-results {
      text-align: center;
      color: #ddd;
      margin: 2rem 0;
      font-size: 1.2rem;
      opacity: 0;
      animation: fadeIn 0.5s forwards;
    }
    .result-count {
      text-align: center;
      color: #00b7eb;
      margin: 1rem 0;
      font-size: 1rem;
      opacity: 0;
      animation: fadeIn 0.5s forwards;
    }
    .filter-btn {
      margin-left: 10px;
      padding: 12px;
      background: linear-gradient(135deg, #00b7eb, #90ee90);
      border: none;
      border-radius: 8px;
      color: #fff;
      font-family: 'Poppins', sans-serif;
      cursor: pointer;
      transition: transform 0.3s ease;
    }
    .filter-btn:hover {
      transform: scale(1.05);
    }
    @media (max-width: 600px) {
      .search-bar {
        max-width: 100%;
      }
      .suggestions {
        max-width: 100%;
      }
      .card {
        padding: 0.5rem;
      }
      .name {
        font-size: 1rem;
      }
      .bio {
        font-size: 0.9rem;
      }
      .versity {
        font-size: 0.85rem;
      }
      .subject  {
        font-size: 0.8rem;
      }
      .gmail {
        font-size: 0.75rem;
      }
      .versity .icon, .subject .icon, .gmail .icon {
        width: 14px;
        height: 14px;
      }
    }
  </style>
</head>
<body>
  <div class="watermark-container" id="watermark-container">
    <img src="https://i.ibb.co.com/S4R68MxP/Chat-GPT-Image-Sep-27-2025-10-42-56-PM.png" alt="BGC Watermark" class="watermark">
  </div>
  <h1>HSC 24  | BGC </h1>
  <div class="search-container">
    <svg class="search-icon" viewBox="0 0 24 24"><path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/></svg>
    <input type="text" class="search-bar" placeholder="Search by name, versity, subject ...">
    <button class="clear-btn">✕</button>
    <button class="filter-btn">Filter</button>
    <div class="suggestions"></div>
  </div>
  <div class="result-count"></div>
  <div class="no-results" style="display: none;">No results found</div>





<marquee>
  <i>
    <h4>
      Please tap on the pictures to visit their Facebook profiles
    </h4>
  </i>
</marquee>








  <div class="grid">


    <div id="206" class="card">
      <div class="image-container">
        <a href="https://www.facebook.com/utsabbin1233" target="_blank">
          <img src="https://i.ibb.co.com/cKp8dJ07/utsab-photo.jpg" alt="Utsab">
        </a>
        <span class="author-label">Author</span>
      </div>
      <div class="name">Utsab Bin Ali</div>
      <div class="bio"> BGC Roll : 1202223010066</div>
      <div class="versity">
        <svg class="icon" viewBox="0 0 24 24">
  <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
</svg>

        <span class="value"> Rajshahi University of Engineering and Technology-RUET   </span>
      </div>
      <div class="subject">
        <svg class="icon" viewBox="0 0 24 24">
  <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
</svg>

        <span class="value"> Mechanical Engineering ( ME )</span>
      </div>
      <div class="gmail">
        <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
        <span class="value">utsaabbinali@gmail.com</span>
      </div>
    </div>
    
        <div id="146" class="card">
      <div class="image-container">
        <a href="https://www.facebook.com/mdiks23" target="_blank">
 <img src="https://i.ibb.co.com/JWQkRPV0/img1-removebg-preview.png" alt="img1-removebg-preview" border="0" />
        </a>
        <span class="author-label">Author</span>
      </div>
      <div class="name">Md. Imtiaz Khondokar Supto </div>
      <div class="bio"> BGC Roll : 1202223010002</div>
      <div class="versity">
        <svg class="icon" viewBox="0 0 24 24">
  <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
</svg>

        <span class="value">Bangladesh Agricultural University ( BAU )   </span>
      </div>
      <div class="subject">
        <svg class="icon" viewBox="0 0 24 24">
  <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
</svg>

        <span class="value">Agricultural Engineering & Technology ( AET )</span>
      </div>
      <div class="gmail">
        <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
        <span class="value">mdiks23@gmail.com</span>
      </div>
    </div>
    

<div id="153" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/16s5v1EVcE/" target="_blank">
<img src="https://i.ibb.co.com/cSXS1Kb8/IMG-20250928-WA0002.jpg" alt="IMG-20250928-WA0002" border="0">
    </a>
  </div>
  <div class="name">MD.Tanvir Hasan</div>
  <div class="bio">BGC Roll : 1202223010016</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jashore University of Science and Technology [4]</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Chemical Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">tanvirhasan10016@gmail.com</span>
  </div>
</div>


<div id="148" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/17TimQ92mc/ " target="shajeeb">
      <img src="https://i.ibb.co.com/pjBQ92gK/inbound706371990528984711.jpg">
    </a>
  </div>
  <div class="name">MD. NAHIDUL ISLAM SHAJEEB</div>
  <div class="bio">BGC Roll : 1202223010059</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">CUET</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Civil engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">shajeebbhuiyan44@gmail.com</span>
  </div>
</div>


<div id="150" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/profile.php?id=61557478753043" target="_blank">
      <img src="https://i.ibb.co.com/jPt38KG2/IMG-20250928-WA0007.jpg">
    </a>
  </div>
  <div class="name">Md. Rajib Khan</div>
  <div class="bio">BGC Roll : 1202223020302</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Shahjalal University of Science and Technology, SUST</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Public Administration</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">rajibkhan643823@gmail.com</span>
  </div>
</div>



    
<div id="101" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Ahnaf Tahmid</div>
  <div class="bio">BGC Roll : 1202223010207</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Bangla</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">tahmidahnaf087@gmail.com</span>
  </div>
</div>

<div id="102" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Akayed Evan Ali Mollah</div>
  <div class="bio">BGC Roll : 1202223010392</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Rajshahi University of Engineering and Technology</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">EEE</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">akayedevna@gmail.com</span>
  </div>
</div>

<div id="103" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Ali Islam</div>
  <div class="bio">BGC Roll : 1202223010250</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Sylhet Agricultural University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Agriculture</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">aliislammd642@gmail.com</span>
  </div>
</div>

<div id="104" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Amena Khanom Nipa</div>
  <div class="bio">BGC Roll : 1202223020011</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Noakhali Science and Technology University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Political Science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">amenakhanomnipa@gmail.com</span>
  </div>
</div>

<div id="105" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="https://i.ibb.co.com/7J1PTRjq/Messenger-creation-23-E01-D7-B-050-A-4024-B77-D-5-ED12-C53-A4-BF.jpg">
    </a>
  </div>
  <div class="name">Anayet Ul Hai</div>
  <div class="bio">BGC Roll : 1202223010354</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Gopalgonj University of Science Technology </span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Fisheries</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">mahfuzulhai@gmail.com</span>
  </div>
</div>

<div id="106" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1CM8LWvPt6/?mibextid=wwXIfr " target="ariful">
      <img src="https://i.ibb.co.com/cSZL1pj4/IMG-20250427-WA0050-edit-4455713977475845.jpg">
    </a>
  </div>
  <div class="name">Ariful Islam Chayon</div>
  <div class="bio">BGC Roll : 1202223020303</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Political Science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">arifulislamchayon539@gmail.com</span>
  </div>
</div>

<div id="107" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/asadulislamfahim.11?mibextid=ZbWKwL" target="fahim">
      <img src="https://i.ibb.co.com/vxXcwV61/inbound303748181540539211-Asadul-Islam-Fahim.jpg">
    </a>
  </div>
  <div class="name">Asadul Islam Fahim</div>
  <div class="bio">BGC Roll : 1202223010341</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">University of Rajshahi</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Economics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">asadulislamfahim05@gmail.com</span>
  </div>
</div>

<div id="108" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/natsa.mim.9?mibextid=ZbWKwL" target="_blank"><img src="https://i.ibb.co.com/X6FF17G/IMG-20250928-WA0004.jpg"></a>
  </div>
  <div class="name">Aysha Maria</div>
  <div class="bio">BGC Roll : 1202223030017</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Management</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">aysha-31st-2024713038@mgt.du.ac.bd</span>
  </div>
</div>

<div id="109" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Azizul Hakim Mahabi Mridha</div>
  <div class="bio">BGC Roll : 1202223020187</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Shahjalal University of Science and Technology</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Public Administration</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">azizulmahabi@gmail.com</span>
  </div>
</div>

<div id="110" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Bonna Srabonti</div>
  <div class="bio">BGC Roll : 1202223030153</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Marketing</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">bonnasrabonti52@gmail.com</span>
  </div>
</div>

<div id="111" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/17C1PbY2Yo/" target="_blank"><img src="https://i.ibb.co.com/gFy5jbt3/IMG-20250928-WA0003.jpg"></a>
  </div>
  <div class="name">Bosrat Jahan Omra</div>
  <div class="bio">BGC Roll : 1202223010025</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Mawlana Bhasani Science and Technology University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Food Technology and Nutritional Science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">bosratjahanomra@gmail.com</span>
  </div>
</div>

<div id="112" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Eirtija Jannat Mrittika</div>
  <div class="bio">BGC Roll : 1202122010211 (HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Pharmacy</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">eirtijamrittika2020@gmail.com</span>
  </div>
</div>

<div id="113" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Ema Hossain</div>
  <div class="bio">BGC Roll : 1202223010221</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Bangladesh Agricultural University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Agricultural Engineering & Technology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">emahossain2006@gmail.com</span>
  </div>
</div>

<div id="114" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Esrat Jahan Mysha</div>
  <div class="bio">BGC Roll : 1202223010039</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">SOMC</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">MBBS</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">nasrinajom20@gmail.com</span>
  </div>
</div>

<div id="115" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/efran.sarker.5"_blank"><img src=""></a>
  </div>
  <div class="name">Eusuf Sorkar</div>
  <div class="bio">BGC Roll : 1202223010104</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Rajshahi</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Material Science and Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">eusufsarker32@gmail.com</span>
  </div>
</div>

<div id="116" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Fariha Khanom Jeny</div>
  <div class="bio">BGC Roll : 1202223020188</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Social Welfare and Research</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">syedrezaulkamalwasim@gmail.com</span>
  </div>
</div>

<div id="117" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/19wdBdj8fZ/" target="Fouzia"><img src="https://i.ibb.co.com/FqLYcwBH/inbound6677495503317876353.jpg"></a>
  </div>
  <div class="name">Fouzia Akter</div>
  <div class="bio">BGC Roll : 1202223020147</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Shahjalal University of Science & Technology, Sylhet</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Social Work</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">fa4768118@gmail.com</span>
  </div>
</div>

<div id="118" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Ifrana Akter</div>
  <div class="bio">BGC Roll : 1202223010153</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Shahjalal University of Science & Technology</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Economics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">ifranaakter84@gmail.com</span>
  </div>
</div>

<div id="119" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Iqbal Hossen Ripon</div>
  <div class="bio">BGC Roll : 1202223030030</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Tourism and Hospitality Management</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">iqbalripon18@gmail.com</span>
  </div>
</div>

<div id="120" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Israt Jahan Saila</div>
  <div class="bio">BGC Roll : 1202223010057</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Bangla</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">salmarahman5081@gmail.com</span>
  </div>
</div>

<div id="121" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Jakia Rahman Arno</div>
  <div class="bio">BGC Roll : 1202223010360</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jagannath University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Film and Television</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">jakiarahmanano12@gmail.com</span>
  </div>
</div>

<div id="122" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/simon50riyaz" target="_blank"><img src="https://i.ibb.co.com/RTKxPMRC/IMG-20250929-WA0018.jpg"></a>
  </div>
  <div class="name">Jannatul Haque</div>
  <div class="bio">BGC Roll : 1202122030163 (HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Noakhali Science and Technology University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Management Information Systems</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">haquejannatul202@gmail.com</span>
  </div>
</div>

<div id="123" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Jui Debnath</div>
  <div class="bio">BGC Roll : 1202223020146</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Japanese Studies</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">juid35482@gmail.com</span>
  </div>
</div>


<div id="124" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/kaniz.anie?mibextid=ZbWKwL" target="_blank"><img src="https://i.ibb.co.com/YFhzsB6d/IMG-20250928-WA0011.jpg"></a>
  </div>
  <div class="name">Kanij Rubaiya Kabir</div>
  <div class="bio">BGC Roll : 1202223010003</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jagannath University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Law</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">anieahmed73@gmail.com</span>
  </div>
</div>

<div id="125" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/19h6u9Ehn9/" target="_blank"><img src="https://i.ibb.co.com/8DkbvDZb/inbound2889906180935412048.jpg"></a>
  </div>
  <div class="name">Kaynat Akter Shayla</div>
  <div class="bio">BGC Roll : 1202223010230</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Sylhet MAG Osmani Medical College</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">MBBS</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">shaylakaynat70@gmail.com</span>
  </div>
</div>

<div id="126" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Kazi Iftekhar Uz Zaman</div>
  <div class="bio">BGC Roll : 1202223010321</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Mathematics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">kaziiftekhar03@gmail.com</span>
  </div>
</div>

<div id="127" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1C5mAfLody/" target="_blank"><img src="https://i.ibb.co.com/XfRnVSxQ/inbound5284689641391871095-Lubna-Rahman-Raufa.jpg"></a>
  </div>
  <div class="name">Lubna Rahman Raufa</div>
  <div class="bio">BGC Roll : 1202223010150</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Political Science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">lubnarahmanraufa2024@gmail.com</span>
  </div>
</div>

<div id="128" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Mahbubur Rahman Khadem</div>
  <div class="bio">BGC Roll : 1202223021236</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Electrical and Electronics Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">mahbuburrahmankhadem@gmail.com</span>
  </div>
</div>


<div id="129" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1BczBhevvX/" target="mahia"><img src="https://i.ibb.co.com/Hfv4Wd72/inbound2736987000851740222.jpg"></a>
  </div>
  <div class="name">Mahia Islam</div>
  <div class="bio">BGC Roll : 1202223095</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">BUET</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Civil</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">islammahia2005@gmail.com</span>
  </div>
</div>

<div id="130" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Mahima Chowdhury Moon</div>
  <div class="bio">BGC Roll : 1202223010281</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Cumilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Chemistry</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">mahima.chowdhury.moon11@gmail.com</span>
  </div>
</div>

<div id="131" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Mahir Hasan</div>
  <div class="bio">BGC Roll : 1202223010138</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Geography and Environmental Studies</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">mahir.hasan1907@gmail.com</span>
  </div>
</div>

<div id="132" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/19zQSJPSDK/" target="_blank"><img src="https://i.ibb.co.com/LDJS12My/IMG-20250928-WA0019.jpg"></a>
  </div>
  <div class="name">Maria Nidhi Ema</div>
  <div class="bio">BGC Roll : 1202223010068</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Chandpur Science & Technology University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">CSE</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">nidhiema@gmail.com</span>
  </div>
</div>


<div id="133" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/profile.php?id=61555706177868" target="_blank">
      <img src="https://i.ibb.co.com/rKbkQrkM/IMG-20250928-WA0001.jpg" alt="IMG-20250928-WA0001" border="0">
      
    </a>
  </div>
  <div class="name">Marzia Akter Tayeba</div>
  <div class="bio">BGC Roll : 1202223020141</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Mass Communication and Journalism</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">marziaakter689@gmail.com</span>
  </div>
</div>

<div id="134" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/16JYQD3EHY/" target="tara"><img src="https://i.ibb.co.com/BVR0KFNN/IMG-20250331-WA0242.jpg"></a>
  </div>
  <div class="name">Masarat Tara</div>
  <div class="bio">BGC Roll : 1202223010042</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Chittagong University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Oceanography</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">taramasarat25@gmail.com</span>
  </div>
</div>

<div id="135" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Masuma Jannat</div>
  <div class="bio">BGC Roll : 1202223020122</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Cumilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Mass Communication and Journalism</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">masujannat0@gmail.com</span>
  </div>
</div>

<div id="136" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank"><img src=""></a>
  </div>
  <div class="name">Mayeda Islam Adiba</div>
  <div class="bio">BGC Roll : 1202223021072</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24"><path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/></svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24"><path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/></svg>
    <span class="value">Computer Science and Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
    <span class="value">fatemabegum22233@gmail.com</span>
  </div>
</div>

<div id="137" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Md Abdul Wadud Bin Alamgir</div>
  <div class="bio">BGC Roll : 1202223010271</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Bangladesh University of Professionals - BUP</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Environmental Science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">abirwadud36@gmail.com</span>
  </div>
</div>

<div id="138" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Md Afif Bhuiyan</div>
  <div class="bio">BGC Roll : 1202223030016</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka Central University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Finance & Banking</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">afifbhuiyan06@gmail.com</span>
  </div>
</div>

<div id="139" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">MD AKRAM HOSSEN</div>
  <div class="bio">BGC Roll : 12022230100106</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Gopalgonj medical college</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">MBBS</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">akramhossen814365@gmail.com</span>
  </div>
</div>

<div id="140" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/meAyonn" target="ayon">
      <img src="https://i.ibb.co.com/twwtVDzd/IMG-20250403-050016-759.jpg">
    </a>
  </div>
  <div class="name">MD AL-AMIN MIAH AYON</div>
  <div class="bio">BGC Roll : 1202223010233</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Rajshahi</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Geology and Mining</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">ayonk651@gmail.com</span>
  </div>
</div>

<div id="141" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/19vuVZz2ut/?mibextid=wwXIfr" target="_blank">
      <img src="https://i.ibb.co.com/twR8BBCQ/IMG-20251001-WA0006.jpg">
    </a>
  </div>
  <div class="name">Md Ayman Ahmed</div>
  <div class="bio">BGC Roll : 1202223030258</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Psychology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">md3317520@gmail.com</span>
  </div>
</div>

<div id="142" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Md Bayjid</div>
  <div class="bio">BGC Roll : 1202223020300</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">English</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">rajibkhan643823@gmail.com</span>
  </div>
</div>

<div id="143" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/19cSLraLWb/" target="ikram">
      <img src="https://i.ibb.co.com/67zkyLBt/IMG-20240629-WA0004.jpg">
    </a>
  </div>
  <div class="name">Md Ikram Hossain</div>
  <div class="bio">BGC Roll : 1202122010286(HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">SUST</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Physics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">ikramsharifpur@gmail.com</span>
  </div>
</div>

<div id="144" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1BQxDRExUx/" target="raihan">
      <img src="https://i.ibb.co.com/WvZBc6Nh/inbound3324009164381512669.jpg">
    </a>
  </div>
  <div class="name">Md Raihan Sarkar</div>
  <div class="bio">BGC Roll : 1202223010273</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">SUST</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Software Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">raihansharkar58@gmail.com</span>
  </div>
</div>

<div id="145" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/abdur.rahman.954206" target="_blank">
      <img src="https://i.ibb.co.com/mnyVhv9/IMG-20250922-WA0004.jpg">
    </a>
  </div>
  <div class="name">Md. Abdur Rahman Mridha</div>
  <div class="bio">BGC Roll : 1202223010123</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jagannath University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Pharmacy</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">rakibmridha1234@gmail.com</span>
  </div>
</div>



<div id="147" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/mohtasimalsiam" target="_blank">
      <img src="https://i.ibb.co.com/r2tV51dq/IMG-20250723-160609.jpg">
    </a>
  </div>
  <div class="name">MD. MAHIN MIA</div>
  <div class="bio">BGC Roll : 1202223010089</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Chemistry</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mohtasimalsiammahin@gmail.com</span>
  </div>
</div>



<div id="149" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/175QuADQth/" target="rafid">
      <img src="https://i.ibb.co.com/N2ssLCgx/inbound2115158303704894223.jpg">
    </a>
  </div>
  <div class="name">Md. Rafid Ashraf</div>
  <div class="bio">BGC Roll : 1202223010346</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Political Science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">md.rafidashraf14063@gmail.com</span>
  </div>
</div>

<div id="151" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1BPj4H7yVm/" target="_blank">
      <img src="https://i.ibb.co.com/gZ2ZYsdL/IMG-20250928-WA0009.jpg">
    </a>
  </div>
  <div class="name">Md. Samir Ahammed</div>
  <div class="bio">BGC Roll : 1202223020082</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Information Science & Library Management</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mdsamirahammed@outlook.com</span>
  </div>
</div>
<div id="152" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/19pB9ZsF4i/" target="_blank">
      <img src="https://i.ibb.co.com/G46Dkg0t/IMG-20250928-WA0005.jpg">
    </a>
  </div>
  <div class="name">Md.Naimul Islam</div>
  <div class="bio">BGC Roll : 1202223010101</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Cumilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Statistics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">naiema53@gmail.com</span>
  </div>
</div>

<div id="154" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Miftahul Jannat</div>
  <div class="bio">BGC Roll : 1202223010028</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Chittagong veterinary science & technology</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Fisheries</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">jannatmuftahul124@gmail.com</span>
  </div>
</div>
<div id="155" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Mobina Islam</div>
  <div class="bio">BGC Roll : 1202223020232</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">CU</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Philosophy</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mobinaislam310@gmail.com</span>
  </div>
</div>
<div id="156" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Mobina Islam</div>
  <div class="bio">BGC Roll : 1202223020232</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">CU</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Philosophy</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mobinaislam310@gmail.com</span>
  </div>
</div>
<div id="157" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Mohammad Kobul Hasan</div>
  <div class="bio">BGC Roll : 1202223020209</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jagannath University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Law & Land Administration</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">kobulofficial2006@gmail.com</span>
  </div>
</div>
<div id="158" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/mozabbidrahan" target="sabit">
      <img src="https://i.ibb.co.com/5ddzc5X/IMG-20250928-WA0008.jpg">
    </a>
  </div>
  <div class="name">Mozabbid Rahan Sabit</div>
  <div class="bio">BGC Roll : 1202223010119</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jagannath University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Chemistry</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sabitmozabbid456@gmail.com</span>
  </div>
</div>
<div id="159" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Ms.Masuma Akter</div>
  <div class="bio">BGC Roll : 1202223010234</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Sylhet Agricultural University, Sylhet</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Agriculture</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">masuma464344@gmail.com</span>
  </div>
</div>
<div id="160" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Mst Sadia Akhter</div>
  <div class="bio">BGC Roll : 1202223020205</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Cumilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Economics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sadiajahan7889@gmail.com</span>
  </div>
</div>
<div id="161" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/sanjida.akter.904770?mibextid=ZbWKwL" target="Sanjida ">
      <img src="https://i.ibb.co.com/WWqvYB7q/MEITU-20250726-202629107.jpg">
    </a>
  </div>
  <div class="name">Mst Sanjida Akter</div>
  <div class="bio">BGC Roll : 1202223020158</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Sociology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mdmohosinmiah67@gmail.com</span>
  </div>
</div>
<div id="162" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1K2WvBWVG3/" target="_blank">
      <img src="https://i.ibb.co.com/twRMFxbn/inbound5256555878240156290.jpg">
    </a>
  </div>
  <div class="name">Mst. Nusrat Jahan Shefa</div>
  <div class="bio">BGC Roll : 1202223010166</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Women and Gender Studies</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">nusratshefa8@gmail.com</span>
  </div>
</div>
<div id="163" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1aXXF5xnXC/"_blank">
<img src="https://i.ibb.co.com/GvWS7WN7/IMG-20250928-WA0000.jpg" alt="IMG-20250928-WA0000" border="0">
    </a>
  </div>
  <div class="name">Mst.Sadia Islam Jannat</div>
  
  <div class="bio">BGC Roll : 1202223020166</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Shajalal University of science and technology</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">BBA</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">s92947311@gmail.com</span>
  </div>
</div>
<div id="164" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/2muskaan.khan" target="muskan">
      <img src="https://i.ibb.co.com/6cHMvgwv/inbound1735585082632298658.jpg">
    </a>
  </div>
  <div class="name">Muskan</div>
  <div class="bio">BGC Roll : 1202223030112</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jagannath University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Marketing</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">muskankhan200531@gmail.com</span>
  </div>
</div>
<div id="165" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Myesha moni Methila</div>
  <div class="bio">BGC Roll : 1202122022098(HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Public administration</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">myeshamethila444@gmail.com</span>
  </div>
</div>
<div id="166" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Mysha Akter</div>
  <div class="bio">BGC Roll : 1202223010141 </div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Sylhet Agricultural University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Fisheries</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">myshaakter926@gmail.com</span>
  </div>
</div>
<div id="167" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/anonna.zaman.2025" target="Anonna">
      <img src="https://i.ibb.co.com/Z1mmDpWH/inbound2808694141007319129.jpg">
    </a>
  </div>
  <div class="name">Nadia Zaman Anonna</div>
  <div class="bio">BGC Roll : 1202223020127</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Islamic Studies</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">nadiazaman452@gmail.com</span>
  </div>
</div>
<div id="168" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/nadiatul.nira.1" target="nira">
      <img src="https://i.ibb.co.com/nMvZQGfV/20240129-011336-2.jpg">
    </a>
  </div>
  <div class="name">Nadiatul Nira</div>
  <div class="bio">BGC Roll : 1202223010067</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Chittagong University of Engineering & Technology (CUET)</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Civil Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">nadiatulnira4@gmail.com</span>
  </div>
</div>
<div id="169" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Nahida Akter</div>
  <div class="bio">BGC Roll : 1202223030075</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">CoU</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Marketing</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">na3669050@gmail.com</span>
  </div>
</div>
<div id="170" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Nahifa Khandaker</div>
  <div class="bio">BGC Roll : 1202223030157</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">RUB</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Sociology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">nahifakhandakar01@gmail.com</span>
  </div>
</div>
<div id="171" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Nawshin Nawal</div>
  <div class="bio">BGC Roll : 1202223010149</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Sylhet Agricultural University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Agricultural economics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">nawalnawshin199@gmail.com</span>
  </div>
</div>
<div id="172" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1Cc9gwpTV9/" target="nitita">
      <img src="https://i.ibb.co.com/99wTXDzP/IMG-20250929-WA0001.jpg">
    </a>
  </div>
  <div class="name">Nitita</div>
  <div class="bio">BGC Roll : 1202223030070</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Accounting and Information Systems</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mi6924878@gmail.com</span>
  </div>
</div>





<div id="173" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1Cx9eNNzZG/" target="tashfia">
      <img src="https://i.ibb.co.com/S4cCLJ1r/20250604-152725.jpg">
    </a>
  </div>
  <div class="name">Nusrat Jahan Tasfia</div>
  <div class="bio">BGC Roll : 1202223010040</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">BUET</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">IPE</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">tasfia0245@gmail.com</span>
  </div>
</div>
<div id="174" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Nusrat kabir buli</div>
  <div class="bio">BGC Roll : 1202223020248</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Fine Arts</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">n14647304@gmail.com</span>
  </div>
</div>
<div id="175" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Pakhiya Akter</div>
  <div class="bio">BGC Roll : 1202223030160</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jahangirnaghar University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Management</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">pakhiya174@gmail.com</span>
  </div>
</div>
<div id="176" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Papia Sultana</div>
  <div class="bio">BGC Roll : 1202223010129</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Noakhali Science and Technology University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Physics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sultanapapia221@gmail.com</span>
  </div>
</div>
<div id="177" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Rahatul Islam Sami</div>
  <div class="bio">BGC Roll : 1202223020240</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">DIS</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">rahatulislamsami1@gmail.com</span>
  </div>
</div>
<div id="178" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Raj Mukut Talukder</div>
  <div class="bio">BGC Roll : 1202122010137(HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Shahjalal University of science and technology</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Political studies</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mukuttalukder3888@gmail.com</span>
  </div>
</div>
<div id="179" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Ramisa Ahmed</div>
  <div class="bio">BGC Roll : 1202223010224</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jamalpur Medical College, Jamalpur</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">MBBS</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">ramisaahmed4012@gmail.com</span>
  </div>
</div>
<div id="180" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Refadul Islam</div>
  <div class="bio">BGC Roll : 1202223030198</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">International business (IB)</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">rjrefad76@gmail.com</span>
  </div>
</div>
<div id="181" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Sabrin Saka Nourin</div>
  <div class="bio">BGC Roll : 1202223010099</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Anthropology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sabrinsakanourin@gmail.com</span>
  </div>
</div>
<div id="182" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/17S4jDe6d3/" target="sabuj">
      <img src="https://i.ibb.co.com/vvs9zKsM/rsz-11000000734-removebg-preview.jpg">
    </a>
  </div>
  <div class="name">SABUJ MIAH</div>
  <div class="bio">BGC Roll : 1202223010303</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Sher-e Bangla agriculture university</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Agriculture</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">duvoahmed@gmail.com</span>
  </div>
</div>
<div id="183" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Sadia Afrose Lisa</div>
  <div class="bio">BGC Roll : 1202223010168</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Sylhet MAG Osmani Medical college</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">MBBS</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sadiaafroselisa20@gmail.com</span>
  </div>
</div>
<div id="184" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1JyEqMt5R1/" target="_blank">
      <img src="https://i.ibb.co.com/zVNK7QYf/IMG-20250929-WA0007.jpg">
    </a>
  </div>
  <div class="name">Sadia Akter</div>
  <div class="bio">BGC Roll : 1202223030069</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Cumilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Management</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">supnilakash2@gmail.com</span>
  </div>
</div>
<div id="185" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Sadia Hossain Suchi</div>
  <div class="bio">BGC Roll : 1202223010130</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Chemistry</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">suchi162006@gmail.com</span>
  </div>
</div>
<div id="186" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/samia.rahman.803553" target="sadia">
      <img src="">
    </a>
  </div>
  <div class="name">Sadia Mehrin</div>
  <div class="bio">BGC Roll : 1202223010056</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Physics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sadiamehrin22052006@gmail.com</span>
  </div>
</div>
<div id="187" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Sadia Sultana Iqra</div>
  <div class="bio">BGC Roll : 1202223010280</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Department of Soil, Water And Environment</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sadiasultanaiqra@gmail.com</span>
  </div>
</div>
<div id="188" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Safa binte sayed</div>
  <div class="bio">BGC Roll : 1202122010249(HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">GST university</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Animal science and veterinary medicine</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">s09695860@gmail.com</span>
  </div>
</div>
<div id="189" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Sakibul Hoque Shourov</div>
  <div class="bio">BGC Roll : 1202223030287</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University Of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">International Business</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sakibulshourov5@gmail.com</span>
  </div>
</div>
<div id="190" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Samia Anowar</div>
  <div class="bio">BGC Roll : 1202223020052</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Philosophy</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">saritu2932@gmail.com</span>
  </div>
</div>
<div id="191" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Samia Rahman</div>
  <div class="bio">BGC Roll : 1202223020079</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jahangirnagar University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Archaeology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">rahmansamia1120@gmail.com</span>
  </div>
</div>
<div id="192" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/sanjida.ritu.48861" target="_blank">
      <img src="https://i.ibb.co.com/5xthCjFH/inbound4171744241714057701.jpg">
    </a>
  </div>
  <div class="name">Sanjida Akther Ritu</div>
  <div class="bio">BGC Roll : 1202223020143</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Sociology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sanjidaritu32@gmail.com</span>
  </div>
</div>
<div id="193" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/sazzad7017/" target="sazzad">
      <img src="https://i.ibb.co.com/ym3V66JZ/IMG-3391-Sazzad-Chowdhury.jpg">
    </a>
  </div>
  <div class="name">Sazzad Chowdhury</div>
  <div class="bio">BGC Roll : 1202223010135</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">SUST</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Physics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">csazzad912@gmail.com</span>
  </div>
</div>
<div id="194" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Shahidul Alam Shawon</div>
  <div class="bio">BGC Roll : 1202223020016</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">History</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mdrabbirhosain13@gmail.com</span>
  </div>
</div>
<div id="195" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Shahnawaz Khandaker</div>
  <div class="bio">BGC Roll : 1202223030145</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Finance and banking</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">shanewazkhandakar@gmail.com</span>
  </div>
</div>
<div id="196" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/15cudqeDQA/" target="_blank">
      <img src="https://i.ibb.co.com/SwGTZqxH/default-profile-account-unknown-icon-black-silhouette-free-vector.jpg">
    </a>
  </div>
  <div class="name">Sinthia Akter Tamanna</div>
  <div class="bio">BGC Roll : 1202223010047</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Chittagong University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Oceanography</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sinthias849@gmail.com</span>
  </div>
</div>
<div id="197" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/17Ffkq2Q4X/" target="sohel">
      <img src="https://i.ibb.co.com/rf46Dt3f/inbound2493966781940740346.jpg">
    </a>
  </div>
  <div class="name">Sohel Khan </div>
  <div class="bio">BGC Roll : 1202223020015</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Dhaka</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Mass Communication And Jurnalism</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">khansohel2980@gmail.com</span>
  </div>
</div>
<div id="198" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Sumaiya Akter</div>
  <div class="bio">BGC Roll : 1202223010236</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla university</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Physics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sumaiyaafrinsumaiya48@gmail.com</span>
  </div>
</div>








<div id="199" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/sumayyah.rupa?mibextid=wwXIfr&mibextid=wwXIfr" target="rupa">
      <img src="https://i.ibb.co.com/1tBqW3Yq/IMG-1056-Sumaiya-Rupa.jpg">
    </a>
  </div>
  <div class="name">Sumaiya Khandaker Rupa</div>
  <div class="bio">BGC Roll : 1202223020124</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Health economics</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sumaiyarupa608@gmail.com</span>
  </div>
</div>

<div id="200" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/arman.mahi.919516" target="mahi">
      <img src="https://i.ibb.co.com/bg8J3XNV/inbound5424008970144792545.jpg">
    </a>
  </div>
  <div class="name">Syed Arman Mahi</div>
  <div class="bio">BGC Roll : 12022230235</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">RUET</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Chemical Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">armanmahi06@gmail.com</span>
  </div>
</div>

<div id="201" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">SYEDA SARIKA SARIA</div>
  <div class="bio">BGC Roll : 1202223010100</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">University of Chittagong</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Soil science</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mdzahir908070@gmail.com</span>
  </div>
</div>

<div id="202" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Tarak Ahammed</div>
  <div class="bio">BGC Roll : 1202223010355</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Jahangirnagar University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Environmental Sciences</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">mohtasimalsiammahin@gmail.com</span>
  </div>
</div>


<div id="203" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/tasnia.nowshad.prapti?mibextid=ZbWKwL" target="prapti">
      <img src="https://i.ibb.co.com/xSxP9y5r/IMG-20250414-WA0083.jpg">
    </a>
  </div>
  <div class="name">Tasnia Nowshad Prapti</div>
  <div class="bio">BGC Roll : 1202223010167</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Cumilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Law</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">tasnianowshadprapti@gmail.com</span>
  </div>
</div>

<div id="204" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Trisha Banik</div>
  <div class="bio">BGC Roll : 1202223010171</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Gazipur Agricultural University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Agricultural & Bioresources Engineering</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">trishabanik192615@gmail.com</span>
  </div>
</div>

<div id="205" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Umme Karima</div>
  <div class="bio">BGC Roll : 1202223020004</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">GST (Comilla University)</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Anthropology</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">ummekarima959@gmail.com</span>
  </div>
</div>



<div id="207" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Wakib Ahmed</div>
  <div class="bio">BGC Roll : 1202223010052</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">CUET</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">EEE</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">u2402002@student.cuet.ac.bd</span>
  </div>
</div>
<div id="208" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">Yusuf Abdulla Aliyan</div>
  <div class="bio">BGC Roll : 1202223020308</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Information Science and Library Management</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">abdullahaliyan2606@gmail.com</span>
  </div>
</div>
<div id="209" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1A3unM7Ruq/" target="_blank">
      <img src="https://i.ibb.co.com/Z1vFTs01/IMG-20250928-131608.jpg">
    </a>
  </div>
  <div class="name">Zannatul Maowa Dolon</div>
  <div class="bio">BGC Roll : 1202223010324</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Dhaka University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Graphic Design</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">zannatuldolon@gmail.com</span>
  </div>
</div>
<div id="210" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/" target="_blank">
      <img src="">
    </a>
  </div>
  <div class="name">নাজিফা জাহান প্রজ্ঞা</div>
  <div class="bio">BGC Roll : 1202122010001(HSC-2023)</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">CSE(Computer Science and Engineering)</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">nazifajahanp@gmail.com</span>
  </div>
</div>
<div id="211" class="card">
  <div class="image-container">
    <a href="https://www.facebook.com/share/1KvVN5fDs8/" target="_blank">
      <img src="https://i.ibb.co.com/s972x8mG/IMG-20250822-WA0003.jpg">
    </a>
  </div>
  <div class="name">সুফল আলম</div>
  <div class="bio">BGC Roll : 1202223030081</div>
  <div class="versity">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 9L3.74 9 12 5l8.26 4L12 12zm-6 4v2c0 2.21 3.58 4 8 4s8-1.79 8-4v-2l-8 3-8-3z"/>
    </svg>
    <span class="value">Comilla University</span>
  </div>
  <div class="subject">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M2 4v16c2-1.5 5-2 8-2s6 0.5 8 2V4c-2-1.5-5-2-8-2s-6 0.5-8 2zm8 0c2.5 0 5 .5 6 1.5v12c-1-.7-3.5-1.5-6-1.5s-5 .8-6 1.5v-12C5 4.5 7.5 4 10 4z"/>
    </svg>
    <span class="value">Accounting and Information Systems</span>
  </div>
  <div class="gmail">
    <svg class="icon" viewBox="0 0 24 24">
      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
    </svg>
    <span class="value">sofulalam720@gmail.com</span>
  </div>
</div>








</div>



  <script>
    // Particle effect for search bar
    const searchContainer = document.querySelector('.search-container');
    function createParticle() {
      const particle = document.createElement('div');
      particle.classList.add('water-particle');
      particle.style.left = `${Math.random() * 100}%`;
      particle.style.top = `${Math.random() * 100}%`;
      particle.style.background = '#00b7eb';
      searchContainer.appendChild(particle);
      setTimeout(() => particle.remove(), 1000);
    }

    // Collect data from cards
    const cards = document.querySelectorAll('.card');
    const searchData = [];
    cards.forEach((card, index) => {
      const name = card.querySelector('.name')?.textContent || '';
      const bio = card.querySelector('.bio')?.textContent || '';
      const versity = card.querySelector('.versity .value')?.textContent || '';
      const subject= card.querySelector('.subject .value')?.textContent || '';
      const gmail = card.querySelector('.gmail .value')?.textContent || '';
      searchData.push({
        index,
        name,
        bio,
        versity,
        subject,
        gmail
      });
    });

    const searchBar = document.querySelector('.search-bar');
    const clearBtn = document.querySelector('.clear-btn');
    const suggestions = document.querySelector('.suggestions');
    const resultCount = document.querySelector('.result-count');
    const noResults = document.querySelector('.no-results');
    const filterBtn = document.querySelector('.filter-btn');

    // Filter state
    let filterFields = ['name', 'bio', 'versity', 'subject', 'gmail'];

    // Toggle filter (for future enhancement)
    filterBtn.addEventListener('click', () => {
      alert('Filter feature: Toggle fields to search (e.g., Name, subject). Coming soon!');
    });

    function highlightText(text, query) {
      if (!query) return text;
      const regex = new RegExp(`(${query})`, 'gi');
      return text.replace(regex, '<span class="highlight">$1</span>');
    }

    function performSearch(query) {
      query = query.toLowerCase().trim();
      let matches = [];
      cards.forEach(card => card.classList.remove('matched'));
      suggestions.innerHTML = '';
      resultCount.textContent = '';
      noResults.style.display = 'none';

      if (query) {
        searchData.forEach(data => {
          filterFields.forEach(field => {
            if (data[field].toLowerCase().includes(query)) {
              matches.push({ ...data, field });
            }
          });
        });

        // Update suggestions
        if (matches.length) {
          suggestions.style.display = 'block';
          matches.forEach(match => {
            const item = document.createElement('div');
            item.classList.add('suggestion-item');
            const icon = document.createElement('svg');
            icon.classList.add('suggestion-icon');
            icon.setAttribute('viewBox', '0 0 24 24');
            icon.innerHTML = match.field === 'name' ? '<path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>' :
                            match.field === 'versity' ? '<path d="M12 2L2 12h3v8h14v-8h3L12 2zm0 2.83l6 6V18h-4v-4h-4v4H6v-7.17l6-6z"/>' :
                            match.field === 'subject' ? '<path d="M12 17.27l5.18 3.73-1.64-5.81L20 11.24l-6.18-.53L12 5l-1.82 5.71L4 11.24l4.46 3.95-1.64 5.81L12 17.27z"/>' :
                            match.field === 'gmail' ? '<path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>' :
                            '<path d="M4 4h16v12H4V4zm2 2v8h12V6H6z"/>';
            item.appendChild(icon);
            item.innerHTML += highlightText(match[match.field], query);
            item.addEventListener('click', () => {
              searchBar.value = match[match.field];
              performSearch(match[match.field]);
              suggestions.style.display = 'none';
            });
            suggestions.appendChild(item);
          });
        } else {
          suggestions.style.display = 'none';
        }

        // Update card visibility
        matches = [...new Set(matches.map(m => m.index))];
        matches.forEach(index => {
          cards[index].classList.add('matched');
          cards[index].style.display = 'block';
          cards[index].scrollIntoView({ behavior: 'smooth', block: 'center' });
        });
        cards.forEach((card, i) => {
          if (!matches.includes(i)) card.style.display = 'none';
        });

        // Update result count
        resultCount.textContent = matches.length ? `Found ${matches.length} result${matches.length > 1 ? 's' : ''} for "${query}"` : '';
        noResults.style.display = matches.length ? 'none' : 'block';
        clearBtn.style.display = 'block';
      } else {
        cards.forEach(card => {
          card.style.display = 'block';
          card.classList.remove('matched');
        });
        suggestions.style.display = 'none';
        clearBtn.style.display = 'none';
      }
    }

    searchBar.addEventListener('input', () => {
      performSearch(searchBar.value);
      createParticle();
    });

    searchBar.addEventListener('keypress', e => {
      if (e.key === 'Enter') {
        performSearch(searchBar.value);
        suggestions.style.display = 'none';
      }
    });

    clearBtn.addEventListener('click', () => {
      searchBar.value = '';
      performSearch('');
    });

    // Hide suggestions when clicking outside
    document.addEventListener('click', e => {
      if (!searchContainer.contains(e.target)) {
        suggestions.style.display = 'none';
      }
    });
  </script>




<div class="footer">
  <p>Developed by <span class="highlight">Utsab & Imtiaz</span></p>
</div>

<style>
.footer {
  text-align: center;
  padding: 1rem 0;
  margin-top: 2rem;
  background: linear-gradient(135deg, rgba(0, 183, 235, 0.2), rgba(144, 238, 144, 0.2));
  border: 2px solid #00b7eb;
  border-radius: 8px;
  box-shadow: 0 0 15px rgba(0, 183, 235, 0.5);
  animation: fadeIn 1s ease-in;
}
.footer p {
  margin: 0;
  font-size: 1.2rem;
  color: #fff;
  font-family: 'Poppins', sans-serif;
}
.footer .highlight {
  background: linear-gradient(90deg, #00b7eb, #90ee90);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: bold;
  text-shadow: 0 0 10px rgba(0, 183, 235, 0.8);
  transition: text-shadow 0.3s ease;
}
.footer .highlight:hover {
  text-shadow: 0 0 15px rgba(0, 183, 235, 1), 0 0 20px rgba(144, 238, 144, 0.8);
}
@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
</style>











</body>
</html>


