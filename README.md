# 🧶 Thread Shed Sales Analysis

This Python project processes a raw string of daily sales data for a fictional "Thread Shed" company. It demonstrates essential data cleaning, parsing, and analysis techniques to extract meaningful insights from unstructured text, such as total sales and the count of specific thread colors sold.

---

## How It Works

The script begins with a messy, multi-line string representing a day's worth of sales transactions. Each transaction includes customer name, sale amount, thread color(s), and date. The script then systematically:

* **Cleans Data**: Replaces inconsistent delimiters and removes extraneous whitespace and newline characters.
* **Parses Transactions**: Splits the large string into individual transactions and then each transaction into separate data points (customer, sale, thread color).
* **Organizes Data**: Populates dedicated lists for customers, sales figures, and thread colors sold.
* **Calculates Total Sales**: Iterates through the sales data to sum up the total revenue for the day.
* **Analyzes Thread Colors**: Splits multi-color thread entries (e.g., "red&blue") into individual colors and then counts the occurrences of each specific color sold.
* **Reports Findings**: Prints a summary of total sales and a breakdown of how many units of each thread color were sold.

---

## Getting Started

### Prerequisites

You'll only need **Python 3** installed on your computer to run this script.

### Installation

No special installation is required. Just save the code to a `.py` file.

1.  **Save the code:** Copy the entire code block provided and save it as `thread_shed_analysis.py` (or any other name ending with `.py`) on your computer.

---

## Usage

1.  **Open your terminal or command prompt.**
2.  **Navigate to the directory** where you saved `thread_shed_analysis.py`.
    ```bash
    cd path/to/your/project
    ```
3.  **Run the script** using Python:
    ```bash
    python thread_shed_analysis.py
    ```
4.  The script will immediately print the calculated total sales and the count for each thread color to your console.

---

## Code

Here's the complete code for the Thread Shed Sales Analysis project:

```python
daily_sales = \
"""Edith Mcbride   ;,;$1.21   ;,;   white ;,;
09/15/17   ,Herbert Tran   ;,;   $7.29;,;
white&blue;,;   09/15/17 ,Paul Clarke ;,;$12.52
;,;   white&blue ;,; 09/15/17 ,Lucille Caldwell
;,;   $5.13   ;,; white   ;,; 09/15/17,
Eduardo George   ;,;$20.39;,; white&yellow
;,;09/15/17   ,   Danny Mclaughlin;,;$30.82;,;
purple ;,;09/15/17 ,Stacy Vargas;,; $1.85   ;,;
purple&yellow ;,;09/15/17,   Shaun Brock;,;
$17.98;,;purple&yellow ;,; 09/15/17 ,
Erick Harper ;,;$17.41;,; blue ;,; 09/15/17,
Michelle Howell ;,;$28.59;,; blue;,;   09/15/17   ,
Carroll Boyd;,; $14.51;,;   purple&blue   ;,;
09/15/17   , Teresa Carter   ;,; $19.64 ;,;
white;,;09/15/17   ,   Jacob Kennedy ;,; $11.40
;,; white&red   ;,; 09/15/17, Craig Chambers;,;
$8.79 ;,; white&blue&red   ;,;09/15/17   , Peggy Bell;,; $8.65 ;,;blue   ;,; 09/15/17,   Kenneth Cunningham ;,;   $10.53;,;   green&blue   ;,;
09/15/17   ,   Marvin Morgan;,;   $16.49;,;
green&blue&red   ;,;   09/15/17 ,Marjorie Russell
;,; $6.55 ;,;   green&blue&red;,;   09/15/17 ,
Israel Cummings;,;   $11.86   ;,;black;,;
09/15/17,   June Doyle   ;,;   $22.29 ;,;
black&yellow ;,;09/15/17 , Jaime Buchanan   ;,;
$8.35;,;   white&black&yellow   ;,;   09/15/17,
Rhonda Farmer;,;$2.91 ;,;   white&black&yellow
;,;09/15/17, Darren Mckenzie ;,;$22.94;,;green
;,;09/15/17,Rufus Malone;,;$4.70   ;,; green&yellow
;,; 09/15/17   ,Hubert Miles;,;   $3.59
;,;green&yellow&blue;,;   09/15/17   , Joseph Bridges   ;,;$5.66   ;,; green&yellow&purple&blue
;,;   09/15/17 , Sergio Murphy   ;,;$17.51   ;,;
black   ;,;   09/15/17 , Audrey Ferguson ;,;
$5.54;,;black&blue   ;,;09/15/17 ,Edna Williams ;,;
$17.13;,; black&blue;,;   09/15/17,   Randy Fleming;,;   $21.13 ;,;black ;,;09/15/17 ,Elisa Hart;,; $0.35   ;,; black&purple;,;   09/15/17   ,
Ernesto Hunt ;,; $13.91   ;,;   black&purple ;,;
09/15/17,   Shannon Chavez   ;,;$19.26   ;,;
yellow;,; 09/15/17   , Sammy Cain;,; $5.45;,;
yellow&red ;,;09/15/17 ,   Steven Reeves ;,;$5.50
;,;   yellow;,;   09/15/17, Ruben Jones   ;,;
$14.56 ;,;   yellow&blue;,;09/15/17 , Essie Hansen;,;   $7.33   ;,;   yellow&blue&red
;,; 09/15/17   ,   Rene Hardy   ;,; $20.22   ;,;
black ;,;   09/15/17 ,   Lucy Snyder   ;,; $8.67
;,;black&red   ;,; 09/15/17 ,Dallas Obrien ;,;
$8.31;,;   black&red ;,;   09/15/17,   Stacey Payne
;,;   $15.70   ;,;   white&black&red ;,;09/15/17
,   Tanya Cox   ;,;   $6.74   ;,;yellow   ;,;
09/15/17 , Melody Moran ;,;   $30.84
;,;yellow&black;,;   09/15/17 , Louise Becker   ;,;
$12.31 ;,; green&yellow&black;,;   09/15/17 ,
Ryan Webster;,;$2.94 ;,; yellow ;,; 09/15/17
,Justin Blake ;,; $22.46   ;,;white&yellow ;,;
09/15/17,   Beverly Baldwin ;,;   $6.60;,;
white&yellow&black ;,;09/15/17   ,   Dale Brady
;,;   $6.27 ;,; yellow   ;,;09/15/17 ,Guadalupe Potter ;,;$21.12   ;,; yellow;,; 09/15/17   ,
Desiree Butler ;,;$2.10   ;,;white;,; 09/15/17
,Sonja Barnett ;,; $14.22 ;,;white&black;,;
09/15/17, Angelica Garza;,;$11.60;,;white&black
;,;   09/15/17   ,   Jamie Welch   ;,; $25.27   ;,;
white&black&red ;,;09/15/17   ,   Rex Hudson
;,;$8.26;,;   purple;,; 09/15/17 ,   Nadine Gibbs
;,;   $30.80 ;,;   purple&yellow   ;,; 09/15/17   ,
Hannah Pratt;,;   $22.61   ;,;   purple&yellow
;,;09/15/17,Gayle Richards;,;$22.19 ;,;
green&purple&yellow ;,;09/15/17   ,Stanley Holland
;,; $7.47   ;,; red ;,; 09/15/17 , Anna Dean;,;$5.49 ;,; yellow&red ;,;   09/15/17   ,
Terrance Saunders ;,;   $23.70   ;,;green&yellow&red
;,; 09/15/17 ,   Brandi Zimmerman ;,; $26.66 ;,;
red   ;,;09/15/17 ,Guadalupe Freeman ;,; $25.95;,;
green&red ;,;   09/15/17   ,Irving Patterson
;,;$19.55 ;,; green&white&red ;,;   09/15/17 ,Karl Ross;,;   $15.68;,;   white ;,;   09/15/17 , Brandy Cortez ;,;$23.57;,;   white&red   ;,;09/15/17,
Mamie Riley   ;,;$29.32;,; purple;,;09/15/17 ,Mike Thornton   ;,; $26.44 ;,;   purple   ;,; 09/15/17,
Jamie Vaughn   ;,; $17.24;,;green ;,; 09/15/17   ,
Noah Day ;,;   $8.49   ;,;green   ;,;09/15/17
,Josephine Keller ;,;$13.10 ;,;green;,;   09/15/17 ,   Tracey Wolfe;,;$20.39 ;,; red   ;,; 09/15/17 ,
Ignacio Parks;,;$14.70   ;,; white&red ;,;09/15/17
, Beatrice Newman ;,;$22.45   ;,;white&purple&red
;,;   09/15/17, Andre Norris   ;,;   $28.46   ;,;
red;,;   09/15/17 ,   Albert Lewis ;,; $23.89;,;
black&red;,; 09/15/17,   Javier Bailey   ;,;
$24.49   ;,; black&red ;,; 09/15/17   , Everett Lyons ;,;$1.81;,;   black&red ;,; 09/15/17 ,
Abraham Maxwell;,; $6.81   ;,;green;,;   09/15/17
,   Traci Craig ;,;$0.65;,; green&yellow;,;
09/15/17 , Jeffrey Jenkins   ;,;$26.45;,;
green&yellow&blue   ;,;   09/15/17,   Merle Wilson
;,;   $7.69 ;,; purple;,; 09/15/17,Janis Franklin
;,;$8.74   ;,; purple&black   ;,;09/15/17 ,
Leonard Guerrero ;,;   $1.86   ;,;yellow
;,;09/15/17,Lana Sanchez;,;$14.75   ;,; yellow;,;
09/15/17   ,Donna Ball ;,; $28.10   ;,;
yellow&blue;,;   09/15/17   , Terrell Barber   ;,;
$9.91   ;,; green ;,;09/15/17   ,Jody Flores;,;
$16.34 ;,; green ;,;   09/15/17,   Daryl Herrera
;,;$27.57;,; white;,;   09/15/17   , Miguel Mcguire;,;$5.25;,; white&blue   ;,;   09/15/17 ,
Rogelio Gonzalez;,; $9.51;,;   white&black&blue
;,;   09/15/17   ,   Lora Hammond ;,;$20.56 ;,;
green;,;   09/15/17,Owen Ward;,; $21.64   ;,;
green&yellow;,;09/15/17,Malcolm Morales ;,;
$24.99   ;,;   green&yellow&black;,; 09/15/17 ,
Eric Mcdaniel ;,;$29.70;,; green ;,; 09/15/17
,Madeline Estrada;,;   $15.52;,;green;,;   09/15/17
, Leticia Manning;,;$15.70 ;,; green&purple;,;
09/15/17 ,   Mario Wallace ;,; $12.36 ;,;green ;,;
09/15/17,Lewis Glover;,;   $13.66   ;,;
green&white;,;09/15/17,   Gail Phelps   ;,;$30.52
;,; green&white&blue   ;,; 09/15/17 , Myrtle Morris
;,;   $22.66   ;,; green&white&blue;,;09/15/17"""

#------------------------------------------------
# Start coding below!
# Per tast 2 in the line of code below I replaced the artifact ;,; with a ---
daily_sales_replaced = daily_sales.replace(";,;", "---")

# Per task 3 I split the string into a list of each individual transaction at the comma
daily_transactions = daily_sales_replaced.split(',')

# Per task 5 I split each individual transaction into a list of its data points
daily_transactions_split = []
for transaction in daily_transactions:
  daily_transactions_split.append(transaction.split('---'))
#print(daily_transactions_split)

# per task 8 I cleaned up the white space around daily transactions split
transactions_clean = []
for transaction in daily_transactions_split:
  transaction_clean = []
  for data in transaction:
    transaction_clean.append(data.replace("\n", "").strip(" "))
  transactions_clean.append(transaction_clean)
#print(transactions_clean)

# Per task 10 I created a empty list for customers, sales, and threads sold then appended thier individual data points to the corresponding lists
customers = []
sales = []
thread_sold = []

for transaction in transactions_clean:
  customers.append(transaction[0])
  sales.append(transaction[1])
  thread_sold.append(transaction[2])
#print(customers)
#print(sales)
#print(thread_sold)

# Per task 13 I created a variable to determine the total value of the days sales
total_sales = 0
for i in sales:
  stripped = float(i.strip("$"))
  total_sales += stripped

#print(total_sales)

# per tasks 16 to 20 I created a function that determines how much thread of a specific color was sold
thread_sold_split = []
for i in thread_sold:
  for symbol in i.split("&"):
    thread_sold_split.append(symbol)

#print(thread_sold_split)

def color_count(color):
  counter = 0
  for count in thread_sold_split:
    if color == count:
      counter += 1
  return counter
#print(color_count("white"))

colors = ['red', 'yellow', 'green', 'white', 'black', 'blue', 'purple']

for color in colors:
  print("Thread Shed sold {0} of {1} thread today".format(color_count(color), color))
```

The "Thread Shed" project is a very common and effective project in Codecademy's Python 3 curriculum, (Codecademy.com) especially in modules focusing on **data manipulation, string methods, and list operations**.

Here's a breakdown of the key learning contexts for this project:

* **String Manipulation and Cleaning:**
    * Using `replace()` to standardize data by changing delimiters.
    * Employing `strip()` to remove unwanted whitespace, including newline characters (`\n`), which are common in raw, multi-line data.
    * Understanding how to handle inconsistent formatting in real-world data.

* **List Operations:**
    * Creating and appending to lists (`append()`).
    * Splitting strings into lists (`split()`).
    * Iterating through lists using `for` loops.
    * Accessing elements within lists (including nested lists) by index.

* **Data Parsing and Structuring:**
    * The process of taking unstructured (or semi-structured) data from a single string and transforming it into a more usable, organized format (lists of lists, then separate lists for different data points).
    * This is a foundational concept in data processing and preparation.

* **Type Conversion:**
    * Converting string representations of numbers (like `"$1.21"`) into numerical types (like `float`) to perform calculations. Using `strip("$")` before conversion is key here.

* **Basic Data Analysis:**
    * Calculating aggregates (e.g., `total_sales`).
    * Counting occurrences of specific items (e.g., `color_count` function).
    * This introduces the idea of extracting insights from raw data.

* **Functions (if implemented):**
    * Defining and calling functions to encapsulate reusable logic (like `color_count`). This promotes modularity and readability.

* **Looping and Conditionals:**
    * Extensive use of `for` loops to iterate through data.
    * Implicit use of conditional logic within the `color_count` function's `if` statement.
