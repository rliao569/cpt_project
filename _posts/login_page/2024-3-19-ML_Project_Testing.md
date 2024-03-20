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
    function makePrediction() {
        var gpa = document.getElementById("gpa").value;
        var sat = document.getElementById("sat").value;
        var extracurriculars = document.getElementById("extracurriculars").value;
        var data = {
            gpa: gpa,
            SAT: sat,
            Extracurricular_Activities: extracurriculars
        };
        fetch('http://127.0.0.1:8086/api/users/Prediction', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        })
        .then(response => response.json())
        .then(result => {
            alert("Prediction Result: " + JSON.stringify(result));
        })
        .catch(error => {
            console.error('Error:', error);
        });
    }
    document.getElementById("checkCompatibility").addEventListener("click", makePrediction);
</script>
</body>
</html>