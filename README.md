# Recreate the HTML file from scratch since the session was reset

html_code = """<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>MLK House Sorting Spinner</title>
  <style>
    body {
      text-align: center;
      font-family: Arial, sans-serif;
      background-color: #f5f5f5;
      padding: 50px;
    }
    #spinner {
      width: 300px;
      height: 300px;
      border: 16px solid #ccc;
      border-top: 16px solid #e74c3c;
      border-radius: 50%;
      margin: 30px auto;
      display: none;
      animation: spin 4s ease-out;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(1440deg); }
    }
    #result, #crest {
      margin-top: 30px;
      font-size: 28px;
      font-weight: bold;
    }
    #crest img {
      width: 300px;
      height: auto;
      display: block;
      margin: 20px auto;
    }
    #next {
      display: none;
      margin-top: 30px;
    }
    select, button {
      font-size: 16px;
      padding: 10px;
      margin: 10px;
    }
  </style>
</head>
<body>
  <h1>MLK Staff House Sorting</h1>
  <select id="staff">
    <option value="" disabled selected>Select a staff member</option>
  </select><br>

  <button onclick="startSpin()">Spin the Wheel</button>
  <div id="spinner"></div>
  <div id="result"></div>
  <div id="crest"></div>
  <button id="next" onclick="resetAll()">Next Staff Member</button>

  <audio id="tick" src="https://www.soundjay.com/button/beep-07.wav" preload="auto"></audio>
  <audio id="win" src="https://www.soundjay.com/human/cheering-01.wav" preload="auto"></audio>

  <script>
    const staffAssignments = {
      "Hutchings": "Altruismo", "Curry": "Altruismo", "Blake": "Isibindi", "Mathis": "Isibindi",
      "Gainey": "Altruismo", "5th Vacancy": "Altruismo", "Nutrition Parks": "Altruismo",
      "Nutrition 2": "Altruismo", "Bentley": "Altruismo", "Walker-Turner": "Reveur", "Smart": "Isibindi",
      "Rogers": "Isibindi", "Dixon": "Isibindi", "S. Williams": "Altruismo", "N. Williams": "Altruismo",
      "Middleton": "Amistad", "Gooden": "Amistad", "Jones": "Amistad", "Brown": "Reveur", "Sapp": "Amistad",
      "Bradford": "Amistad", "Crossing Guard": "Reveur", "Stewart": "Reveur", "Watson": "Reveur",
      "Henriques": "Amistad", "Hooks": "Amistad", "Copeland": "Reveur", "Wooten": "Isibindi",
      "Nutrtion Stephens": "Isibindi", "Mr. Al": "Isibindi", "Heyser": "Altruismo", "Raines": "Altruismo",
      "Reese": "Altruismo", "Ashley": "Altruismo", "Nutrition Parker": "Altruismo", "Parker": "Amistad",
      "Parrot": "Isibindi", "Whipple-Wilson": "Isibindi", "Middlebrooks": "Isibindi", "Abad": "Reveur",
      "Orr": "Altruismo", "Glover": "Amistad", "Ogbuka": "Isibindi", "Cornelius": "Isibindi",
      "Scott": "Reveur", "Harrison": "Reveur", "Fordham": "Amistad", "Davis": "Amistad",
      "Bentley 4th": "Amistad", "Booker": "Amistad", "Thompson": "Reveur", "S. Sherman": "Reveur",
      "Gomes": "Reveur", "Odom": "Reveur", "2nd Vacancy": "Amistad", "Mathis Cust": "Amistad",
      "Pryor": "Amistad", "Nurse Carswell": "Altruismo", "Banks": "Altruismo", "Milton": "Reveur",
      "Bell": "Isibindi", "Anderson": "Isibindi", "PEC co-teacher": "Isibindi", "PEC Para": "Isibindi",
      "Duncan": "Isibindi", "Starks": "Altruismo", "Hampton": "Reveur", "Basley": "Amistad",
      "Canty": "Amistad", "Conaway": "Amistad", "J. Sherman": "Amistad"
    };

    const houseDetails = {
      "Amistad": {
        color: "#e74c3c",
        crest: "https://via.placeholder.com/300x300?text=Amistad+Crest"
      },
      "Isibindi": {
        color: "#27ae60",
        crest: "https://via.placeholder.com/300x300?text=Isibindi+Crest"
      },
      "Altruismo": {
        color: "#2c3e50",
        crest: "https://via.placeholder.com/300x300?text=Altruismo+Crest"
      },
      "Reveur": {
        color: "#2980b9",
        crest: "https://via.placeholder.com/300x300?text=Reveur+Crest"
      }
    };

    window.onload = function () {
      const dropdown = document.getElementById("staff");
      const names = Object.keys(staffAssignments).sort();
      names.forEach(name => {
        const option = document.createElement("option");
        option.value = name;
        option.textContent = name;
        dropdown.appendChild(option);
      });
    };

    function startSpin() {
      const staff = document.getElementById("staff").value;
      if (!staff) return alert("Please select a staff member.");
      const house = staffAssignments[staff];

      document.getElementById("spinner").style.display = "block";
      document.getElementById("result").innerText = "";
      document.getElementById("crest").innerHTML = "";
      document.getElementById("next").style.display = "none";

      const tick = document.getElementById("tick");
      const win = document.getElementById("win");
      let clicks = 0;
      const clicker = setInterval(() => {
        tick.play();
        clicks++;
        if (clicks > 20) clearInterval(clicker);
      }, 100);

      setTimeout(() => {
        const data = houseDetails[house];
        document.body.style.backgroundColor = data.color;
        document.getElementById("result").innerText = `${staff} has been sorted into House ${house}!`;
        document.getElementById("crest").innerHTML = `<img src="${data.crest}" alt="${house} Crest">`;
        win.play();
        document.getElementById("next").style.display = "inline-block";
      }, 4100);
    }

    function resetAll() {
      document.getElementById("spinner").style.display = "none";
      document.getElementById("staff").selectedIndex = 0;
      document.getElementById("result").innerText = "";
      document.getElementById("crest").innerHTML = "";
      document.getElementById("next").style.display = "none";
      document.body.style.backgroundColor = "#f5f5f5";
    }
  </script>
</body>
</html>
"""

html_file_path = "/mnt/data/MLK_House_Sorting_Spinner_Regenerated.html"
with open(html_file_path, "w") as f:
    f.write(html_code)

html_file_path
