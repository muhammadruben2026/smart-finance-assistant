AI Collaborations 
### AI collaboration # 1
**Context**: I was trying to get AI to load a CSV file with transaction data using the prompt the module/lab gave us, getting the AI to do the provided cleaning and writing the professional python code. 

**Prompt**: "I'm building a Smart Finance Assistant for my programming assignment. I need to load a CSV file with transaction data (columns: Date, Amount, Category, Description). The Amount column has dollar signs that need cleaning. Please write professional Python code with detailed comments that:
Loads the CSV data
Cleans and validates the data
Shows basic information about the dataset
Handles any common data issues"*

**Result**: AI provided the working code and cleaned and validated the data as the prompt requested. AI also provided basic info about the dataset and handled any issues regarding the data. 

**Reflection**: What worked well was that the AI was able to produce the code instantaneously and it listened to the specific requests the prompt asked for, what didn't work well was that I got confused at some parts of the code but the explanation AI provided gave me an insight into what it was doing and essentially what was going on. I learned that AI can generate a CSV file quickly and that in the business world AI is needed to help us finish coding things quicker and moving forward. 

### AI Collaboration # 2
**Context**: Needed AI to help create the Core Analysis Functions basically the foundation of my finance assistant

**Prompt**: "For my Smart Finance Assistant, I need functions to analyze spending data. Please create well-documented functions that:
Calculate total spending by category
Find the top 5 spending categories
Calculate average spending per transaction
Identify any unusual transactions (very high or negative amounts) Each function should have clear business explanations and error handling."

**Result**: The AI managed to generate the code instantaneously again, AI also implemented features so that I can find what the prompt requested for e.g. the total spending by category, top 5 spending categories , etc. AI also implemented clear business explanations and handled any errors that may have appeared. 

**Reflection**: What worked well was that the AI managed to generate the code quick and listened to the specifc requirements listed in the prompt, AI rarely had problems during this bit, I learned that AI can build core anaylsis functins and add more to its own coding. 

### AI Collaboration # 3 
**Context**: Needed AI to help generate Business insights 

**Prompt**: "Using the transaction analysis functions, help me create a comprehensive spending report that would be useful for personal financial planning. Include recommendations for potential savings and spending pattern observations. Format it like a professional financial summary."

**Result**: It implemented the spending report in the code and gave a descritpion on what it did and why. The AI also formatted it to look like a professional financial summary. 

**Reflection**: What worked well was that AI was able to format it like a professional financial summary and keep it structured and clear. What didn't work well was that AI didn't explain what it did until I had to ask what it did and why it did it, I learned that AI can structure things better and professionally which saves alot of time especially for those who need things done quickly. 


### AI Collaboration # 4
**Context**: Needed AI to generate CSV transaction sample data for the starter notebook. 

**Prompt**: "Hi Claude could you create realistic sample transaction data that includes Australia businesses and various spending categories."

**Result**: Claude generated a file of sample transaction data, transactions that included the date, amount, time, category, description. Was able to implement in the cell and answer the following questions in assisting in building my Finance Assistant. 

**Reflection**: What worked well was that AI could generate this list in a short time and give me data to work off for my project, there wasn't much the didn't work well in this scenario as its pretty hard to mess up for the AI I think. 


### AI Collaboration # 5 
**Context**: Help brainstorm a finance problem as instructed by the starter notebook using the example prompt given. 

**Prompt**: Help me brainstorm specific personal finance problems that could be solved
with a CSV analysis tool. I'm interested in helping people with budgeting and spending awareness. What are common financial challenges that data analysis could address?"

**Result**: Here are common budgeting and spending-awareness problems that a CSV of transactions can address. They’re grouped by what the analysis actually does with the data.

1. “Where did my money go?”

Problem: people can’t say what they spent last month, only that the account is low.
Analysis: categorise each transaction and total it by category, then show each category as a percentage of spending.
Output: “Dining out was 18% of your spending, $612 across 31 transactions.”

2. Small purchases that add up

Problem: $6 coffees and $20 delivery orders feel harmless one at a time.
Analysis: group by merchant or category and count the frequency, so the total is shown next to the number of purchases.
Output: “You bought coffee 22 times this month for $142. Over a year that’s about $1,700.”

3. Forgotten or creeping subscriptions

Problem: people pay for services they’ve stopped using, and prices rise without notice.
Analysis: find charges with the same merchant and similar amount that repeat monthly, then flag price changes.
Output: “5 recurring charges total $187/month. Netflix rose from $16.99 to $18.99.”

**Reflection**: AI again was able to generate multiple finance problems to help tackle my challenge and this helped me brainstorm what finance problem I wanted my Finance Assistant to tackle. Everything worked well for this section, I liked how AI listed problems and the analysis to further explain these financial problems people face in their day to day lives.

### AI Collaboration # 6 
***Context**: Using AI to help find what inputs and outputs I should collect for my finance tracker and what I should expect for a good result, following the starter notebooks prompt. 

**Prompt**: "For a personal finance assistant that analyzes CSV transaction data, what are the most valuable inputs I should collect and outputs I should provide? Consider both technical data processing and business value for the user." 

**Result**: Inputs
Input	Technical considerations	Business value	Keep?
Transaction CSV (date, description, amount)	Clean $ signs, commas and mixed date formats, remove duplicates and bad rows, and decide the sign convention for spending vs income	The raw material for everything else	Required
Savings goal amount	A number greater than 0	Gives the analysis a target	Required
Deadline (months or years)	A whole number greater than 0, and convert years to months	Turns a wish into a plan	Required
Current savings	Optional, default 0, can’t be negative	Makes the monthly figure realistic	Optional
Interest rate	Optional, default 0	Shows what a savings account would add	Optional
Category (if the bank provides it)	Otherwise auto-categorise from the description with keyword rules	Shows where money goes	Derived
Monthly income	Can be detected from salary rows in the CSV, or entered manually	Needed for savings rate and budget percentages	Derived or manual
Chat questions	Free text, passed to the LLM	Personalised coaching	Required
Extra documents (notes, budget tips)	.txt/.md files for RAG	Grounds the advice in real sources	Optional
Outputs
Output	Technical considerations	Business value	Keep?
Monthly saving needed	Compound-interest formula, with edge cases like a goal already reached	The number that answers “what do I do?”	Core
Savings rate (income − spending) ÷ income	Handle zero income	Shows whether the person is on track	Core
Spending by category	groupby plus a sort	Makes spending visible	Core
Feasibility check: can they afford the required monthly amount?	Compare the required amount to the actual monthly surplus	The most actionable output: “your goal needs $258/mo but you currently save $297/mo, so you’re fine”	Core
Top habits to trim (small frequent purchases, subscriptions)	Frequency counts and recurring-charge detection	Shows concrete places to find savings	Strong
Coach message with a tip	LLM with a system prompt, grounded in the analysis numbers	Motivation, which is half the problem	Core
Month-to-month trend	Group by month and compare	Shows if things are getting better or worse	Nice to have
Unusual transactions	Outlier detection	Catches errors and one-offs	Nice to have
Chart (spending by category)	One simple Gradio plot	Faster to understand than a table	Nice to have
Cleaning report: how many rows were removed and why	Count rows before and after	Builds trust in the numbers	Good for testing

**Reflection**: AI created two clean tables showing what Inputs I should be collecting, or ensuring I use to get effective use from my finance assistant, Maybe a problem was that AI generated a bit too much to keep track of but the tables compensated for it. 

### AI Collaboration # 7
***Context**: Using AI to help generate realistic examples of Australian transactions to help with manual calculations, using the starer notebook prompt. 

**Prompt**: Give me 3 realistic examples of Australian transaction data with different scenarios (normal spending, refunds, large purchases). Show me how to manually calculate meaningful financial insights from each scenario." 

**Result**: Scenario 1: Normal spending (one fortnight)
Date	Description	Category	Amount
02/10	Salary, ACME Logistics	Income	+2,865.40
03/10	Ray White Rent	Housing	−1,150.00
03/10	Woolworths Canning Vale	Groceries	−112.35
04/10	Ampol Canning Vale	Transport	−78.20
05/10	Telstra Mobile	Utilities	−69.00
06/10	Dome Cafe Fremantle	Dining	−6.80
08/10	Uber Eats	Dining	−38.90
09/10	Netflix	Entertainment	−18.99
09/10	Spotify	Entertainment	−13.99
10/10	Coles Southlake	Groceries	−64.80
11/10	Hungry Jacks	Dining	−14.50
12/10	Transperth SmartRider	Transport	−20.00

By hand

Income: $2,865.40
Total spending: add all the negatives: 1,150.00 + 112.35 + 78.20 + 69.00 + 6.80 + 38.90 + 18.99 + 13.99 + 64.80 + 14.50 + 20.00 = $1,587.53
Net saved: 2,865.40 − 1,587.53 = $1,277.87
Savings rate: 1,277.87 ÷ 2,865.40 × 100 = 44.6%
By category (% of spending): Housing $1,150.00 (72.4%), Groceries $177.15 (11.2%), Transport $98.20 (6.2%), Utilities $69.00 (4.3%), Dining $60.20 (3.8%), Entertainment $32.98 (2.1%). These add up to 100%.
Fixed vs flexible: fixed costs are rent + phone + Netflix + Spotify = $1,251.98 (78.9% of spending). Flexible is $335.55 (groceries, transport, dining).

Insight: this person saves a lot in this fortnight. But 79% of spending is fixed, so the room to cut is the $335.55 flexible portion, and dining ($60.20) is the easiest part of it.

Scenario 2: Refunds (one month of shopping)
Date	Description	Category	Amount
02/09	Kmart Carillon	Shopping	−85.00
04/09	JB Hi-Fi Garden City	Shopping	−279.00
06/09	The Iconic	Shopping	−160.00
10/09	Bunnings Warehouse	Shopping	−140.00
12/09	Kmart Carillon (refund)	Shopping	+25.00
15/09	The Iconic (refund)	Shopping	+160.00
18/09	Bunnings (return)	Shopping	+62.50
20/09	Woolworths Canning Vale	Groceries	−95.20

By hand (Shopping only)

Gross shopping: 85.00 + 279.00 + 160.00 + 140.00 = $664.00
Refunds: 25.00 + 160.00 + 62.50 = $247.50
Net shopping: 664.00 − 247.50 = $416.50
Refund share: 247.50 ÷ 664.00 × 100 = 37.3% of what was bought came back
The trap: if you only add up the negative amounts, you get $664.00. That overstates real spending by 247.50 ÷ 416.50 = 59.4%.

Insight: refunds should be netted against the category they belong to, not counted as income. Otherwise spending looks too high, and if refunds are added to income, income looks too high. A pattern also shows up: 3 of the 4 purchases were returned (75%), which a coach could point out as impulse buying.

Scenario 3: Large purchase (one month with a trip)
Item	Category	Amount
Salary × 2	Income	+5,730.80
Rent × 2	Housing	−2,300.00
Groceries	Groceries	−480.00
Dining	Dining	−210.00
Transport	Transport	−260.00
Bills	Utilities	−320.00
Subscriptions	Entertainment	−32.98
Qantas Perth–Melbourne	Travel	−318.00
Airbnb Melbourne	Travel	−412.50

By hand

Total spending: 2,300.00 + 480.00 + 210.00 + 260.00 + 320.00 + 32.98 + 318.00 + 412.50 = $4,333.48
Net saved: 5,730.80 − 4,333.48 = $1,397.32, a savings rate of 24.4%
The trip: 318.00 + 412.50 = $730.50, or 16.9% of the month’s spending
Without the trip: spending is 4,333.48 − 730.50 = $3,602.98, net saved is $2,127.82, and the rate is 37.1%
Spread over time: $730.50 ÷ 12 = $60.88 a month (or $121.75 a month if saved over 6 months)

**Reflection**: AI was useful in generating realistic Australian transactions to help me with my manual calculations, however AI generated alot of content for such a simple question in my opinion and it guided me through manual calculations which I felt like I could've done myself. 

### AI Collaboration # 8 

***Context**: Writing Pseudocode basically sketching the algorithm in plain english before coding, using the example prompt from the starter notebook. 

**Prompt**: FUNCTION analyze_spending_data(csv_file):
    // Step 1: Load and validate data
    - Read CSV file into DataFrame
    - Check for required columns (Date, Amount, Category, Description)
    - Handle missing or invalid data
    
    // Step 2: Clean financial data  
    - Remove dollar signs from Amount column
    - Convert to numeric values
    - Separate positive spending from refunds
    
    // Step 3: Calculate business metrics
    - Group transactions by category
    - Calculate totals, averages, counts per category
    - Identify spending patterns and outliers
    
    // Step 4: Generate insights
    - Calculate percentages of total spending
    - Identify top spending categories
    - Suggest potential savings opportunities
    
    // Step 5: Format for presentation
    - Create business-friendly output
    - Include currency formatting
    - Add explanatory text for insights
    
    RETURN formatted_analysis
"Review my pseudocode for analyzing spending data from a CSV. Are there any edge cases I'm missing? What business logic should I add to make this more valuable for personal finance insights?"

**Result**: FUNCTION analyze_spending_data(csv_file):
    # 1. Load and validate
    TRY read CSV                     ON FAIL -> RETURN error message
    normalise column names (strip, lowercase, map aliases)
    IF date or amount column missing -> RETURN error message
    IF category column missing -> create it from description keyword rules
    IF fewer than 1 valid row -> RETURN "not enough data"

    # 2. Clean (and keep a report of what was removed)
    parse dates (ISO first, then day/month/year); invalid -> drop, count
    parse amounts (remove $ and commas, "(x)" -> negative); invalid -> drop, count
    remove exact duplicates, count
    remove internal transfers, count
    cleaning_report = {rows_in, rows_out, dropped by reason}

    # 3. Split
    income    = rows where amount > 0 and category is Income
    refunds   = rows where amount > 0 and category is not Income
    spending  = rows where amount < 0
    net spending per category = spending - refunds in that category

    # 4. Metrics (guard every division)
    months = days between first and last date / 30.44
    savings_rate = (income - net spending) / income   IF income > 0
    per category: total, count, average, share of net spending
    fixed vs flexible split
    month-by-month totals and change vs average
    recurring charges (same merchant, similar amount, about monthly)
    one-offs: transactions above threshold; savings rate without them
    uncategorised share

    # 5. Insights (rules on the numbers)
    top 3 categories
    FOR each rule (dining > 15%, subscription total, category up > 20%, ...):
        IF triggered -> add insight text using the actual numbers
    IF goal given -> feasibility = monthly surplus vs monthly saving needed

    # 6. Return
    RETURN { metrics, insights, cleaning_report }     # data, not text
    FUNCTION format_report(result) -> currency-formatted summary   # separate step

**Reflection**: The AI managed to polish up on the pseudocode and add lists its own recommendation and what I should add to the pseudocode before I start actually coding, again it gave me a bunch of information which was difficult to look at first but going through its section by section helped developed my understanding for this pseudocode writing. 

### AI Collaboration # 9 

***Context**: Using AI to help convert the pseudocode into python following the starter notebook instructions and prompt. 

**Prompt**: "I'm implementing a Smart Finance Assistant. Based on my pseudocode, please create
a Python function that [specific functionality]. The code should:
- Handle real-world CSV data issues (dollar signs, missing values)
- Include clear comments explaining business logic
- Use professional variable names
- Format output for business presentation
- Include basic error handling"

**Result**: """
Tests for spending_analysis.py  (Step 6: Test with a Variety of Data)
Run:  python test_spending_analysis.py        (from the folder containing the CSV files)
In a notebook: paste the body of run_all_tests() into your Testing section.
"""
import math

from spending_analysis import (analyze_spending_data, format_report, parse_amount, parse_date,
                               categorise_description, money)

# ---- Test data dictionaries (spending POSITIVE, refunds NEGATIVE, as in the assignment example) ----
sample_transactions = {
    'Date':        ['2026-08-01', '2026-08-02', '2026-08-03', '2026-08-04', '2026-08-05',
                    '2026-08-06', '2026-08-07', '2026-08-08'],
    'Amount':      ['$45.50', '$12.00', '$89.95', '$3.50', '-$25.00', '$1,250.00', '$68.40', '$7.20'],
    'Category':    ['Groceries', 'Transport', 'Entertainment', 'Coffee', 'Refund',
                    'Rent', 'Utilities', 'Dining'],
    'Description': ['Woolworths Canning Vale', 'Transperth SmartRider', 'Ticketek Concert',
                    'Campus Cafe Curtin', 'Kmart Returned Item', 'Ray White Rent',
                    'Synergy Electricity', 'Boost Juice Garden City'],
}
edge_case_transactions = {
    'Date':        ['2026-08-01', '2026-08-01', '01/08/2026', 'not a date', '2026-08-09',
                    '2026-08-10', '', '2026-08-12', '2026-08-13'],
    'Amount':      ['$45.50', '$45.50', '$1,203.50', '$12.00', '',
                    '(25.00)', '$9.99', '0.00', 'abc'],
    'Category':    ['Groceries', 'Groceries', 'rent', 'Transport', 'Dining',
                    'Refund', 'Coffee', 'Other', 'Shopping'],
    'Description': ['Woolworths', 'Woolworths', '  RENT payment  ', 'Transperth', 'Hungry Jacks',
                    'Bunnings Return', 'Dome Cafe', 'Mystery charge', 'Amazon AU'],
}


def approx(a, b, tol=0.01):
    return abs(a - b) <= tol


def run_all_tests():
    # 1. Helper functions ------------------------------------------------------
    assert parse_amount("$1,203.50") == 1203.50
    assert parse_amount("-$25.00") == -25.0
    assert parse_amount("$-25.00") == -25.0
    assert parse_amount("(25.00)") == -25.0
    assert parse_amount(45.5) == 45.5
    assert parse_amount("") is None and parse_amount("abc") is None and parse_amount(None) is None
    assert str(parse_date("2026-08-01").date()) == "2026-08-01"        # ISO is not flipped
    assert str(parse_date("01/08/2026").date()) == "2026-08-01"        # day-first
    assert str(parse_date("03/04/2026").date()) == "2026-04-03"        # ambiguous date read day-first
    assert parse_date("not a date") is parse_date("") or str(parse_date("")) == "NaT"
    assert categorise_description("WOOLWORTHS CANNING VALE") == "Groceries"
    assert categorise_description("UBER EATS") == "Dining"
    assert categorise_description("UBER TRIP PERTH") == "Transport"
    assert categorise_description("BPAY something") == ""             # 'bp' must not match inside 'BPAY'
    assert money(1234.5) == "$1,234.50" and money(-5) == "-$5.00"
    print("OK 1: helper functions")

    # 2. Clean sample CSV (364 rows) --------------------------------------------
    r = analyze_spending_data("sample_transactions.csv")
    assert r["ok"] and r["cleaning_report"]["rows_out"] == 364
    t = r["totals"]
    assert approx(t["income"], 37938.70) and approx(t["net_spending"], 36156.03)
    assert approx(t["net_saved"], 1782.67) and t["savings_rate_pct"] == 4.7
    cats = r["categories"].set_index("category")
    assert approx(cats.loc["Housing", "net_spending"], 15562.40)
    assert r["categories"].iloc[0]["category"] == "Housing"           # sorted, biggest first
    assert approx(r["categories"]["share_pct"].sum(), 100, 0.5)       # shares add up to ~100%
    assert "Other" not in cats.index                                  # every merchant categorised
    assert any("RENT" in m for m in r["recurring"]["merchant"])       # rent detected as recurring
    assert not any(r["one_offs"]["category"].isin(["Housing", "Utilities", "Insurance"]))
    names = " ".join(r["one_offs"]["description"])
    assert "QANTAS" in names and "AIRBNB" in names                    # trip flagged as one-off
    assert r["savings_rate_without_one_offs_pct"] > t["savings_rate_pct"]
    print("OK 2: clean CSV")

    # 3. Messy CSV: bad rows removed and reported ----------------------------------
    r = analyze_spending_data("messy_transactions.csv")
    rep = r["cleaning_report"]
    assert r["ok"] and rep["rows_in"] == 366 and rep["rows_out"] == 362
    assert rep["dropped_invalid_date"] == 2          # 'not a date' + blank row
    assert rep["dropped_invalid_amount"] == 1        # missing amount
    assert rep["dropped_duplicates"] == 1
    assert rep["rows_in"] - rep["rows_out"] == sum(v for k, v in rep.items() if k.startswith("dropped_"))
    print("OK 3: messy CSV")

    # 4. Dict inputs with spending positive ------------------------------------------
    r = analyze_spending_data(sample_transactions, spending_is_negative=False)
    assert r["ok"] and r["cleaning_report"]["rows_out"] == 8
    t = r["totals"]
    assert approx(t["gross_spending"], 1476.55) and approx(t["refunds"], 25.0)
    assert approx(t["net_spending"], 1451.55)        # refund reduces spending
    assert t["income"] == 0 and t["savings_rate_pct"] is None   # no income -> no divide-by-zero
    cats = r["categories"].set_index("category")
    assert approx(cats.loc["Dining", "net_spending"], 10.70)    # 'Coffee' aliased to Dining
    assert approx(cats.loc["Housing", "net_spending"], 1250.0)  # 'Rent' aliased to Housing
    assert "No income" in " ".join(r["insights"])
    print("OK 4: sample dict")

    r = analyze_spending_data(edge_case_transactions, spending_is_negative=False)
    rep = r["cleaning_report"]
    assert r["ok"] and rep["rows_in"] == 9 and rep["rows_out"] == 4
    assert rep["dropped_invalid_date"] == 2 and rep["dropped_invalid_amount"] == 2
    assert rep["dropped_duplicates"] == 1
    assert approx(r["totals"]["refunds"], 25.0)                 # "(25.00)" read as a refund
    assert approx(r["totals"]["gross_spending"], 45.50 + 1203.50)
    print("OK 4b: edge-case dict")

    # 5. Savings goal feasibility ----------------------------------------------------
    on_track = analyze_spending_data("sample_transactions.csv", required_monthly_saving=250.0)
    assert any("On track" in s for s in on_track["insights"])           # surplus is about $296/month
    short = analyze_spending_data("sample_transactions.csv", required_monthly_saving=900.0)
    assert any("Shortfall" in s for s in short["insights"])
    print("OK 5: goal feasibility")

    # 6. Error handling: never raises -------------------------------------------------
    bad_inputs = {
        "missing file": "no_such_file.csv",
        "empty dict": {},
        "missing column": {"Date": ["2026-01-01"], "Description": ["x"]},
        "all rows invalid": {"Date": ["bad"], "Amount": ["abc"], "Description": ["x"]},
    }
    for label, bad in bad_inputs.items():
        out = analyze_spending_data(bad)
        assert out["ok"] is False and out["error"], label
        assert format_report(out).startswith("Could not analyse"), label
    print("OK 6: error handling")

    # 7. Tiny and unusual data ----------------------------------------------------------
    one_row = analyze_spending_data({"date": ["2026-08-01"], "description": ["Woolworths"], "amount": ["-50"]})
    assert one_row["ok"] and approx(one_row["totals"]["net_spending"], 50)
    assert one_row["period"]["months_covered"] == 1.0                    # never extrapolates short data
    income_only = analyze_spending_data({"date": ["2026-08-01"], "description": ["Salary"], "amount": ["1000"]})
    assert income_only["ok"] and income_only["totals"]["net_spending"] == 0
    assert income_only["totals"]["savings_rate_pct"] == 100.0
    transfer = analyze_spending_data({"date": ["2026-08-01", "2026-08-02"],
                                      "description": ["Transfer to savings", "Coles"],
                                      "amount": ["-500", "-20"]})
    assert transfer["cleaning_report"]["dropped_transfers"] == 1
    assert approx(transfer["totals"]["net_spending"], 20)
    print("OK 7: tiny and unusual data")

    # 8. Report formatting -----------------------------------------------------------------
    text = format_report(analyze_spending_data("sample_transactions.csv"))
    for needle in ("SPENDING REPORT", "$37,938.70", "SPENDING BY CATEGORY", "INSIGHTS", "DATA QUALITY"):
        assert needle in text, needle
    print("OK 8: report formatting")
    print("\nAll tests passed.")


if __name__ == "__main__":
    run_all_tests()

**Reflection**: AI managed to generate and convert my pseudocode to python and assist in building my finance assistant. AI code did run into errors but with simple fixes the code is able to run. 

## AI Collaboration # 10 



