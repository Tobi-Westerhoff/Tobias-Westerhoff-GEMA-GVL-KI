# Tobias-Westerhoff-GEMA-GVL-KI
<!DOCTYPE html>
<html lang="de">
<head>
 <meta charset="UTF-8">
 <title>GEMA & GVL KI</title>
 <style>
   body {
     font-family: Arial, sans-serif;
     margin: 0;
     background-color: #f4f4f4;
     display: flex;
     flex-direction: column;
     align-items: center;
   }
   header {
     width: 100%;
     padding: 20px;
     text-align: right;
     font-size: 14px;
     color: #555;
     background: #fff;
     box-shadow: 0 2px 5px rgba(0,0,0,0.1);
   }
   h1 {
     margin-top: 80px;
   }
   input[type="text"] {
     width: 60%;
     max-width: 500px;
     padding: 12px 16px;
     font-size: 16px;
     border: 1px solid #ccc;
     border-radius: 24px;
   }
   button {
     padding: 10px 20px;
     margin-top: 20px;
     font-size: 16px;
     background-color: #1a73e8;
     color: white;
     border: none;
     border-radius: 24px;
     cursor: pointer;
   }
   .container {
     display: flex;
     flex-direction: row;
     justify-content: space-around;
     width: 90%;
     max-width: 1200px;
     margin-top: 50px;
   }
   .left, .right {
     flex: 1;
     padding: 30px;
     background-color: #fff;
     border-radius: 12px;
     margin: 10px;
     box-shadow: 0 0 10px rgba(0,0,0,0.05);
   }
   table {
     width: 100%;
     border-collapse: collapse;
     margin-top: 20px;
   }
   th, td {
     padding: 10px;
     border: 1px solid #ddd;
     text-align: center;
   }
   th {
     background-color: #1a73e8;
     color: white;
   }
   img {
     width: 200px;
     height: 200px;
     border-radius: 100px;
     object-fit: cover;
     margin-bottom: 20px;
   }
 </style>
</head>
<body>

 <header>Erstellt von Tobias Westerhoff</header>

 <h1>GEMA & GVL Analyse-KI</h1>
 <p>Füge hier einen YouTube- oder Spotify-Link ein:</p>
 <input id="linkInput" type="text" placeholder="https://open.spotify.com/track/...">
 <br>
 <button onclick="analyze()">Analyse starten</button>

 <div class="container" id="result" style="display:none;">
   <div class="left">
     <h2>Auswertung</h2>
     <table>
       <thead>
         <tr>
           <th>Land</th>
           <th>Plattform</th>
           <th>Streams</th>
           <th>€/Stream</th>
           <th>Einnahmen (€)</th>
         </tr>
       </thead>
       <tbody id="dataBody"></tbody>
     </table>
   </div>
   <div class="right">
     <img id="artistImage" src="" alt="Künstlerbild" />
     <h2 id="artistName">Künstlername</h2>
     <p><strong>Bürgerlicher Name:</strong> <span id="realName"></span></p>
     <p><strong>Geburtsdatum:</strong> <span id="birth"></span></p>
     <p><strong>Alter:</strong> <span id="age"></span></p>
     <p><strong>Label:</strong> <span id="label"></span></p>
   </div>
 </div>

 <script>
   function analyze() {
     const link = document.getElementById("linkInput").value.toLowerCase();
     if (!link.includes("spotify") && !link.includes("youtube")) {
       alert("Bitte einen gültigen Spotify- oder YouTube-Link eingeben.");
       return;
     }

     // Beispielkünstler (Ufo361)
     const artistData = {
       name: "Ufo361",
       realName: "Ufuk Bayraktar",
       birth: "28. Mai 1988",
       age: 36,
       label: "Stay High",
       image: "https://upload.wikimedia.org/wikipedia/commons/1/19/Ufo361_2019.jpg",
       streams: [
         { country: "Deutschland", platform: "Spotify", streams: 1200000, rate: 0.004, earnings: "4.800,00" },
         { country: "Türkei", platform: "Spotify", streams: 300000, rate: 0.0032, earnings: "960,00" },
         { country: "Deutschland", platform: "YouTube", streams: 2000000, rate: 0.0015, earnings: "3.000,00" },
         { country: "Schweiz", platform: "YouTube", streams: 400000, rate: 0.0015, earnings: "600,00" }
       ]
     };

     // Daten einfügen
     document.getElementById("artistName").textContent = artistData.name;
     document.getElementById("realName").textContent = artistData.realName;
     document.getElementById("birth").textContent = artistData.birth;
     document.getElementById("age").textContent = artistData.age;
     document.getElementById("label").textContent = artistData.label;
     document.getElementById("artistImage").src = artistData.image;

     const tbody = document.getElementById("dataBody");
     tbody.innerHTML = "";
     artistData.streams.forEach(entry => {
       const tr = document.createElement("tr");
       tr.innerHTML = `
         <td>${entry.country}</td>
         <td>${entry.platform}</td>
         <td>${entry.streams.toLocaleString()}</td>
         <td>${entry.rate.toFixed(4).replace('.', ',')} €</td>
         <td>${entry.earnings} €</td>
       `;
       tbody.appendChild(tr);
     });

     document.getElementById("result").style.display = "flex";
   }
 </script>

</body>
</html>
