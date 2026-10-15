## Six-Step Development Methodology ## 
**1. Sample Transaction Data Setup** 
1. Understand the Problem - Using AI to help create realistic sample transaction data , include Australia business and various spending categories, sample data for structuring and create dataframe from sample data. 

2. Inputs - Asking AI specific prompts to get the answer I need , the prompt will be "Hi Claude could you create realistic sample transaction data that includes Australia businesses and various spending categories." This will be my first prompt.
Outputs - AI will generate sample transaction data that I can use in my starter notebook generated along with Australian businesses and various spending categories.

3. Work the Problem by hand - Sampling the data for structuring will include writing the date, amount, category, description e.g. 2026-08-01, $45.50, Groceries, Woolworths Canning Vale.
Creating the dataframe from sample data can simply be done by the code:
df_sample = pd.DataFrame(sample_transactions)
print("📋 Sample transaction data created:")
print(df_sample)  

4. Write Pseudo Code -
For each sample transaction to be created, generate a random transaction amount, generate a random transaction date, select a transaction category, create a transaction description. Store the transaction details in a samples transactions lists. Display the sampled transactions. 
    
5. Convert to Python - ample_transactions = {
    'Date':        ['2026-08-01', '2026-08-02', '2026-08-03', '2026-08-04', '2026-08-05',
                    '2026-08-06', '2026-08-07', '2026-08-08'],
    'Amount':      ['$45.50', '$12.00', '$89.95', '$3.50', '-$25.00', '$1,250.00', '$68.40', '$7.20'],
    'Category':    ['Groceries', 'Transport', 'Entertainment', 'Coffee', 'Refund',
                    'Rent', 'Utilities', 'Dining'],
    'Description': ['Woolworths Canning Vale', 'Transperth SmartRider', 'Ticketek Concert',
                    'Campus Cafe Curtin', 'Kmart Returned Item', 'Ray White Rent',
                    'Synergy Electricity', 'Boost Juice Garden City'],
}

6. Test with a variety of data - All tests passed
📋 Sample transaction data created:
         Date     Amount       Category              Description
0  2026-08-01     $45.50      Groceries  Woolworths Canning Vale
1  2026-08-02     $12.00      Transport    Transperth SmartRider
2  2026-08-03     $89.95  Entertainment         Ticketek Concert
3  2026-08-04      $3.50         Coffee       Campus Cafe Curtin
4  2026-08-05    -$25.00         Refund      Kmart Returned Item
5  2026-08-06  $1,250.00           Rent           Ray White Rent
6  2026-08-07     $68.40      Utilities      Synergy Electricity
7  2026-08-08      $7.20         Dining  Boost Juice Garden City

**2. Data Loading and Cleaning Function** 
1. Understand the Problem - Creating a function to load the CSV data with date, amount , category, description. Ensuring that the data is clean and up to par for my finance assistant. Making sure there are business focused error messages if anything goes wrong. Doing this with assistance from AI. 

2. Inputs - CSV, Data, Date, amount, description
Outputs - Clean transaction list that has everything stated, clear business focused error messgaes if anything does end up in an error.

3.Work the Problem by hand - Making sure dollar signs are inputted and not missing, making sure values aren't missing so that the data can be interpreted, making sure the date, amount, category and description are in the CSV list as if theses are missing the Finance tracker won't work correctly. 

4. Write Pseudo Code - The CSV transaction list should look something like this, Date: 08-08-2026, Amount: $42.50, Category: Entertainment, Description: Movie Night. Each transaction should have each of these values filled out for my finance tracker.

5. Convert to Python - import re
from datetime import date, datetime

import pandas as pd

ISO first (2026-08-01), then Australian day-first formats (01/08/2026).
Each format is tried explicitly because pandas' dayfirst=True misreads ISO dates.
_DATE_FORMATS = ("%Y-%m-%d", "%d/%m/%Y", "%d-%m-%Y", "%d/%m/%y", "%Y/%m/%d")

_COLUMN_ALIASES = {
    "date":        ["date", "transaction date", "posted", "posting date"],
    "amount":      ["amount", "value", "total", "amount (aud)"],
    "description": ["description", "details", "merchant", "memo", "narrative", "transaction description"],
    "category":    ["category", "type"],
}


def _parse_amount(value):
    """'$1,203.50' -> 1203.5 | '-$25.00' or '(25.00)' -> -25.0 | unusable -> None."""
    if value is None or (isinstance(value, float) and value != value):    # None or NaN
        return None
    if isinstance(value, (int, float)):
        return float(value)
    text = str(value).strip()
    digits = re.sub(r"[^0-9.]", "", text)                  # drop $, commas, spaces and letters
    if digits in ("", "."):
        return None
    try:
        number = float(digits)
    except ValueError:                                     # e.g. '1.2.3'
        return None
    return -number if ("-" in text or "(" in text) else number


def _parse_date(value):
    """Return a Timestamp, or NaT when the date is missing or in an unknown format."""
    if isinstance(value, (pd.Timestamp, datetime, date)):
        return pd.Timestamp(value)
    text = str(value).strip()
    for fmt in _DATE_FORMATS:
        try:
            return pd.Timestamp(datetime.strptime(text, fmt))
        except ValueError:
            continue
    return pd.NaT


def _clean_text(value, default=""):
    """Trim and collapse whitespace; blank or missing values become `default`."""
    if value is None or (isinstance(value, float) and value != value):
        return default
    return " ".join(str(value).split()) or default


def load_and_clean_transaction_data(file_path, verbose=True):
    """
    Load and clean transaction data for the Smart Finance Assistant

    🤖 AI Collaboration Prompt:
    "Create a function to load CSV transaction data with Date, Amount, Category,
    Description columns. Handle dollar signs in Amount, missing values, and
    data validation. Include clear business-focused error messages."

    Args:
        file_path: Path to CSV file or file object (a DataFrame or dict also works, handy for tests)
        verbose:   Print a one-line summary of what was loaded and removed

    Returns:
        pandas.DataFrame with columns Date (datetime), Amount (float), Category, Description.
        Amount keeps the sign used in the file (nothing is flipped).
        What was removed is stored in df.attrs["cleaning_report"].

    Raises:
        ValueError: with a plain-English explanation of what is wrong and how to fix it.
    """
    # --- 1. Load the file ---------------------------------------------------------
    try:
        if isinstance(file_path, pd.DataFrame):
            raw = file_path.copy()
        elif isinstance(file_path, dict):
            raw = pd.DataFrame(file_path)
        else:
            # Read everything as text so we control how $ signs and blanks are handled
            raw = pd.read_csv(file_path, dtype=str, keep_default_na=False)
    except FileNotFoundError:
        raise ValueError(f"We couldn't find '{file_path}'. Check the file name and that it has been "
                         "uploaded to Colab (folder icon on the left).") from None
    except pd.errors.EmptyDataError:
        raise ValueError("The file is empty. Please export your transactions again.") from None
    except (pd.errors.ParserError, UnicodeDecodeError) as err:
        raise ValueError("The file couldn't be read as a CSV. Open it in a spreadsheet and "
                         f"re-save it as 'CSV (comma delimited)'. Details: {err}") from err
    if raw.empty:
        raise ValueError("The file has column headings but no transactions.")

    # --- 2. Check the columns (names are case and spacing insensitive) -------------------
    raw.columns = [str(c).strip().lower() for c in raw.columns]
    for standard, options in _COLUMN_ALIASES.items():
        if standard not in raw.columns:
            match = next((c for c in raw.columns if c in options), None)
            if match is not None:
                raw = raw.rename(columns={match: standard})
    for column in ("date", "amount"):
        if column not in raw.columns:
            raise ValueError(f"Your file has no '{column.title()}' column, so we can't analyse it. "
                             f"Columns found: {list(raw.columns)}. Please include Date and Amount "
                             "(Description and Category are optional).")
    notes = []
    for column, default_note in (("description", "no Description column: rows are labelled '(no description)'"),
                                 ("category", "no Category column: rows are labelled 'Uncategorised'")):
        if column not in raw.columns:
            raw[column] = ""
            notes.append(default_note)

    # --- 3. Clean: dates, amounts, text -----------------------------------------------
    report = {"rows_in": len(raw)}
    df = raw[["date", "amount", "category", "description"]].copy()

    df["date"] = df["date"].map(_parse_date)
    usable = df["date"].notna()
    report["missing_or_invalid_date"] = int((~usable).sum())
    df = df[usable].copy()

    df["amount"] = df["amount"].map(_parse_amount)
    usable = df["amount"].notna()
    report["missing_or_invalid_amount"] = int((~usable).sum())
    df = df[usable].copy()

    if df.empty:
        raise ValueError(f"None of the {report['rows_in']} rows had both a usable date and amount, so "
                         "there is nothing to analyse. Common causes: dates not written like 2026-08-01 "
                         "or 01/08/2026, or amounts that contain text.")

    df["date"] = pd.to_datetime(df["date"])
    df["description"] = df["description"].map(lambda v: _clean_text(v, "(no description)"))
    df["category"] = df["category"].map(lambda v: _clean_text(v, "Uncategorised").title())

    # --- 4. Validate: remove exact duplicates (same date, merchant and amount) -------------
    before = len(df)
    df = df.drop_duplicates(subset=["date", "description", "amount"])
    report["duplicates"] = before - len(df)

    # --- 5. Tidy the result --------------------------------------------------------------
    df = df.rename(columns=str.title)[["Date", "Amount", "Category", "Description"]]
    df = df.sort_values("Date", kind="stable").reset_index(drop=True)
    report["rows_out"] = len(df)
    df.attrs["cleaning_report"] = report

    if verbose:
        print(f"✅ Loaded {report['rows_out']} of {report['rows_in']} transactions "
              f"({df['Date'].min():%d %b %Y} to {df['Date'].max():%d %b %Y}).")
        removed = [f"{report[key]} {label}" for key, label in (
            ("missing_or_invalid_date", "with a missing/invalid date"),
            ("missing_or_invalid_amount", "with a missing/invalid amount"),
            ("duplicates", "duplicates")) if report[key]]
        if removed:
            print("⚠️ Removed: " + ", ".join(removed) + ".")
        for note in notes:
            print(f"ℹ️ {note}")
    return df

6. Test with a Verity of Data - ✅ Loaded 364 of 364 transactions (01 Apr 2026 to 30 Sep 2026).
ℹ️ no Category column: rows are labelled 'Uncategorised'
{'rows_in': 364, 'missing_or_invalid_date': 0, 'missing_or_invalid_amount': 0, 'duplicates': 0, 'rows_out': 364}
Test Passed and data is cleaned out.

**3. Comprehensive Spending Analysis** 
1. Understand the problem - Creating a function that can analyse spending by category, calculates percentages, identifies trends such as top spending areas, generates insights formatted for future business presentations.

2. Inputs - CSV data, transactions lists
Outputs - Trends, insights, data ready for business presentation or can easily be interpreted.

3. Work the Problem by hand - Finance tracker should be able to produce results such as giving insights and outputting information thats can be easily read and transferred for a business presentation, for example the Finance Tracker should give recommendations and identify trends in someones spending, for example if Housing is taking up 80% of someones spending.

4. Pseudo Code - Code should output an analysis report. e.g.print (anaysis["report"])

5. Convert to Python - import re

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

6. Test with a verity of Data -
OK 1: sample CSV
OK 2: messy data
OK 3: purchases-positive data
OK 4: unusual data
OK 5: error messages

All tests passed.

**4. Professional Financial Recommendations** 
1. Understand the problem - Generating professional financial recommendations based on spending analysis, observing patterns, trends and generating actionable advice formatted for a financial assistant user.

2. Inputs - Spending Analysis Data, CSV 
Outputs - Actionable advice, spending patterns/trends

3. Work the Problem by hand - Snapshot or summary of the users spending habits, action plan - what type of actions the user should be doing to help save some extra money.

4. Write Pseudo Code - Needs: "Housing", "Utilities", "Insurance", "Groceries", "Transport", "Health".
Wants: "Dining", "Entertainment", "Shopping", "Travel", "Cash"

5. Convert to Python - # Business rules - edit these to tune the advice
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

6. Test with a Variety of Data - All Tests Passed.


**5. Financial Advice Chatbot**
1. Understand the Problem - Creating a friendly and professional chatbot that can provide advice based on spending transaction analysis.

2. Inputs - Gemini AI Key, CSV data, users spending patterns/trends 
Outputs - A chatbot that is able to assist and provide advice based on the users spending habits.

3. Work the Problem by hand - if the user has bad spending habits that exceeds their income the chatbot can provide advice on what categories to cut spending on. If the user has good spending habits the AI can motivate them to keep going and motivate the user to reach their savings goal.

4. Write Pseudocode - If the user has bad spending habits messages the chatbot could use are, "Your spending is putting you at danger, cutting down on xxx will save you this $xxx".
If the user has good spending habits messages the chatbot could use are, "Your spending habits are great and are getting you closer to your savings goal of $xxx, keep going!".

5. Convert to Python - import os

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

6. Test with a Variety of Data - All Tests Passed.

**6. RAG System** 
1. Understand the Problem - Setting up a RAG system that can retrieve data from financial documents, budgeting guides, and transaction summaries.

2. Inputs - Financial documents, budgeting guides, transaction summaries
Outputs - Answer the users questions about their finances, summaries from documents that are too long to read.

3. Work the Problem by hand - Implementing a system that can generate important points from documents that may benefit the user in their spending and budgeting.

4. Write Pseudocode - Budgeting Guide 50/30/20, essentially the finance assistant producing guides/tips that benefit the user and inform them on what to do in their future spending, and ways to save.

5. Convert to Python - import math
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

6. Test with a Variety of Data - All Tests Passed.

**7. Custom Tool Development**
1. Understand the Problem - Creating financial tools that would benefit the user and make their budgeting/spend journey easier and making sure the format is user-friendly.

2. Inputs - Values inputted by the user, CSV data list, Spending habits/trends
Outputs - Values ready and calculated for the user, amounts the user needs to reach their goal essentially.

3. Work the Problem by hand - Building a financial calculator that can help solve users problems and also this calculator can help find what amounts users may need to save to reach their future goals.

4. Write Pseudocode - something similar to this ef calculate_savings_goal(current, monthly, target, annual_rate), to help calculate users needs and find what amounts they need in order to reach their goal.

5. Convert to Python - import math
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

6. Test with a Variety of Data - All Tests Passed.


**
