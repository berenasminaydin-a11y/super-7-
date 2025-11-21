# super-7-
a site that helps students to find themselves the perfect passion project and more 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Super7 Prototype</title>
<style>
  body { font-family: Arial, sans-serif; padding: 20px; background: #f0f0f0; }
  h1 { text-align: center; }
  .question, .preference { margin-bottom: 20px; background: #fff; padding: 15px; border-radius: 10px; }
  button { padding: 10px 20px; font-size: 16px; margin: 5px; cursor: pointer; }
  .results { display: none; margin-top: 30px; background: #fff; padding: 20px; border-radius: 10px; }
  .project { margin-bottom: 15px; padding: 10px; border: 1px solid #ccc; border-radius: 5px; }
</style>
</head>
<body>

<h1>Super7 Prototype</h1>

<div id="quiz">
  <div class="question" data-category="STEM">
    <h3>1. Do you enjoy solving complex problems?</h3>
    <button data-value="1">Not at all</button>
    <button data-value="2">A little</button>
    <button data-value="3">Neutral</button>
    <button data-value="4">Mostly</button>
    <button data-value="5">Absolutely</button>
  </div>

  <div class="question" data-category="Art">
    <h3>2. Do you enjoy expressing yourself creatively?</h3>
    <button data-value="1">Not at all</button>
    <button data-value="2">A little</button>
    <button data-value="3">Neutral</button>
    <button data-value="4">Mostly</button>
    <button data-value="5">Absolutely</button>
  </div>

  <div class="question" data-category="Social">
    <h3>3. Do you like helping people or working in groups?</h3>
    <button data-value="1">Not at all</button>
    <button data-value="2">A little</button>
    <button data-value="3">Neutral</button>
    <button data-value="4">Mostly</button>
    <button data-value="5">Absolutely</button>
  </div>
</div>

<div id="preference" class="preference" style="display:none;">
  <h3>Which category do you want most of your 7 projects from?</h3>
  <button data-pref="STEM">STEM</button>
  <button data-pref="Art">Art</button>
  <button data-pref="Social">Social</button>
</div>

<div class="results" id="results">
  <h2>Your Top 7 Passion Projects</h2>
  <div id="projects"></div>
</div>

<script>
const questions = document.querySelectorAll('.question');
const preferenceDiv = document.getElementById('preference');
const resultsDiv = document.getElementById('results');
const projectsDiv = document.getElementById('projects');

let scores = { STEM: 0, Art: 0, Social: 0 };
let answered = 0;

// Projects database
const projectsDB = {
  STEM: ['Build a robot', 'Create a mini app', 'Conduct a science experiment'],
  Art: ['Start a sketchbook', 'Create a digital art portfolio', 'Write a short story'],
  Social: ['Volunteer at a local NGO', 'Organize a community project', 'Start a blog to help others']
};

// Handle question answers
questions.forEach(q => {
  q.querySelectorAll('button').forEach(btn => {
    btn.addEventListener('click', () => {
      const category = q.getAttribute('data-category');
      scores[category] += parseInt(btn.getAttribute('data-value'));
      q.style.display = 'none';
      answered++;
      if (answered === questions.length) {
        preferenceDiv.style.display = 'block';
      }
    });
  });
});

// Handle preference selection
preferenceDiv.querySelectorAll('button').forEach(btn => {
  btn.addEventListener('click', () => {
    const pref = btn.getAttribute('data-pref');
    showResults(pref);
    preferenceDiv.style.display = 'none';
  });
});

// Show results based on preference
function showResults(pref) {
  resultsDiv.style.display = 'block';
  let topProjects = [];

  // Add 3 from preferred category
  topProjects = topProjects.concat(projectsDB[pref]);

  // Add 2 from other categories
  Object.keys(projectsDB).forEach(cat => {
    if (cat !== pref) topProjects = topProjects.concat(projectsDB[cat].slice(0,2));
  });

  // Add 2 random filler projects
  topProjects.push('Start a personal challenge project');
  topProjects.push('Try a new hobby you never considered');

  // Shuffle and pick 7
  topProjects = topProjects.sort(() => 0.5 - Math.random()).slice(0,7);

  projectsDiv.innerHTML = topProje
