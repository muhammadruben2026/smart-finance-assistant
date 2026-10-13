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
**Context**: Using AI to create a comprehensive spending analysis following the starter notebook instructions and prompt. 
**Prompt**: "Create a function that analyzes spending by category, calculates percentages, identifies top spending areas, and generates actionable financial insights formatted for business presentation."
**Result**: import re

import pandas as pd

# =============================================================================
# BUSINESS RULES - edit these to tune the analysis
# =============================================================================
SMALL_PURCHASE_LIMIT = 25.00      # purchases under this count as "small habit" spending
TRIM_PERCENT = 20                 # the "what if you cut X by 20%" suggestion
DAYS_PER_MONTH = 30.44

# 50/30/20 budgeting rule: needs ~50% of income, wants ~30%, savings ~20%
NEEDS = {"Housing", "Utilities", "Insurance", "Groceries", "Transport", "Health"}
WANTS = {"Dining", "Entertainment", "Shopping", "Travel", "Cash"}

# Your own category names are mapped onto the standard ones
_ALIASES = {"coffee": "Dining", "food": "Dining", "eating out": "Dining", "takeaway": "Dining",
            "rent": "Housing", "mortgage": "Housing", "bills": "Utilities",
            "salary": "Income", "wages": "Income", "refunds": "Refund", "returns": "Refund"}

# Keyword rules for Australian merchants (first match wins) - used when a row has no real category
_KEYWORDS = {
    "Income":        ["salary", "payroll", "wage", "ato tax refund", "interest paid", "payout"],
    "Groceries":     ["woolworths", "coles", "aldi", "iga", "grocery", "supermarket"],
    "Dining":        ["restaurant", "cafe", "coffee", "hungry jacks", "guzman", "subway", "boost juice",
                      "mcdonald", "uber eats", "doordash", "menulog", "pizza", "dan murphys"],
    "Transport":     ["ampol", "bp", "7-eleven", "united petrol", "fuel", "petrol", "uber trip",
                      "transperth", "smartrider", "parking", "rac wa car"],
    "Housing":       ["rent", "mortgage", "strata", "rates", "council"],
    "Utilities":     ["synergy", "water corporation", "atco gas", "electric", "telstra", "optus",
                      "aussie broadband", "internet", "nbn"],
    "Insurance":     ["medibank", "insurance", "bupa", "hcf"],
    "Entertainment": ["netflix", "spotify", "disney", "binge", "cinema", "eventbrite", "ticketek",
                      "steam", "youtube"],
    "Health":        ["chemist warehouse", "priceline", "pharmacy", "medical", "dental",
                      "anytime fitness", "gym"],
    "Travel":        ["qantas", "virgin australia", "jetstar", "airbnb", "booking.com"],
    "Shopping":      ["kmart", "bunnings", "jb hi-fi", "officeworks", "amazon", "target", "afterpay",
                      "the iconic", "ebay"],
    "Cash":          ["atm withdrawal"],
}
_RULES = {cat: re.compile(r"\b(?:" + "|".join(re.escape(k) for k in kws) + r")\b", re.IGNORECASE)
          for cat, kws in _KEYWORDS.items()}


def _guess_category(description):
    """Guess a category from the merchant text; '' if nothing matches."""
    for category, pattern in _RULES.items():
        if pattern.search(description):
            return category
    return ""


def _money(amount):
    """1234.5 -> $1,234.50 and -5 -> -$5.00"""
    return f"-${abs(amount):,.2f}" if amount < 0 else f"${amount:,.2f}"


def analyze_spending_patterns(df, spending_is_negative=None):
    """
    Analyze spending by category and generate actionable insights

    🤖 AI Collaboration Prompt:
    "Create a function that analyzes spending by category, calculates percentages,
    identifies top spending areas, and generates actionable financial insights
    formatted for business presentation."

    Args:
        df: Cleaned transaction DataFrame (columns Date, Amount, Category, Description,
            as returned by load_and_clean_transaction_data)
        spending_is_negative: True if purchases are negative numbers (bank CSV style),
            False if they are positive (refunds negative). Default None = detect automatically
            from which sign is more common.

    Returns:
        dict: "summary" (totals, savings rate), "by_category" (DataFrame), "top_categories",
              "small_purchases", "insights" (list of plain-English findings) and
              "report" (formatted text ready to print).

    Raises:
        ValueError: with a plain-English explanation if the data can't be analysed.
    """
    # --- 1. Validate the input --------------------------------------------------
    if not isinstance(df, pd.DataFrame) or df.empty:
        raise ValueError("There are no transactions to analyse. Load your data first with "
                         "load_and_clean_transaction_data().")
    data = df.rename(columns=lambda c: str(c).strip().title()).copy()
    missing = [c for c in ("Date", "Amount", "Description") if c not in data.columns]
    if missing:
        raise ValueError(f"The data is missing these column(s): {', '.join(missing)}. "
                         "Run it through load_and_clean_transaction_data() first.")
    if "Category" not in data.columns:
        data["Category"] = ""
    data["Date"] = pd.to_datetime(data["Date"], errors="coerce")
    data["Amount"] = pd.to_numeric(data["Amount"], errors="coerce")
    data = data.dropna(subset=["Date", "Amount"])
    if data.empty:
        raise ValueError("None of the rows had a usable date and amount.")

    # --- 2. Work out each row's category ---------------------------------------------
    def resolve(category, description):
        label = "" if pd.isna(category) else " ".join(str(category).split())
        if label.lower() in ("", "uncategorised", "uncategorized", "nan"):
            return _guess_category(str(description))            # '' if unknown (handled below)
        return _ALIASES.get(label.lower(), label.title())
    data["Category"] = [resolve(c, d) for c, d in zip(data["Category"], data["Description"])]

    # Make the sign consistent: spending negative, income and refunds positive
    detected = spending_is_negative is None
    if detected:
        # Look only at non-income rows: whichever sign is more common is the sign of a purchase
        non_income = data.loc[data["Category"] != "Income", "Amount"]
        spending_is_negative = bool((non_income < 0).sum() >= (non_income > 0).sum())
    if not spending_is_negative:
        not_income = data["Category"] != "Income"
        data.loc[not_income, "Amount"] = -data.loc[not_income, "Amount"]

    # Still unknown: money in is Income (or a Refund), money out is "Other"
    def fallback(category, description, amount):
        if category:
            return category
        if amount > 0:
            return "Refund" if re.search(r"refund|return", str(description), re.IGNORECASE) else "Income"
        return "Other"
    data["Category"] = [fallback(c, d, a) for c, d, a in zip(data["Category"], data["Description"], data["Amount"])]

    # --- 3. Totals (refunds reduce spending - they are not income) -------------------------
    start, end = data["Date"].min(), data["Date"].max()
    months = max(((end - start).days + 1) / DAYS_PER_MONTH, 1.0)      # never extrapolate short data

    income = data.loc[data["Category"] == "Income", "Amount"].sum()
    purchases = data[(data["Amount"] < 0) & (data["Category"] != "Income")]
    refunds = data[(data["Amount"] > 0) & (data["Category"] != "Income")]["Amount"].sum()
    net_spending = -purchases["Amount"].sum() - refunds
    net_saved = income - net_spending
    savings_rate = round(net_saved / income * 100, 1) if income > 0 else None      # guard divide-by-zero

    # --- 4. Spending by category: totals, share of spending, counts, averages ---------------
    rows = []
    for category, group in data[data["Category"] != "Income"].groupby("Category"):
        if category == "Refund":
            continue                                   # refunds with no category are handled above
        bought = group[group["Amount"] < 0]
        rows.append({"Category": category, "Total": -group["Amount"].sum(), "Transactions": len(bought),
                     "Average": (-bought["Amount"].sum() / len(bought)) if len(bought) else 0.0})
    by_category = pd.DataFrame(rows, columns=["Category", "Total", "Transactions", "Average"])
    total = by_category["Total"].sum()
    by_category["Share %"] = (by_category["Total"] / total * 100).round(1) if total > 0 else 0.0
    by_category["Per Month"] = by_category["Total"] / months
    by_category = by_category.sort_values("Total", ascending=False).reset_index(drop=True)
    top = by_category.head(3)
    top_categories = [{"category": r["Category"], "total": round(r["Total"], 2), "share_pct": r["Share %"]}
                      for r in top.to_dict("records")]

    # Small purchases: coffees, takeaway, top-ups - small one at a time, large in total
    # Subscriptions and top-ups (same merchant AND same amount in 3+ different months) are not "habits"
    charge_key = purchases["Description"].astype(str).str.upper() + "|" + purchases["Amount"].round(2).astype(str)
    months_seen = purchases.groupby(charge_key)["Date"].transform(lambda d: d.dt.strftime("%Y-%m").nunique())
    small = purchases[(purchases["Amount"].abs() < SMALL_PURCHASE_LIMIT) & (months_seen < 3)]
    small_total = -small["Amount"].sum()
    small_info = {"count": len(small), "total": round(float(small_total), 2),
                  "per_year": round(float(small_total / months * 12), 2)}

    needs = by_category.loc[by_category["Category"].isin(NEEDS), "Total"].sum()
    wants = by_category.loc[by_category["Category"].isin(WANTS), "Total"].sum()

    # --- 5. Insights: plain rules applied to the numbers (nothing is invented) ----------------
    insights = []
    if savings_rate is None:
        insights.append("No income was found, so a savings rate can't be calculated. "
                        "Check that salary rows are in the file.")
    elif net_saved < 0:
        insights.append(f"Spending was {_money(-net_saved)} more than income in this period.")
    elif savings_rate < 20:
        insights.append(f"Savings rate is {savings_rate}%, below the common 20% guide. "
                        "The suggestions below show where to find the difference.")
    else:
        insights.append(f"Savings rate is {savings_rate}%, at or above the common 20% guide.")

    if len(top):
        text = ", ".join(f"{r['Category']} ({r['Share %']}%)" for r in top.to_dict("records"))
        insights.append(f"Top spending areas: {text}.")
    if income > 0 and needs / income * 100 > 50:
        insights.append(f"Essentials (housing, bills, groceries, transport, health, insurance) take "
                        f"{needs / income * 100:.1f}% of income, above the 50% guide, "
                        "so most savings will need to come from the 'wants' below.")
    if income > 0 and wants / income * 100 > 30:
        insights.append(f"Wants (dining, entertainment, shopping, travel, cash) take "
                        f"{wants / income * 100:.1f}% of income, above the 30% guide.")

    bigger_wants = by_category[by_category["Category"].isin(WANTS) & (by_category["Total"] > 0)]
    if len(bigger_wants):
        row = bigger_wants.iloc[0]
        saving = row["Per Month"] * TRIM_PERCENT / 100
        insights.append(f"Action: cutting {row['Category']} by {TRIM_PERCENT}% would free up about "
                        f"{_money(saving)} a month ({_money(saving * 12)} a year).")
    if small_info["count"] >= 10:
        insights.append(f"Action: {small_info['count']} small purchases (under {_money(SMALL_PURCHASE_LIMIT)}) "
                        f"total {_money(small_info['total'])}, about {_money(small_info['per_year'])} a year. "
                        "Setting a weekly limit for these is an easy first step.")
    if refunds > 0:
        insights.append(f"Refunds of {_money(refunds)} were subtracted from spending (not counted as income).")
    other = by_category.loc[by_category["Category"] == "Other", "Share %"]
    if len(other) and other.iloc[0] > 20:
        insights.append(f"{other.iloc[0]}% of spending is 'Other', so the category breakdown is less reliable.")

    # --- 6. Format for presentation --------------------------------------------------------------
    rate_text = f"{savings_rate}%" if savings_rate is not None else "n/a"
    lines = ["SPENDING BY CATEGORY", "=" * 58,
             f"Period: {start:%d %b %Y} to {end:%d %b %Y} ({len(data)} transactions)", "",
             f"  Income             {_money(income):>14}",
             f"  Spending (net)     {_money(net_spending):>14}",
             f"  Saved              {_money(net_saved):>14}",
             f"  Savings rate       {rate_text:>14}", "",
             f"  {'Category':<16}{'Total':>13}{'Share':>8}{'Count':>7}{'Per month':>12}"]
    for r in by_category.to_dict("records"):
        lines.append(f"  {r['Category']:<16}{_money(r['Total']):>13}{r['Share %']:>7.1f}%"
                     f"{r['Transactions']:>7}{_money(r['Per Month']):>12}")
    lines += ["", "INSIGHTS"] + [f"  - {text}" for text in insights]
    if detected:
        sign = "negative" if spending_is_negative else "positive"
        lines.append(f"\nAssumption: purchases are {sign} numbers in your data (detected automatically; "
                     "pass spending_is_negative=True/False to override).")
    lines.append("\nGeneral information only, not licensed financial advice.")

    return {
        "summary": {"income": round(float(income), 2), "net_spending": round(float(net_spending), 2),
                    "net_saved": round(float(net_saved), 2),
                    "savings_rate_pct": None if savings_rate is None else float(savings_rate),
                    "refunds": round(float(refunds), 2), "months_covered": round(float(months), 2),
                    "purchases_are_negative": spending_is_negative},
        "by_category": by_category, "top_categories": top_categories,
        "small_purchases": small_info, "insights": insights, "report": "\n".join(lines),
    }


# Both names work
analyze_spending_by_category = analyze_spending_patterns


# ====================== TESTS ======================
import pandas as pd

load = load_and_clean_transaction_data
analyse = analyze_spending_by_category


def approx(a, b, tol=0.01):
    return abs(a - b) <= tol


def run_all_tests():
    probe = analyse(load("sample_transactions.csv", verbose=False))
    if probe is None:
        raise RuntimeError("analyse() returned nothing: the function in memory is the empty starter stub. "
                           "Delete the starter's 'def analyze_spending_patterns' cell, then run this cell again.")
    # 1. Sample CSV: no Category column, so categories are guessed from merchant names --------
    r = analyse(load("sample_transactions.csv", verbose=False))
    s = r["summary"]
    assert approx(s["income"], 37938.70) and approx(s["net_spending"], 36156.03)
    assert s["savings_rate_pct"] == 4.7 and s["purchases_are_negative"] is True
    categories = r["by_category"].set_index("Category")
    assert approx(categories.loc["Housing", "Total"], 15562.40)
    assert "Other" not in categories.index                       # every merchant was recognised
    assert approx(r["by_category"]["Share %"].sum(), 100, 0.5)   # shares add up to ~100%
    assert [t["category"] for t in r["top_categories"]] == ["Housing", "Groceries", "Dining"]
    assert r["by_category"]["Total"].is_monotonic_decreasing     # biggest first
    assert 60 <= r["small_purchases"]["count"] <= 90             # habits only, not subscriptions
    assert any("Action" in text for text in r["insights"])
    for heading in ("SPENDING BY CATEGORY", "INSIGHTS", "$37,938.70"):
        assert heading in r["report"]
    print("OK 1: sample CSV")

    # 2. Messy data (typed in here, so no extra file is needed): $ signs, a comma, brackets,
    #    a duplicate, a bad date and missing amounts
    messy = load({
        'Date':        ['2026-08-01', '2026-08-01', '01/08/2026', 'not a date', '2026-08-09',
                        '2026-08-10', '', '2026-08-12', '2026-08-13'],
        'Amount':      ['$45.50', '$45.50', '$1,203.50', '$12.00', '',
                        '(25.00)', '$9.99', '0.00', 'abc'],
        'Category':    ['Groceries', 'Groceries', 'rent', 'Transport', 'Dining',
                        'Refund', 'Coffee', 'Other', 'Shopping'],
        'Description': ['Woolworths', 'Woolworths', '  RENT payment  ', 'Transperth', 'Hungry Jacks',
                        'Bunnings Return', 'Dome Cafe', 'Mystery charge', 'Amazon AU']}, verbose=False)
    assert len(messy) == 4 and messy.attrs["cleaning_report"]["duplicates"] == 1
    m = analyse(messy)
    assert approx(m["summary"]["net_spending"], 1224.00)         # 45.50 + 1,203.50 - 25.00 refund
    assert approx(m["summary"]["refunds"], 25.0)
    assert m["summary"]["savings_rate_pct"] is None              # no income rows
    print("OK 2: messy data")

    # 3. Assignment-style data: purchases POSITIVE, refund negative, no income ------------------------
    data = load({'Date': ['2026-08-01', '2026-08-02', '2026-08-03', '2026-08-04', '2026-08-05',
                          '2026-08-06', '2026-08-07', '2026-08-08'],
                 'Amount': ['$45.50', '$12.00', '$89.95', '$3.50', '-$25.00', '$1,250.00', '$68.40', '$7.20'],
                 'Category': ['Groceries', 'Transport', 'Entertainment', 'Coffee', 'Refund',
                              'Rent', 'Utilities', 'Dining'],
                 'Description': ['Woolworths', 'Transperth', 'Ticketek', 'Campus Cafe', 'Kmart Return',
                                 'Ray White Rent', 'Synergy', 'Boost Juice']}, verbose=False)
    r = analyse(data)
    assert r["summary"]["purchases_are_negative"] is False       # sign detected automatically
    assert approx(r["summary"]["net_spending"], 1451.55) and approx(r["summary"]["refunds"], 25.0)
    assert r["summary"]["savings_rate_pct"] is None              # no income: no divide-by-zero
    assert any("No income" in text for text in r["insights"])
    categories = r["by_category"].set_index("Category")
    assert approx(categories.loc["Dining", "Total"], 10.70)      # 'Coffee' counted as Dining
    assert approx(categories.loc["Housing", "Total"], 1250.0)    # 'Rent' counted as Housing
    assert approx(analyse(data, spending_is_negative=False)["summary"]["net_spending"], 1451.55)
    print("OK 3: purchases-positive data")

    # 4. Unusual data ------------------------------------------------------------------------------
    income_only = analyse(pd.DataFrame({"Date": ["2026-08-01"], "Amount": [1000.0],
                                        "Category": ["Income"], "Description": ["Salary"]}))
    assert income_only["summary"]["savings_rate_pct"] == 100.0 and len(income_only["by_category"]) == 0
    one_row = analyse(pd.DataFrame({"date": ["2026-08-01"], "amount": [-50.0],      # lowercase columns
                                    "description": ["Woolworths"]}))                 # and no Category
    assert approx(one_row["summary"]["net_spending"], 50) and one_row["summary"]["months_covered"] == 1.0
    refund_netted = analyse(pd.DataFrame({
        "Date": ["2026-08-01", "2026-08-05", "2026-08-02"], "Amount": [-100.0, 40.0, 3000.0],
        "Category": ["Shopping", "Shopping", "Income"], "Description": ["Kmart", "Kmart refund", "Salary"]}))
    assert approx(refund_netted["by_category"].set_index("Category").loc["Shopping", "Total"], 60.0)
    assert refund_netted["summary"]["purchases_are_negative"] is True
    print("OK 4: unusual data")

    # 5. Friendly errors -------------------------------------------------------------------------------
    bad_inputs = {"empty DataFrame": pd.DataFrame(), "not a DataFrame": "file.csv",
                  "no Amount column": pd.DataFrame({"Date": ["2026-01-01"], "Description": ["x"]}),
                  "nothing usable": pd.DataFrame({"Date": ["x"], "Amount": ["y"], "Description": ["z"]})}
    for label, bad in bad_inputs.items():
        try:
            analyse(bad)
            raise AssertionError(f"{label}: should have raised ValueError")
        except ValueError as error:
            assert str(error)
    print("OK 5: error messages")
    print("\nAll tests passed.")


run_all_tests()

**Reflection**: AI was able to generate it efficiently but it made mistakes for example it was giving some terms that weren't defined yet so I had to fix them manually however AI made this process quick and gave me less manual work in general. 

## AI Collaboration # 11
**Context**: Using AI to help build Professional Financial Recommendations following the starter notebook insturctions and prompt. 
**Prompt**: "Based on spending analysis data, create professional financial recommendations. Include specific savings opportunities, spending pattern observations, and actionable advice formatted for a personal finance app user."
**Result**: # Business rules - edit these to tune the advice
CUT_PERCENT = 20          # how much of each "want" category to suggest trimming
TARGET_SAVINGS_RATE = 20  # common guide: save ~20% of income
SMALL_HABIT_CUT = 25      # suggest trimming small purchases by this percent
_REC_NEEDS = {"Housing", "Utilities", "Insurance", "Groceries", "Transport", "Health"}
_REC_WANTS = {"Dining", "Entertainment", "Shopping", "Travel", "Cash"}


def _dollars(amount):
    """1234.5 -> $1,234.50"""
    return f"-${abs(amount):,.2f}" if amount < 0 else f"${amount:,.2f}"


def generate_financial_recommendations(analysis_data):
    """
    Generate actionable financial recommendations based on spending analysis

    🤖 AI Collaboration Prompt:
    "Based on spending analysis data, create professional financial
    recommendations. Include specific savings opportunities, spending
    pattern observations, and actionable advice formatted for a
    personal finance app user."

    Args:
        analysis_data: Dictionary with spending analysis results
                       (the result of analyze_spending_patterns(df))
    Returns:
        str: Formatted recommendations report

    Raises:
        ValueError: if the analysis results are missing or incomplete.
    """
    # --- 1. Validate the input ----------------------------------------------------
    needed = ("summary", "by_category", "small_purchases")
    if not isinstance(analysis_data, dict) or any(key not in analysis_data for key in needed):
        raise ValueError("These recommendations need the results of the spending analysis. "
                         "Run  analysis = analyze_spending_patterns(df)  first, then pass `analysis` in.")
    summary, table, small = analysis_data["summary"], analysis_data["by_category"], analysis_data["small_purchases"]
    months = summary["months_covered"]
    income, saved, rate = summary["income"], summary["net_saved"], summary["savings_rate_pct"]
    monthly_income = income / months
    monthly_surplus = saved / months

    # --- 2. Spending pattern observations --------------------------------------------
    observations = []
    for row in table.head(3).to_dict("records"):
        observations.append(f"{row['Category']} is {row['Share %']}% of your spending "
                            f"({_dollars(row['Per Month'])} a month).")
    needs_total = table.loc[table["Category"].isin(_REC_NEEDS), "Total"].sum()
    wants_total = table.loc[table["Category"].isin(_REC_WANTS), "Total"].sum()
    needs_pct = wants_pct = None
    if income > 0:
        needs_pct, wants_pct = needs_total / income * 100, wants_total / income * 100
        observations.append(f"Essentials take {needs_pct:.1f}% of income (guide: 50%) and "
                            f"wants take {wants_pct:.1f}% (guide: 30%).")

    # --- 3. Savings opportunities: trim the biggest "wants" ---------------------------------
    wants = table[table["Category"].isin(_REC_WANTS) & (table["Total"] > 0)].sort_values("Per Month", ascending=False)
    opportunities, monthly_cuts = [], 0.0
    for row in wants.head(3).to_dict("records"):
        saving = row["Per Month"] * CUT_PERCENT / 100
        monthly_cuts += saving
        opportunities.append(f"{row['Category']}: trim by {CUT_PERCENT}% to save about "
                             f"{_dollars(saving)} a month ({_dollars(saving * 12)} a year).")
    habit_monthly = 0.0
    if small["count"] >= 10:
        habit_monthly = small["per_year"] * SMALL_HABIT_CUT / 100 / 12
        opportunities.append(f"Small purchases: {small['count']} purchases under $25 total {_dollars(small['total'])}. "
                             f"Trimming {SMALL_HABIT_CUT}% would save about {_dollars(habit_monthly)} a month "
                             "(this overlaps with the categories above).")

    # --- 4. Snapshot and the gap to the savings target ----------------------------------------
    snapshot, gap = [], None
    if income <= 0:
        snapshot.append("No income was found in the data, so a savings rate can't be calculated.")
    else:
        snapshot.append(f"Savings rate: {rate}% (guide: {TARGET_SAVINGS_RATE}%).")
        snapshot.append(f"Average monthly income {_dollars(monthly_income)}, "
                        f"saving about {_dollars(monthly_surplus)} a month.")
        gap = monthly_income * TARGET_SAVINGS_RATE / 100 - monthly_surplus

    # --- 5. Action plan (most important first) -----------------------------------------------------
    actions = []
    if gap is not None and gap <= 0:
        actions.append(f"You're at or above the {TARGET_SAVINGS_RATE}% guide. Move about {_dollars(monthly_surplus)} a "
                       "month into a separate savings account so it isn't spent.")
    elif gap is not None:
        if saved < 0:
            actions.append(f"Spending is {_dollars(-saved)} above income over this period, so the first priority is "
                           "bringing spending below income.")
        if monthly_cuts > 0 and saved < 0:
            actions.append(f"Start with the trims above, which free up about {_dollars(monthly_cuts)} a month, "
                           "then review essentials for further savings.")
        elif monthly_cuts > 0:
            share = min(monthly_cuts / gap * 100, 100)
            actions.append(f"Set up an automatic transfer of about {_dollars(monthly_cuts)} on payday, funded by the "
                           f"trims above. That closes roughly {share:.0f}% of the {_dollars(gap)} monthly gap to "
                           f"a {TARGET_SAVINGS_RATE}% savings rate.")
        else:
            actions.append(f"Find about {_dollars(gap)} a month to reach a {TARGET_SAVINGS_RATE}% savings rate.")
    if habit_monthly > 0:
        weekly_cap = small["per_year"] / 52 * (1 - SMALL_HABIT_CUT / 100)
        actions.append(f"Set a weekly limit of about {_dollars(weekly_cap)} for small purchases like coffee and takeaway.")
    if needs_pct is not None and needs_pct > 50:
        actions.append(f"Essentials are {needs_pct:.0f}% of income. Compare providers for insurance, phone, internet "
                       "and energy, since cutting wants alone may not be enough.")
    actions.append("Re-run this report next month to see whether the changes are working.")

    # --- 6. Format the report ------------------------------------------------------------------------------
    def section(title, items, numbered=False):
        lines = ["", title]
        for number, item in enumerate(items, 1):
            lines.append(f"  {number}. {item}" if numbered else f"  - {item}")
        return lines

    report = ["FINANCIAL RECOMMENDATIONS", "=" * 58]
    report += section("YOUR SNAPSHOT", snapshot)
    report += section("WHERE YOUR MONEY GOES", observations)
    if opportunities:
        report += section("SAVINGS OPPORTUNITIES", opportunities)
    report += section("YOUR ACTION PLAN", actions, numbered=True)
    report += ["", "General information only, not licensed financial advice."]
    return "\n".join(report)

**Reflection**: AI able to output it quickly and I had to make 2 manual adjustments other than that all good.

## AI Collaboration # 12 
**Context**: Using AI to help build a Financial Advice Chatbot that can give recommendations on budgeting and spending habits, building this chatbot using instructions from the starter notebook and prompt. 
**Prompt**: Help me create a system prompt for a friendly, professional financial advisor chatbot that can provide spending advice based on transaction analysis. The personality should be encouraging but practical. 
**Result**: import os

import requests

# One cell, no extra packages: Penny talks to Gemini directly using the key in your Colab Secrets.
GEMINI_API = "https://generativelanguage.googleapis.com/v1beta"
SECRET_NAMES = ("GEMINI_API_KEY", "GOOGLE_API_KEY", "GEMINI_KEY", "GOOGLE_GEMINI_API_KEY", "GEMINI")
SKIP_WORDS = ("lite", "image", "tts", "live", "audio", "embed", "vision", "exp", "thinking")

PENNY_PERSONA = """You are Penny, a friendly and professional personal finance coach for Australians.
Be warm, encouraging and practical. Use plain language and short answers (3 to 6 sentences) with one or
two specific next steps. Amounts are in Australian dollars. Use the user's spending facts below when they
are provided, and never invent transactions or figures. You give general financial education, not licensed
advice; for big decisions suggest a licensed adviser."""


def _find_key():
    """Read the Gemini key from Colab Secrets (it is never printed)."""
    try:
        from google.colab import userdata
    except ImportError:
        return os.environ.get("GEMINI_API_KEY") or os.environ.get("GOOGLE_API_KEY")
    for name in SECRET_NAMES:
        try:
            return userdata.get(name)
        except Exception:                 # secret missing, or 'Notebook access' is off
            continue
    return None


def _api_error(reply):
    """Short, readable reason from a failed Gemini request."""
    try:
        detail = reply.json()["error"]["message"]
    except Exception:
        detail = reply.text[:200]
    hints = {400: "the key may be invalid", 401: "the key was rejected", 403: "the key doesn't have access",
             404: "the model name wasn't found", 429: "too many requests or the free limit was reached"}
    return f"HTTP {reply.status_code} ({hints.get(reply.status_code, 'request failed')}): {detail}"


GEMINI_KEY = _find_key()
GEMINI_MODEL = None
if not GEMINI_KEY:
    print("No Gemini key found. Click the key icon (Secrets) on the left, add a secret named GEMINI_API_KEY "
          "with your key, switch 'Notebook access' on, then run this cell again.")
else:
    try:                                   # pick a current Gemini 'flash' model that can chat
        reply = requests.get(f"{GEMINI_API}/models", headers={"x-goog-api-key": GEMINI_KEY},
                             params={"pageSize": 200}, timeout=20)
        reply.raise_for_status()
        names = [m["name"].split("/")[-1] for m in reply.json().get("models", [])
                 if "generateContent" in m.get("supportedGenerationMethods", [])]
        flash = sorted((n for n in names if n.startswith("gemini") and "flash" in n
                        and not any(word in n for word in SKIP_WORDS)), reverse=True)
        GEMINI_MODEL = (flash or [n for n in names if n.startswith("gemini")] or ["gemini-2.5-flash"])[0]
    except requests.HTTPError:
        print("Gemini rejected the request:", _api_error(reply))
    except Exception as problem:
        print("Could not reach Gemini:", problem)


def spending_facts():
    """Short summary of your analysis (if you have run analyze_spending_patterns) for Penny to use."""
    result = globals().get("analysis")
    if not isinstance(result, dict) or "summary" not in result:
        return ""
    s = result["summary"]
    lines = [f"Income ${s['income']:,.2f}, net spending ${s['net_spending']:,.2f}, saved ${s['net_saved']:,.2f} "
             f"over {s['months_covered']} months; savings rate {s['savings_rate_pct']}%."]
    lines += [f"{t['category']}: ${t['total']:,.2f} ({t['share_pct']}% of spending)"
              for t in result.get("top_categories", [])]
    lines += result.get("insights", [])[:5]
    return "\n".join(lines)


def penny_reply(message, history=None):
    """Ask Penny a question. `history` is optional: a list of {'role','content'} dicts or (user, bot) pairs."""
    if not GEMINI_KEY or not GEMINI_MODEL:
        return "Penny isn't connected yet. Run the setup above and check the message it printed."
    contents = []
    for turn in (history or [])[-8:]:
        pairs = ([("user" if turn["role"] == "user" else "model", str(turn["content"]))]
                 if isinstance(turn, dict) else [("user", str(turn[0])), ("model", str(turn[1]))])
        contents += [{"role": role, "parts": [{"text": text}]} for role, text in pairs if text]
    contents.append({"role": "user", "parts": [{"text": message}]})

    system_text = PENNY_PERSONA
    facts = spending_facts()
    if facts:
        system_text += "\n\nThe user's spending facts:\n" + facts
    try:
        reply = requests.post(f"{GEMINI_API}/models/{GEMINI_MODEL}:generateContent",
                              headers={"x-goog-api-key": GEMINI_KEY},
                              json={"system_instruction": {"parts": [{"text": system_text}]}, "contents": contents},
                              timeout=60)
        if not reply.ok:
            return "Sorry, Gemini returned an error: " + _api_error(reply)
        parts = reply.json()["candidates"][0]["content"]["parts"]
        return "".join(part.get("text", "") for part in parts).strip() or "(Penny had nothing to say, try rephrasing.)"
    except (KeyError, IndexError):
        return "Sorry, Gemini's reply was blocked or empty. Try rephrasing your question."
    except Exception as problem:
        return f"Sorry, I couldn't reach Gemini: {problem}"


if GEMINI_MODEL:
    print(f"Penny is connected (model: {GEMINI_MODEL}). Test reply:\n")
    print(penny_reply("Say hello and introduce yourself in two sentences."))

**Reflection**: The AI managed to help me build a chatbot however, the first chatbots weren't working then AI finally built a working one with Gemini other than that all good and quick with AI. 

## AI Collaboration # 13 
**Context**: Using AI to help build the RAG system within the Finance Assistant following the instructuions from the starter notebook and prompt. 
**Prompt**: Help me set up a RAG system that can retrieve information from financial documents, budgeting guides, and transaction summaries to answer user questions about personal finance.
**Result**: import math
import os
import re
from collections import Counter

# Optional: hands-on-ai embeddings are only used if you switch this on AND the AI server works.
# Keyword search (the default) needs no server, so the RAG always works.
USE_EMBEDDINGS = False
INDEX_PATH = "finance_index.npz"

# --- 1. The documents (budgeting guides and savings advice). Add or edit paragraphs freely. -------
FINANCE_DOCUMENTS = {
    "Budgeting guide: 50/30/20 rule": """
The 50/30/20 rule splits after-tax income into three parts: 50% for needs, 30% for wants and 20% for savings or debt repayment.
Needs are things you must pay such as rent, utilities, groceries, insurance, transport to work and minimum debt payments.
Wants are dining out, entertainment, shopping, holidays and subscriptions you could live without.
If your needs are above 50% of income, look at rent, energy, phone and insurance providers before cutting wants.
""",
    "Savings guide: emergency fund": """
An emergency fund is money kept aside for surprises such as car repairs, medical bills or losing a job.
A good first goal is $1,000, then build towards three to six months of essential expenses.
Keep the emergency fund in a separate high interest savings account so it is not spent by accident.
Automatic transfers on payday are the easiest way to build the fund because you never see the money.
""",
    "Savings guide: saving habits": """
Pay yourself first: move your savings out on payday, then spend what is left.
Set a clear goal with an amount and a date, then divide it by the number of weeks or months to get a regular amount.
Round up purchases, put windfalls like tax refunds and bonuses into savings, and review progress every month.
A savings rate of about 20% of income is a common target, but any regular saving is a good start.
""",
    "Spending guide: small purchases": """
Small purchases such as coffee, takeaway and snacks feel harmless but add up to hundreds or thousands of dollars a year.
Track purchases under $25 for a month to see the total, then set a weekly limit for them.
Cutting small purchases by a quarter is often easier than cutting a big bill, and the savings add up quickly.
""",
    "Spending guide: subscriptions": """
Subscriptions like streaming, music, gym and apps renew automatically and are easy to forget.
List every recurring charge, cancel what you have not used in a month and share family plans where you can.
Check your bank statement every three months for charges you do not recognise.
""",
    "Debt guide: paying off debt": """
List your debts with their interest rates. The avalanche method pays the highest interest debt first and saves the most money.
The snowball method pays the smallest balance first, which gives quick wins and keeps you motivated.
Always pay at least the minimum on every debt and avoid new credit card spending while you pay down balances.
""",
}

STOP_WORDS = set("a an and are as at be by can do does for from how i if in is it me my of on or so that the "
                 "this to was what when which with you your should would about get".split())


def _words(text):
    """Lower-case words with a tiny bit of stemming (savings -> saving, bills -> bill)."""
    found = []
    for word in re.findall(r"[a-z0-9$%]+", text.lower()):
        if word in STOP_WORDS:
            continue
        for ending in ("ings", "ing", "es", "s"):
            if word.endswith(ending) and len(word) - len(ending) >= 3:
                word = word[: -len(ending)]
                break
        found.append(word)
    return found


def _transaction_summaries():
    """Turn the cleaned transactions (`df`) into a few plain-English summary paragraphs, if df exists."""
    data = globals().get("df")
    if data is None or not hasattr(data, "columns") or not {"Date", "Amount"} <= set(data.columns):
        return {}
    try:
        table = data.copy()
        category = table["Category"] if "Category" in table.columns else "Uncategorised"
        table["_cat"] = category
        table["_month"] = table["Date"].dt.strftime("%B %Y")
        summaries = {}
        for month, rows in table.groupby("_month", sort=False):
            income = rows.loc[rows["_cat"] == "Income", "Amount"].sum()
            spend = rows.loc[rows["_cat"] != "Income"]
            if len(spend) and (spend["Amount"] < 0).sum() >= (spend["Amount"] > 0).sum():
                spend = spend.assign(Amount=-spend["Amount"])
            top = spend.groupby("_cat")["Amount"].sum().sort_values(ascending=False).head(3)
            parts = ", ".join(f"{name} ${value:,.2f}" for name, value in top.items())
            summaries[f"Transaction summary: {month}"] = (
                f"In {month} income was ${income:,.2f} and spending was ${spend['Amount'].sum():,.2f}. "
                f"The biggest spending categories were {parts}.")
        return summaries
    except Exception:
        return {}


def _split_into_chunks(text, max_words=70):
    """Split a document into short chunks (one per paragraph/line group)."""
    chunks, current = [], []
    for line in (l.strip() for l in text.strip().splitlines()):
        if line:
            current.append(line)
        if current and (not line or len(" ".join(current).split()) >= max_words):
            chunks.append(" ".join(current))
            current = []
    if current:
        chunks.append(" ".join(current))
    return chunks


def setup_financial_rag(extra_documents=None, use_embeddings=None):
    """
    Set up RAG system for financial documents and transaction data

    🤖 AI Collaboration Prompt:
    "Help me set up a RAG system that can retrieve information from financial
    documents, budgeting guides, and transaction summaries to answer user
    questions about personal finance."

    Args:
        extra_documents: optional dict {"name": "text"} of your own documents to add.
        use_embeddings: True to try hands-on-ai embeddings (needs a working AI server).
    Returns:
        function: retrieve(question, k=3) -> list of (chunk, source) tuples, best match first.
                  Also has .chunks, .method and .answer(question) attributes.
    """
    # --- Document ingestion: guides + your extra documents + summaries of your transactions ----------
    documents = dict(FINANCE_DOCUMENTS)
    documents.update(_transaction_summaries())
    if extra_documents:
        documents.update(extra_documents)
    chunks, sources = [], []
    for name, text in documents.items():
        for piece in _split_into_chunks(text):
            chunks.append(piece)
            sources.append(name)
    if not chunks:
        raise ValueError("No documents to search. Add some text to FINANCE_DOCUMENTS.")

    # --- Keyword index (always built, works offline) -----------------------------------------------------
    chunk_words = [Counter(_words(f"{source} {chunk}")) for chunk, source in zip(chunks, sources)]
    document_counts = Counter(word for words in chunk_words for word in words)

    def keyword_search(question, k):
        wanted = set(_words(question))
        scored = []
        for index, words in enumerate(chunk_words):
            score = sum((1 + math.log(1 + words[w])) * math.log(1 + len(chunks) / document_counts[w])
                        for w in wanted if w in words)
            if score > 0:
                scored.append((score, index))
        scored.sort(reverse=True)
        return [(chunks[i], sources[i]) for _, i in scored[:k]]

    # --- Optional: embeddings through hands-on-ai ---------------------------------------------------------
    embedding_search, method = None, "keyword search"
    if (USE_EMBEDDINGS if use_embeddings is None else use_embeddings) and os.environ.get("HANDS_ON_AI_SERVER"):
        try:
            from hands_on_ai.rag.utils import get_embeddings, get_top_k, save_index_with_sources
            save_index_with_sources(chunks, get_embeddings(chunks), sources, INDEX_PATH)
            embedding_search = lambda question, k: list(get_top_k(question, INDEX_PATH, k=k))
            method = "embeddings (hands-on-ai)"
        except Exception as problem:
            print("Embeddings aren't available, using keyword search instead:", str(problem)[:120])

    def retrieve(question, k=3):
        """Return the k most relevant (chunk, source) pairs for a question."""
        if not str(question).strip():
            return []
        if embedding_search:
            try:
                return embedding_search(question, k)
            except Exception:
                pass                                       # server went away: fall back to keywords
        return keyword_search(question, k)

    def answer(question, k=3):
        """Answer using the retrieved text. Uses Penny (the AI) if she is connected, else quotes the best matches."""
        found = retrieve(question, k)
        if not found:
            return "I couldn't find anything about that in my guides. Try asking about budgeting, saving or debt."
        context = "\n".join(f"- {chunk} [{source}]" for chunk, source in found)
        ask = globals().get("penny_reply")
        if ask and globals().get("GEMINI_MODEL"):
            reply = ask(f"Answer using ONLY this information, and mention the source name.\n{context}\n\nQuestion: {question}")
            if not reply.startswith(("Sorry", "Penny isn't")):
                return reply
        return "Here is what my guides say:\n" + context

    retrieve.answer, retrieve.chunks, retrieve.sources, retrieve.method = answer, chunks, sources, method
    print(f"RAG ready: {len(chunks)} chunks from {len(documents)} documents ({method}).")
    return retrieve


# --- Try it ----------------------------------------------------------------------------------------------------
rag_search = setup_financial_rag()
for question in ["How big should my emergency fund be?", "What is the 50/30/20 rule?",
                 "How can I cut down on coffee and takeaway?"]:
    print("\nQ:", question)
    for chunk, source in rag_search(question, k=2):
        print(f"  [{source}] {chunk[:110]}...")

**Reflection**: AI was able to get it perfect first try with little to no manual changes, AI was efficient in this task and all went perfect. 

## AI Collaboration # 14 
**Context**: Using AI to build a Custom Tool Development for the Finance Tracker following the starter notebook instructions and following prompt. 
**Prompt**: Create a savings goal calculator function that takes current savings, monthly contribution, and target amount, then calculates time to reach goal. Format output for user-friendly display.
**Result**: import math
import re
from datetime import date

from hands_on_ai import agent

MAX_MONTHS = 1200      # stop after 100 years: the goal is effectively out of reach


def calculate_savings_goal(current, monthly, target, annual_rate_pct=0.0):
    """Months needed to go from `current` to `target` saving `monthly` (optional yearly interest, in %)."""
    for name, value in (("current savings", current), ("monthly saving", monthly),
                        ("target", target), ("interest rate", annual_rate_pct)):
        if value is None or isinstance(value, bool) or not isinstance(value, (int, float)) or math.isnan(value):
            raise ValueError(f"The {name} must be a number.")
    if current < 0 or monthly < 0 or annual_rate_pct < 0:
        raise ValueError("Savings, monthly saving and interest rate can't be negative.")
    if target <= 0:
        raise ValueError("The target must be more than $0.")
    if annual_rate_pct > 100:
        raise ValueError("The interest rate looks too high. Enter it as a percent, for example 4.5.")

    result = {"current": current, "monthly": monthly, "target": target, "rate": annual_rate_pct}
    if current >= target:
        return {**result, "months": 0, "balance": current, "interest_earned": 0.0, "reached": True}

    monthly_rate, balance, months = annual_rate_pct / 100 / 12, current, 0
    while balance < target and months < MAX_MONTHS:
        balance = balance * (1 + monthly_rate) + monthly
        months += 1
        if monthly == 0 and monthly_rate == 0:
            break
    reached = balance >= target
    interest = balance - current - monthly * months
    return {**result, "months": months, "balance": balance, "interest_earned": max(interest, 0.0), "reached": reached}


def _add_months(start, months):
    index = start.year * 12 + start.month - 1 + months
    return date(index // 12, index % 12 + 1, 1)


def _format_goal(r):
    money = lambda x: f"${x:,.2f}"
    if r["months"] == 0:
        return f"Great news: you have already reached your {money(r['target'])} goal (you have {money(r['current'])})."
    if not r["reached"]:
        if r["monthly"] == 0:
            return "With $0 a month going in, you won't reach this goal. Try adding a regular monthly amount."
        return "At that pace the goal would take more than 100 years. Try a bigger monthly amount or a smaller target."
    years, months = divmod(r["months"], 12)
    time_text = " and ".join(part for part in (f"{years} year{'s' * (years != 1)}" if years else "",
                                               f"{months} month{'s' * (months != 1)}" if months else "") if part)
    lines = [f"SAVINGS GOAL: {money(r['target'])}",
             f"  Starting savings : {money(r['current'])}",
             f"  Saving each month: {money(r['monthly'])}" + (f"  (interest {r['rate']:g}% a year)" if r["rate"] else ""),
             f"  Time to goal     : {time_text} ({r['months']} months)",
             f"  Target date      : {_add_months(date.today(), r['months']).strftime('%B %Y')}"]
    if r["rate"]:
        lines.append(f"  Interest earned  : about {money(r['interest_earned'])}")
    lines.append(f"  Tip: saving an extra $50 a month would get you there sooner.")
    return "\n".join(lines)


def savings_goal_calculator(text):
    """
    Agent tool. Input: one text with 3 numbers (and an optional 4th):
    'current savings, monthly saving, target [, yearly interest %]'  e.g. '500, 200, 5000, 4.5'
    Output: a friendly text answer (or a friendly error message).
    """
    text = str(text)
    if re.search(r"-\s*\$?\d", text):
        return "Sorry, I couldn't work that out: numbers can't be negative."
    # '$1,000' keeps its thousands comma; if that leaves too few numbers, treat commas as separators ('100,100,50')
    values = []
    for pattern in (r"\d{1,3}(?:,\d{3})+(?![\d])(?:\.\d+)?|\d+(?:\.\d+)?|\.\d+", r"\d+(?:\.\d+)?|\.\d+"):
        values = [float(n.replace(",", "")) for n in re.findall(pattern, text)]
        if len(values) >= 3:
            break
    if len(values) < 3:
        return ("I need three numbers: current savings, how much you save each month, and your target. "
                "For example: 500, 200, 5000  (you can add a yearly interest rate as a 4th number, like 4.5).")
    try:
        return _format_goal(calculate_savings_goal(values[0], values[1], values[2],
                                                   values[3] if len(values) > 3 else 0.0))
    except ValueError as problem:
        return f"Sorry, I couldn't work that out: {problem}"


def create_savings_calculator_tool():
    """
    Create a custom savings goal calculator as an agent tool

    🤖 AI Collaboration Prompt:
    "Create a savings goal calculator function that takes current savings,
    monthly contribution, and target amount, then calculates time to reach
    goal. Format output for user-friendly display."

    Returns:
        function: the calculator (takes one text, returns one text), already registered as an agent tool.
    """
    agent.register_tool(
        "savings_goal_calculator",
        "Works out how long it takes to reach a savings goal. Input: 'current savings, monthly saving, "
        "target' as numbers, optionally followed by a yearly interest rate in percent. "
        "Example: '500, 200, 5000, 4.5'.",
        savings_goal_calculator,
    )
    return savings_goal_calculator


# --- Register it and try it (works without any AI server) ------------------------------------------------
savings_tool = create_savings_calculator_tool()
print("Tool registered: savings_goal_calculator\n")
print(savings_tool("500, 200, 5000"))
print()
print(savings_tool("current $1,000 monthly $250 target $10,000 rate 4.5"))
print()
print(savings_tool("abc"))

**Reflection**: Again AI was able to do this task perfectly and no manual changes were applied. 

## AI Collaboration # 15 
**Context**: Using AI to help build Gradio UI Integration for the finance assistant, following the instructions from the starter notebook and prompt. 
**Prompt**: Help me design a Gradio interface that combines CSV upload, spending analysis, chat functionality, and custom tools in a user-friendly layout suitable for a personal finance application.
**Result**: import re

import gradio as gr

# This cell uses the functions from your earlier cells. Run those cells first (in order).
_NEEDED = ["load_and_clean_transaction_data", "analyze_spending_patterns", "generate_financial_recommendations",
           "setup_financial_rag", "savings_goal_calculator", "penny_reply"]
_missing = [name for name in _NEEDED if name not in globals()]
if _missing:
    print("Run these earlier cells first. Still missing:", ", ".join(_missing))

SAMPLE_CSV = "sample_transactions.csv"


# --- Handlers: plain functions, so you can also test them without the UI ------------------------------
def analyse_file(uploaded_file):
    """Load a CSV (the upload, or the sample file if nothing was uploaded) and return report, advice, table."""
    global df, analysis, rag_search
    path = getattr(uploaded_file, "name", uploaded_file) or SAMPLE_CSV     # works with any Gradio version
    try:
        df = load_and_clean_transaction_data(path, verbose=False)
        analysis = analyze_spending_patterns(df)
        rag_search = setup_financial_rag()                                 # re-index with the new transactions
        status = f"Loaded {len(df)} transactions from {path}."
        return status, analysis["report"], generate_financial_recommendations(analysis), analysis["by_category"]
    except Exception as problem:                                           # show a friendly message, never crash
        return f"Sorry, I couldn't analyse that file: {problem}", "", "", None


def goal_tool(current, monthly, target, rate):
    """Run the savings goal calculator tool from the form fields."""
    try:
        text = f"{current or 0}, {monthly or 0}, {target or 0}, {rate or 0}"
        return savings_goal_calculator(text)
    except Exception as problem:
        return f"Sorry, something went wrong: {problem}"


def finance_chat(message, history):
    """Chat router: savings maths -> calculator tool; otherwise Penny, helped by the RAG guides."""
    try:
        if not str(message).strip():
            return "Ask me anything about budgeting, saving or your spending."
        numbers = re.findall(r"\d[\d,]*\.?\d*", str(message))
        if len(numbers) >= 3 and re.search(r"sav|goal|target|reach|how long", str(message), re.I):
            return savings_goal_calculator(message)
        guides = globals().get("rag_search")
        found = guides(message, 3) if guides else []
        context = "\n".join(f"- {chunk} [{source}]" for chunk, source in found)
        if globals().get("GEMINI_MODEL"):
            prompt = message if not context else f"{message}\n\nUseful background (cite the source name):\n{context}"
            reply = penny_reply(prompt, history)
            if not reply.startswith(("Sorry", "Penny isn't")):
                return reply
        return guides.answer(message) if guides else "Sorry, my guides aren't loaded yet. Run the RAG cell first."
    except Exception as problem:
        return f"Sorry, something went wrong: {problem}"


# --- The interface ---------------------------------------------------------------------------------------------------
def create_finance_assistant_ui():
    """
    Create a comprehensive Gradio interface for the Smart Finance Assistant

    🤖 AI Collaboration Prompt:
    "Help me design a Gradio interface that combines CSV upload, spending
    analysis, chat functionality, and custom tools in a user-friendly
    layout suitable for a personal finance application."

    Returns:
        gr.Blocks: call .launch() on it to start the app.
    """
    with gr.Blocks(title="Smart Finance Assistant: Savings Coach") as demo:
        gr.Markdown("# 💰 Smart Finance Assistant: Savings Coach\n"
                    "Upload your transactions, chat with Penny and plan your savings goals. "
                    "General information only, not licensed financial advice.")

        with gr.Tab("📊 My Spending"):
            gr.Markdown("Upload a CSV with Date, Amount and Description columns (Category is optional), "
                        "or leave it empty and press the button to use the sample data.")
            upload = gr.File(label="Transactions CSV", file_types=[".csv"])
            analyse_button = gr.Button("Analyse my spending", variant="primary")
            status = gr.Markdown()
            with gr.Row():
                report = gr.Textbox(label="Spending analysis", lines=22)
                advice = gr.Textbox(label="Recommendations", lines=22)
            table = gr.Dataframe(label="Spending by category")
            analyse_button.click(analyse_file, inputs=upload, outputs=[status, report, advice, table])

        with gr.Tab("💬 Chat with Penny"):
            gr.ChatInterface(
                finance_chat,
                examples=["How big should my emergency fund be?", "What is the 50/30/20 rule?",
                          "How can I spend less on coffee and takeaway?",
                          "I have 500 saved, save 200 a month, goal 5000. How long to reach it?"])

        with gr.Tab("🎯 Savings Goal Calculator"):
            gr.Markdown("Work out how long it takes to reach a savings goal.")
            with gr.Row():
                current = gr.Number(label="Current savings ($)", value=500, minimum=0)
                monthly = gr.Number(label="Saved each month ($)", value=200, minimum=0)
                target = gr.Number(label="Target ($)", value=5000, minimum=0)
                rate = gr.Number(label="Yearly interest (%), optional", value=0, minimum=0)
            calculate = gr.Button("Calculate", variant="primary")
            goal_result = gr.Textbox(label="Result", lines=8)
            calculate.click(goal_tool, inputs=[current, monthly, target, rate], outputs=goal_result)

    return demo


demo = create_finance_assistant_ui()
demo.launch()

**Reflection**: Just had to change the last part doing the share=false, debug=true and that fixed it however AI again proved quick and good for this task. 

## AI Collaboration # 16 
**Context**: Using AI to help test the finance tracker I built and the normal function tests following instructions from the starter notebook and prompts. 
**Prompts**: "Create tests that verify business insights are appropriate:
    - High spending categories are identified correctly
    - Savings opportunities are realistic
    - Recommendations match spending patterns
    - Output format is user-friendly"
"Create tests for spending analysis that verify:
    - Category totals are calculated correctly
    - Percentages add up to 100%
    - Refunds are handled appropriately
    - Edge cases like single transactions or empty categories
Use assert statements with known expected results."
"Create assert statements to test my data loading function with:
    - Valid CSV data
    - CSV with dollar signs in amounts
    - Missing values and invalid data
    - Empty files and corrupted data
Verify that cleaning works correctly and errors are handled gracefully."

**Results**: import os
import tempfile

import pandas as pd

# Tests for load_and_clean_transaction_data (Step 6: Test with a Variety of Data).
# Each test writes a small CSV to a temporary folder, loads it, and checks the result with assert.


def test_data_loading():
    folder = tempfile.mkdtemp()

    def write(name, text, mode="w"):
        path = os.path.join(folder, name)
        with open(path, mode) as handle:
            handle.write(text)
        return path

    def must_fail(path, expected_words):
        try:
            load_and_clean_transaction_data(path, verbose=False)
        except ValueError as problem:                       # a friendly message, not a crash
            assert str(problem) and any(word in str(problem).lower() for word in expected_words), str(problem)
        else:
            raise AssertionError(f"{path} should have raised a ValueError")

    # 1. Valid CSV data
    path = write("valid.csv", "Date,Amount,Category,Description\n2026-08-01,-10.50,Dining,Hudsons Coffee\n"
                              "2026-08-02,3000,Income,Salary\n")
    clean = load_and_clean_transaction_data(path, verbose=False)
    assert list(clean.columns) == ["Date", "Amount", "Category", "Description"] and len(clean) == 2
    assert clean["Amount"].tolist() == [-10.5, 3000.0]
    assert pd.api.types.is_datetime64_any_dtype(clean["Date"]) and pd.api.types.is_float_dtype(clean["Amount"])
    assert clean.attrs["cleaning_report"]["rows_out"] == 2
    print("OK 1: valid CSV")

    # 2. Dollar signs, commas, brackets and different date styles
    path = write("dollars.csv", 'Date,Amount,Description\n2026-08-01,"$1,234.50",Salary\n02/08/2026,($20.00),Kmart\n'
                                '2026-08-03,-$5.00,Coffee\n')
    clean = load_and_clean_transaction_data(path, verbose=False)
    assert clean["Amount"].tolist() == [1234.5, -20.0, -5.0]               # brackets mean negative
    assert clean["Date"].dt.day.tolist() == [1, 2, 3]                      # 02/08/2026 is 2 August (day first)
    assert (clean["Category"] == "Uncategorised").all()                    # no Category column: filled in
    print("OK 2: dollar signs and date formats")

    # 3. Missing values and invalid data: bad rows are dropped and counted
    path = write("messy.csv", "Date,Amount,Description\n2026-08-01,-10,A\n,-5,B\nnot a date,-6,C\n2026-08-03,,D\n"
                              "2026-08-04,xyz,E\n2026-08-05,-7,F\n2026-08-05,-7,F\n")
    clean = load_and_clean_transaction_data(path, verbose=False)
    report = clean.attrs["cleaning_report"]
    assert report["rows_in"] == 7 and report["rows_out"] == len(clean) == 2
    assert report["missing_or_invalid_date"] == 2 and report["missing_or_invalid_amount"] == 2
    assert report["duplicates"] == 1
    assert clean["Amount"].tolist() == [-10.0, -7.0]
    print("OK 3: missing and invalid data")

    # 4. Empty files and corrupted data give friendly errors
    must_fail(write("empty.csv", ""), ["empty"])
    must_fail(write("header_only.csv", "Date,Amount,Description\n"), ["no transactions"])
    must_fail(write("no_amount.csv", "Date,Description\n2026-08-01,Woolworths\n"), ["amount"])
    must_fail(write("all_bad.csv", "Date,Amount,Description\nx,y,z\n"), ["nothing to analyse", "usable"])
    must_fail(write("binary.csv", bytes([0, 255, 254, 1, 2, 3, 200, 201]), "wb"), ["csv", "couldn't"])
    must_fail(os.path.join(folder, "does_not_exist.csv"), ["couldn't find", "find"])
    must_fail(None, ["path", "file", "invalid"])
    print("OK 4: empty and corrupted files")

    # 5. Loading from a dictionary or table works too, and the original is not changed
    raw = {"Date": ["2026-08-01"], "Amount": ["$12.00"], "Category": ["Dining"], "Description": ["Zambrero"]}
    clean = load_and_clean_transaction_data(raw, verbose=False)
    assert clean["Amount"].tolist() == [12.0] and raw["Amount"] == ["$12.00"]
    print("OK 5: dictionary input")
    print("\nData loading tests passed.")


test_data_loading()

**Reflection**: AI was able to create the test functions for my finance tracker and all ran well and accordingly with little to no manual changes done. 

## AI Collaboration # 17 
**Context**: Using Ai to help build Integration tests to test my finance tracker, following instructions from the finance tracker and the following prompts. 
**Prompts**: "Create an end-to-end test that:
    1. Loads sample CSV data
    2. Runs complete analysis pipeline
    3. Generates chat responses about the data
    4. Verifies RAG system retrieval
    5. Tests custom tool functionality
    Ensure all components work together seamlessly."
"Create tests that verify error handling for:
    - Invalid file uploads
    - Network connection issues
    - Malformed data
    - User input validation
Ensure error messages are user-friendly and helpful."

**Result**: # End-to-end test: every part of the Smart Finance Assistant working together on the sample CSV.
# Run all the earlier cells first (loader, analysis, recommendations, chatbot, RAG, tool).


def test_end_to_end():
    global df, analysis, rag_search                      # the chat and RAG read these notebook variables
    close = lambda a, b, tol=0.01: abs(a - b) <= tol

    # 1. Load the sample CSV
    data = load_and_clean_transaction_data("sample_transactions.csv", verbose=False)
    df = data
    assert len(data) > 300 and list(data.columns) == ["Date", "Amount", "Category", "Description"]
    print(f"OK 1: loaded {len(data)} transactions")

    # 2. Complete analysis pipeline: analyse, then recommend
    result = analyze_spending_patterns(data)
    assert close(result["summary"]["income"], 37938.70) and close(result["summary"]["net_spending"], 36156.03)
    assert result["summary"]["savings_rate_pct"] == 4.7
    assert [t["category"] for t in result["top_categories"]] == ["Housing", "Groceries", "Dining"]
    advice = generate_financial_recommendations(result)
    assert "Savings rate: 4.7%" in advice and "YOUR ACTION PLAN" in advice
    print("OK 2: analysis and recommendations")

    # 3. Chat responses about the data (Penny if connected, otherwise the guides: both must give a real answer)
    analysis = result
    rag_search = setup_financial_rag()                  # the chat uses the guides + your transaction summaries
    question = "How can I save more each month?"
    if "finance_chat" in globals():
        reply = finance_chat(question, [])
    else:
        reply = penny_reply(question)
    assert isinstance(reply, str) and len(reply) > 40
    print("OK 3: chat answered:", reply[:70].replace("\n", " "), "...")
    if "penny_reply" in globals() and globals().get("GEMINI_MODEL"):
        direct = penny_reply("In one sentence, what is my savings rate?")
        print("   Penny says:", direct[:100].replace("\n", " "))

    # 4. RAG retrieval
    guides = rag_search
    found = guides("how much should I keep in an emergency fund")
    assert found and found[0][1] == "Savings guide: emergency fund"
    assert any(source.startswith("Transaction summary") for source in guides.sources)   # your own data is searchable too
    assert "50%" in guides("explain the 50/30/20 rule")[0][0]
    print("OK 4: RAG retrieval")

    # 5. Custom tool
    answer = savings_goal_calculator("500, 200, 5000")
    assert "23 months" in answer and "SAVINGS GOAL: $5,000.00" in answer
    print("OK 5: savings tool")

    # 6. The parts work together: your real monthly saving feeds the calculator
    monthly_saving = result["summary"]["net_saved"] / result["summary"]["months_covered"]
    assert monthly_saving > 0
    plan = savings_goal_calculator(f"0, {monthly_saving:.2f}, 5000")
    assert "SAVINGS GOAL" in plan and "Time to goal" in plan
    print(f"OK 6: at your real saving of ${monthly_saving:,.0f} a month: {plan.splitlines()[3].strip()}")
    print("\nEnd-to-end test passed.")


test_end_to_end()

**Reflection**: AI was able to build the Integration tests again with little to no manual changes required, AI was great in this task and definitely saved a lot of time. 



