<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>World Geography — Grade 9 Quiz</title>
  <style>
    body { font-family: 'Segoe UI', Arial, sans-serif; max-width: 980px; margin: 30px auto; padding: 0 16px; background: #f0f4f8; color: #222; }
    h1 { text-align: center; color: #114b5f; margin-bottom: 24px; }
    .question { background: #fff; border-radius: 10px; padding: 18px; margin: 14px 0; box-shadow: 0 2px 8px rgba(0,0,0,0.08); transition: transform .2s ease; }
    .question:hover { transform: scale(1.01); }
    .options { margin-top: 8px; }
    label { display:block; padding:10px; border-radius:8px; cursor:pointer; transition: background .2s; }
    label:hover { background: #eef6fa; }
    input[type="radio"] { margin-right:8px; }
    .feedback { margin-top:10px; font-weight:600; }
    .correct { color: #0b6; }
    .incorrect { color: #d00; }
    .controls { display:flex; gap:12px; margin:20px 0; align-items:center; flex-wrap:wrap; }
    button { padding:12px 18px; border-radius:6px; border:none; background:#0066cc; color:#fff; cursor:pointer; font-weight:600; }
    button.secondary { background:#666; }
    button:hover { background:#004c99; }
    .scorebox { padding:14px; background:#fff; border-radius:8px; box-shadow:0 1px 3px rgba(0,0,0,0.1); display:none; font-size:1.1rem; }
    .toggleDiv { background:#fff; border-radius:8px; padding:12px; margin-bottom:10px; }
    textarea { width:100%; min-height:100px; margin-top:8px; padding:8px; border-radius:6px; border:1px solid #ddd; }
  </style>
</head>
<body>
  <h1>World Geography — Grade 9 (Interactive Quiz)</h1>
  <div class="toggleDiv">
    <label><input type="checkbox" id="revealToggle"> Reveal Correct Answers Automatically</label>
  </div>
  <div id="quiz"></div>
  <div class="controls">
    <button id="showScoreBtn">Show Score</button>
    <button id="resetBtn" class="secondary">Reset Answers</button>
    <div id="score" class="scorebox"></div>
  </div>
<script>
const questions = [
  { q: "1. What is the crust of the Earth?", options: ["The inner molten layer","The atmosphere","The outermost solid layer","The ocean floor"], correct: 2 },
  { q: "2. What distinguishes the continental crust from the oceanic crust?", options: ["Continental is thinner and denser","Continental is thicker and less dense","Oceanic is thicker","Both are equal"], correct: 1 },
  { q: "3. What is the mantle, and how does it relate to the crust?", options: ["Lies above the crust","Lies beneath the crust and allows plate motion","Forms the atmosphere","Creates mountains"], correct: 1 },
  { q: "4. What are the two main parts of the Earth’s core?", options: ["Inner and outer core","Crust and mantle","Lithosphere and asthenosphere","Outer and lower mantle"], correct: 0 },
  { q: "5. What are mountains, and how do they form?", options: ["Form through tectonic forces or volcanic activity","Created by erosion only","Found underwater only","Form when rivers flood"], correct: 0 },
  { q: "6. A major mountain range located in Asia is:", options: ["Andes","Alps","Himalayas","Rockies"], correct: 2 },
  { q: "7. What role do mountains play in the environment?", options: ["Destroy climates","Increase ocean salinity","Influence regional climate and biodiversity","Lower oxygen levels"], correct: 2 },
  { q: "8. How do glaciers in mountain ranges contribute to freshwater supply?", options: ["By melting rapidly","By storing and slowly releasing freshwater","By drying up rivers","By blocking streams"], correct: 1 },
  { q: "9. What are the characteristics of the Andes Mountains?", options: ["Shortest mountain range","Longest continental range in South America","Lowest elevation range","Found in Africa"], correct: 1 },
  { q: "10. Why are rivers important for agriculture?", options: ["Provide fresh water for irrigation","Increase soil salinity","Create deserts","Block rainfall"], correct: 0 },
  { q: "11. How does the Nile River help Egypt?", options: ["Creates deserts","Provides irrigation water","Separates Asia and Africa","Forms mountains"], correct: 1 },
  { q: "12. The Amazon River plays what environmental role?", options: ["Destroys forests","Supports biodiversity and carbon regulation","Creates deserts","Reduces rainfall"], correct: 1 },
  { q: "13. The Danube River in Europe is used for:", options: ["Transportation and power","Ice fishing","Forest cutting","Tourism only"], correct: 0 },
  { q: "14. What are deserts?", options: ["Dry areas with little vegetation and rainfall","Rainy regions","Cold mountains","Dense forests"], correct: 0 },
  { q: "15. The Rub’ al Khali desert is located in:", options: ["Egypt","Saudi Arabia","Australia","South Africa"], correct: 1 },
  { q: "16. How do desert plants and animals survive?", options: ["Store water and adapt to heat","Need no water","Live only in water","Avoid sunlight"], correct: 0 },
  { q: "17. The Atacama Desert is known for:", options: ["Being the driest place on Earth","Being the wettest desert","Its forests","Snowfall"], correct: 0 },
  { q: "18. The Sahara Desert is in:", options: ["South America","North Africa","Europe","Australia"], correct: 1 },
  { q: "19. The Indian Ocean is known for:", options: ["Warm waters and monsoon patterns","Icebergs","Cold polar temperatures","No currents"], correct: 0 },
  { q: "20. The Great Barrier Reef is located:", options: ["Off the coast of Australia","Near Africa","In the Pacific Ocean near Chile","In the Arctic Ocean"], correct: 0 },
  { q: "21. How do tectonic plates affect mountains?", options: ["They push upward when colliding","They form caves","They melt rock","They create oceans"], correct: 0 },
  { q: "22. When tectonic plates separate, they form:", options: ["Rift valleys","Mountains","Rivers","Volcanoes only"], correct: 0 },
  { q: "23. How can tectonic movement benefit the environment?", options: ["Enrich soil with minerals","Create deserts","Remove vegetation","Cause floods"], correct: 0 },
  { q: "24. What are divergent boundaries?", options: ["Plates moving apart","Plates colliding","Plates sliding past each other","Plates fixed in place"], correct: 0 },
  { q: "25. The Mid-Atlantic Ridge is an example of:", options: ["Divergent boundary","Convergent boundary","Transform boundary","Subduction zone"], correct: 0 },
  { q: "26. At divergent boundaries, what happens?", options: ["Magma rises and forms new crust","Plates collide","Volcanoes stop forming","Erosion begins"], correct: 0 },
  { q: "27. The East African Rift shows:", options: ["Divergent boundary","Convergent boundary","Transform boundary","None"], correct: 0 },
  { q: "28. Convergent boundaries occur when:", options: ["Plates collide","Plates move apart","Plates stay still","Plates rise vertically"], correct: 0 },
  { q: "29. What happens when tectonic plates collide?", options: ["Mountains or volcanoes form","Oceans disappear","Earth stops spinning","Deserts grow"], correct: 0 },
  { q: "30. The Himalayas formed from which collision?", options: ["Indian and Eurasian plates","Pacific and Eurasian","African and Arabian","Antarctic and Australian"], correct: 0 },
  { q: "31. What is subduction?", options: ["One plate moves under another","Plates move apart","Plates stay still","Plates break evenly"], correct: 0 },
  { q: "32. Transform boundaries cause:", options: ["Earthquakes","Volcanoes","Tsunamis only","Deserts"], correct: 0 },
  { q: "33. An example of a transform fault:", options: ["San Andreas Fault","Mid-Atlantic Ridge","East African Rift","Andes Range"], correct: 0 },
  { q: "34. Erosion is:", options: ["The movement of weathered materials","The breaking down of rocks","Formation of lava","Creation of minerals"], correct: 0 },
  { q: "35. Fluvial erosion means:", options: ["Erosion caused by rivers","Wind erosion","Glacial erosion","Coastal erosion"], correct: 0 },
  { q: "36. A famous river erosion example:", options: ["Nile Delta","Grand Canyon","Amazon Basin","Mississippi Delta"], correct: 1 },
  { q: "37. Coastal erosion is caused by:", options: ["Ocean waves hitting cliffs","Earthquakes","Windstorms","Forests"], correct: 0 },
  { q: "38. Coastal erosion can form:", options: ["Sea arches and stacks","Glaciers","Plateaus","Deserts"], correct: 0 },
  { q: "39. The Twelve Apostles in Australia are formed by:", options: ["Coastal erosion","Volcanic activity","Ice movement","Rainfall"], correct: 0 },
  { q: "40. Glaciers are:", options: ["Slow-moving rivers of ice","Solid rocks","Hot lava","Storm clouds"], correct: 0 },
  { q: "41. Glaciers carved deep fjords in:", options: ["China","Norway","Australia","Brazil"], correct: 1 },
  { q: "42. Types of volcanoes include:", options: ["Shield, stratovolcano, cinder cone","Ice, ash, rock","Lava, magma, mud","River, wind, fire"], correct: 0 },
  { q: "43. What is weather?", options: ["Atmospheric conditions at a specific time","Long-term climate average","Ocean movement","Solar energy only"], correct: 0 },
  { q: "44. What is climate?", options: ["Short-term temperature","Long-term weather average","Daily humidity","Air pressure"], correct: 1 },
  { q: "45. Coastal areas usually have:", options: ["Milder temperatures","Hotter deserts","More earthquakes","Stronger winds only"], correct: 0 },
  { q: "46. Humidity is:", options: ["The amount of water vapor in the air","The weight of air","Ocean temperature","Air movement"], correct: 0 },
  { q: "47. High-pressure systems bring:", options: ["Clear and sunny weather","Storms","Tornadoes","Snowfall"], correct: 0 },
  { q: "48. Wind is:", options: ["Movement of air between pressure areas","Movement of water","Movement of clouds","Ocean current"], correct: 0 },
  { q: "49. Precipitation includes:", options: ["Rain, snow, sleet, hail","Sunlight and fog","Sandstorms","Humidity"], correct: 0 },
  { q: "50. Latitude affects climate by:", options: ["Changing the amount of solar energy","Controlling ocean currents","Influencing volcanoes","Affecting soil color"], correct: 0 },
  { q: "51. Altitude affects temperature because:", options: ["Higher altitudes are cooler","Lower altitudes freeze","Heat increases with height","It stays the same"], correct: 0 },
  { q: "52. For every 1,000 m of altitude gained:", options: ["Temperature drops about 6.5°C","Temperature rises","Pressure doubles","Air warms"], correct: 0 },
  { q: "53. Ocean currents are:", options: ["Flows of water moving heat","Air movement","Wind patterns","Rain cycles"], correct: 0 },
  { q: "54. The Gulf Stream is a:", options: ["Warm current raising temperatures","Cold current","Air jet stream","Polar wind"], correct: 0 },
  { q: "55. The California Current is:", options: ["A cold current cooling coastal U.S.","Warm current","River","Air flow"], correct: 0 },
  { q: "56. The Humboldt Current causes:", options: ["Dry climate in Atacama Desert","Wet monsoons","Floods in Chile","Ice melting"], correct: 0 },
  { q: "57. Transpiration is:", options: ["Release of water vapor from plants","Ocean evaporation","Air condensation","Cloud formation"], correct: 0 },
  { q: "58. The five stages of the water cycle include:", options: ["Evaporation, transpiration, condensation, precipitation, collection","Heating, melting, freezing, cooling, solidifying","Photosynthesis steps","Only rain and snow"], correct: 0 }
];
const quizDiv = document.getElementById('quiz');
const revealToggle = document.getElementById('revealToggle');
function createQuiz() {
  quizDiv.innerHTML = '';
  questions.forEach((item, idx) => {
    const qDiv = document.createElement('div');
    qDiv.className = 'question';
    const qTitle = document.createElement('div');
    qTitle.innerHTML = `<strong>${item.q}</strong>`;
    qDiv.appendChild(qTitle);
    const optionsDiv = document.createElement('div');
    optionsDiv.className = 'options';
    item.options.forEach((opt, i) => {
      const id = `q${idx}_opt${i}`;
      const label = document.createElement('label');
      label.htmlFor = id;
      label.innerHTML = `<input type="radio" name="q${idx}" id="${id}" value="${i}"> ${String.fromCharCode(65+i)}) ${opt}`;
      optionsDiv.appendChild(label);
      label.querySelector('input').addEventListener('change', () => showFeedback(idx));
    });
    qDiv.appendChild(optionsDiv);
    const fb = document.createElement('div');
    fb.className = 'feedback';
    fb.id = `fb${idx}`;
    qDiv.appendChild(fb);
    quizDiv.appendChild(qDiv);
  });
}
function showFeedback(i) {
  const chosen = document.querySelector(`input[name="q${i}"]:checked`);
  const fb = document.getElementById('fb'+i);
  fb.innerHTML = '';
  if (!chosen) return;
  const val = Number(chosen.value);
  const correct = questions[i].correct;
  if (val === correct) {
    fb.textContent = '✅ Correct!';
    fb.className = 'feedback correct';
  } else {
    if (revealToggle.checked)
      fb.textContent = `❌ Incorrect. Correct answer: ${String.fromCharCode(65+correct)}) ${questions[i].options[correct]}`;
    else
      fb.textContent = '❌ Incorrect.';
    fb.className = 'feedback incorrect';
  }
}
document.getElementById('showScoreBtn').addEventListener('click', () => {
  let correctCount=0;
  questions.forEach((_,i)=>{
    const chosen=document.querySelector(`input[name="q${i}"]:checked`);
    if(chosen && Number(chosen.value)===questions[i].correct) correctCount++;
  });
  const score=document.getElementById('score');
  score.style.display='block';
  score.innerHTML=`Your Score: ${correctCount}/${questions.length} (${Math.round(100*correctCount/questions.length)}%)`;
});
document.getElementById('resetBtn').addEventListener('click',()=>{createQuiz();document.getElementById('score').style.display='none';});
createQuiz();
</script>
</body>
</html>
