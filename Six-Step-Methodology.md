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

# ISO first (2026-08-01), then Australian day-first formats (01/08/2026).
# Each format is tried explicitly because pandas' dayfirst=True misreads ISO dates.
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

6. Test with a Verity of Data - 
