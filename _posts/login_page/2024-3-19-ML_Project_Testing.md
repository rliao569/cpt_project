---
toc: true
comments: false
layout: base
permalink: /mlproject
---
<html>
<head>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  h1 {
    font-family: 'Poppins', sans-serif;
    text-align: center;
    color: #333;
    animation: bounce 1s infinite alternate;
    font-size: 40px; 
  }
  @keyframes bounce {
    0% { transform: translateY(0); }
    100% { transform: translateY(-20px); }
  }
  .container {
    width: 50%;
    margin: 0 auto; 
    text-align: center;
  }
  .input-box {
    display: inline-block;
    margin-bottom: 30px; 
    margin-right: 20px; 
  }
  .input-box label {
    display: block;
    margin-bottom: 5px;
  }
  .input-box input {
    width: 200px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }
  .btn {
    background-color: #4CAF50;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  .btn:hover {
    background-color: #45a049;
  }
</style>
</head>
<body>
<center>
  <h1>Admission Predictor</h1>
  <div class="container">
    <div class="input-box">
      <label for="sat">SAT Score:</label><br>
      <input type="number" id="sat" name="sat" placeholder="SAT score">
    </div>
    <div class="input-box">
      <label for="gpa">GPA:</label><br>
      <input type="number" step="0.01" id="gpa" name="gpa" placeholder="GPA">
    </div>
    <div class="input-box">
      <label for="extracurriculars">Extracurriculars:</label><br>
      <input type="number" id="extracurriculars" name="extracurriculars" placeholder="Extracurriculars">
    </div>
    <br>
    <button class="btn" id="checkCompatibility">Check</button>
  </div>
</center>
<script>
document.getElementById('checkCompatibility').addEventListener('click', function() {
  const satScore = document.getElementById('sat').value;
  const gpa = document.getElementById('gpa').value;
  const extracurriculars = document.getElementById('extracurriculars').value;
  const formData = new FormData();
  formData.append('SAT', satScore);
  formData.append('gpa', gpa);
  formData.append('Extracurricular_Activities', extracurriculars);
  fetch('http://127.0.0.1:5000/api/Prediction', {
    method: 'POST',
    body: formData
  })
  .then(response => response.json())
  .then(data => {
    alert(`Compatibility checked! Response: ${JSON.stringify(data)}`);
  })
  .catch(error => {
    console.error('Error:', error);
  });
});
</script>
</body>
</html>
