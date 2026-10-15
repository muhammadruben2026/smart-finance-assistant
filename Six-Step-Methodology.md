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
