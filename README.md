<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Computation Tool</title>
    <style>
        body {
            font-family: Droid system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
            margin: 20px;
            padding: 20px;
            max-width: 600px;
            margin: auto;
        }
        label, input {
            display: block;
            margin-bottom: 10px;
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        .error {
            color: red;
        }
    </style>
</head>
<body>
    <h1>Grade Computation Tool</h1>
    <form method="POST">
        <label for="prelim_grade">Enter Prelim Grade (0-100):</label>
        <input type="number" id="prelim_grade" name="prelim_grade" min="0" max="100" required>
        <button type="submit">Calculate</button>
    </form>
    
    {% if prelim_grade is not none %}
        <div class="result">
            <h2>Results:</h2>
            <p>Prelim Grade: {{ prelim_grade }}</p>
            <p>Required Midterm Grade: {{ required_midterm }}</p>
            <p>Required Final Grade: {{ required_final }}</p>
            <p>
                {% if can_pass %}
                    You have a chance to pass!
                {% else %}
                    It is difficult to pass.
                {% endif %}
            </p>
            <p>
                {% if dean_lister_possible %}
                    You can qualify for Dean’s Lister!
                {% else %}
                    You cannot qualify for Dean’s Lister.
                {% endif %}
            </p>
        </div>
    {% endif %}
    
    {% if error %}
        <p<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Computation Tool</title>
    <style>
        body {
            font-family: Droid system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
            margin: 20px;
            padding: 20px;
            max-width: 600px;
            margin: auto;
        }
        label, input {
            display: block;
            margin-bottom: 10px;
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        .error {
            color: red;
        }
    </style>
</head>
<body>
    <h1>Grade Computation Tool</h1>
    <form method="POST">
        <label for="prelim_grade">Enter Prelim Grade (0-100):</label>
        <input type="number" id="prelim_grade" name="prelim_grade" min="0" max="100" required>
        <button type="submit">Calculate</button>
    </form>
    
    {% if prelim_grade is not none %}
        <div class="result">
            <h2>Results:</h2>
            <p>Prelim Grade: {{ prelim_grade }}</p>
            <p>Required Midterm Grade: {{ required_midterm }}</p>
            <p>Required Final Grade: {{ required_final }}</p>
            <p>
                {% if can_pass %}
                    You have a chance to pass!
                {% else %}
                    It is difficult to pass.
                {% endif %}
            </p>
            <p>
                {% if dean_lister_possible %}
                    You can qualify for Dean’s Lister!
                {% else %}
                    You cannot qualify for Dean’s Lister.
                {% endif %}
            </p>
        </div>
    {% endif %}
    
    {% if error %}
        <p class="error">{{ error }}</p>
    {% endif %}
</body>
</html> class="error">{{ error }}</p>
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        try:
            prelim_grade = float(request.form['prelim_grade'])

            if not 0 <= prelim_grade <= 100:
                error = "Prelim grade must be between 0 and 100."
                return render_template('index.html', error=error)

            # Calculate the required Midterm and Final grades to pass
            required_midterm = (75 - 0.2 * prelim_grade) / 0.3
            required_final = (75 - 0.2 * prelim_grade - 0.3 * required_midterm) / 0.5
            can_pass = required_midterm <= 100 and required_final <= 100

            # Calculate for Dean's Lister
            # Total average needed to be a Dean’s Lister is 90%
            # Midterm and Final grade needed to achieve an average of 90% overall
            required_midterm_dean = (90 - 0.2 * prelim_grade) / 0.3
            required_final_dean = (90 - 0.2 * prelim_grade - 0.3 * required_midterm_dean) / 0.5
            dean_lister_possible = required_midterm_dean <= 100 and required_final_dean <= 100

            return render_template(
                'index.html',
                prelim_grade=prelim_grade,
                required_midterm=round(required_midterm, 2),
                required_final=round(required_final, 2),
                can_pass=can_pass,
                dean_lister_possible=dean_lister_possible
            )
        except ValueError:
            error = "Invalid input. Please enter a valid number."
            return render_template('index.html', error=error)

    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)

    {% endif %}
</body>
</html>
