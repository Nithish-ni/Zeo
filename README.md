# Zeo
# application 1
Rule Engine Overview
The rule engine will evaluate user eligibility based on attributes like age, department, income, and spending using an Abstract Syntax Tree (AST).

# 1. Data Structure for AST
We'll create a simple structure to represent each rule.

# code 
class Node:
    def __init__(self, node_type, left=None, right=None, value=None):
        self.node_type = node_type  
        self.left = left            
        self.right = right          
        self.value = value          
# 2. Data Storage
Database Choice:
Use PostgreSQL to store rules.

Schema Example:

sql
Copy code
CREATE TABLE rules (
    id SERIAL PRIMARY KEY,
    rule_string TEXT NOT NULL
);
Sample Data:


INSERT INTO rules (rule_string) VALUES 
    ('((age > 30 AND department = ''Sales'') OR (age < 25 AND department = ''Marketing'')) AND (salary > 50000 OR experience > 5)'),
    ('((age > 30 AND department = ''Marketing'')) AND (salary > 20000 OR experience > 5)');
# 3. API Design
Create Rule Function
Convert a rule string into an AST.


def create_rule(rule_string):
    
Combine Rules Function
Combine multiple rules into one AST.


def combine_rules(rules):
    
Evaluate Rule Function
Evaluate the AST against provided user data.



def evaluate_rule(ast, data):
  
# 4. Test Cases
1. Create Individual Rules:


rule1_ast = create_rule("((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing'))")
2. Combine Example Rules:


combined_ast = combine_rules([rule1, rule2])
# 3. Evaluate Rules with Sample Data:


data = {"age": 35, "department": "Sales", "salary": 60000, "experience": 3}
result = evaluate_rule(combined_ast, data)
Bonus Features
# Error Handling: Check for valid rule strings.
Attribute Validations: Ensure attributes used in rules are valid.
Modify Rules: Allow updates to existing rules.


# application 2
Weather Monitoring System Overview
Goal:
Monitor weather conditions in real-time and summarize data daily using OpenWeatherMap API.

Steps to Build the System
# 1. Fetch Weather Data
Use the OpenWeatherMap API to get weather data for major Indian cities.
Retrieve important data: weather condition, temperature, and update time.
#Code:
import requests

API_KEY = 'YOUR_API_KEY'
CITIES = ['Delhi', 'Mumbai', 'Chennai', 'Bangalore', 'Kolkata', 'Hyderabad']

def fetch_weather_data(city):
    response = requests.get(f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}")
    return response.json()
# 2. Convert Temperatures
Convert temperature from Kelvin to Celsius or Fahrenheit based on user preference.
Conversion Functions:

def kelvin_to_celsius(kelvin):
    return kelvin - 273.15
# 3. Daily Weather Summary
Keep track of daily weather data (average, max, min temperature, and dominant condition).
Summary Calculation:

python
Copy code
daily_summary = {}

def update_daily_summary(city, temp, condition):
    Update daily summary with new data
# 4. Set Up Alerts
Create user-configurable temperature thresholds.
Trigger alerts if the temperature exceeds the threshold for consecutive updates.
Alert Function:


def check_alerts(temp):
    if temp > threshold:
      
# 5. Visualization (Optional)
Use libraries like Matplotlib or Plotly to visualize daily summaries and alerts.
Test Cases
API Connection: Ensure you can fetch data from the API with a valid key.
Data Retrieval: Simulate getting weather data.
Temperature Conversion: Test if temperatures convert correctly.
Daily Summary Calculation: Verify the summary calculations are accurate.
Alert Functionality: Check if alerts trigger correctly.
Bonus Ideas
Include more weather data (like humidity and wind speed).
Add forecast data to the summaries.
Directory Structure
Organize your files like this:

bash
Copy code
weather_monitor/
├── src/
│   ├── main.py          
│   ├── weather.py      
│   ├── alerts.py        
│   └── summary.py       
├── tests/
│   ├── test_weather.py  
│   └── test_alerts.py   
├── requirements.txt      
└── README.md             
README.md
# Include:
# Project overview
Setup instructions
How to run the application
Design choices


