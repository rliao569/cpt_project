
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>College Acceptance Prediction</title>
</head>
<body>
    <h1>College Acceptance Prediction</h1>
    <form id="prediction-form">
        GPA: <input type="number" name="gpa" step="0.01" required><br>
        SAT: <input type="number" name="sat" required><br>
        Extracurriculars: <input type="number" name="extracurriculars" required><br>
        <button type="submit">Predict</button>
    </form>
    <div id="result"></div>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
        $(document).ready(function () {
            $('#prediction-form').submit(function (e) {
                e.preventDefault();
                $.ajax({
                    type: 'POST',
                    url: '/predict',
                    data: $('#prediction-form').serialize(),
                    success: function (response) {
                        $('#result').text('Prediction: ' + response.result);
                    }
                });
            });
        });
    </script>
</body>
</html>
