## Six-Step Development Methodology ## 
** 1. Sample Transaction Data Setup ** 
1. Using AI to help create realistic sample transaction data , include Australia business and various spending categories, sample data for structuring and create dataframe from sample data. 

2. Inputs - Asking AI specific prompts to get the answer I need , the prompt will be "Hi Claude could you create realistic sample transaction data that includes Australia businesses and various spending categories." This will be my first prompt.
Outputs - AI will generate sample transaction data that I can use in my starter notebook generated along with Australian businesses and various spending categories.

3. Work the Problem by hand - Sampling the data for structuring will include writing the date, amount, category, description e.g. 2026-08-01, $45.50, Groceries, Woolworths Canning Vale.
Creating the dataframe from sample data can simply be done by the code:
df_sample = pd.DataFrame(sample_transactions)
print("📋 Sample transaction data created:")
print(df_sample)  

5. Write Pseudo Code -
For each sample transaction to be created, generate a random transaction amount, generate a random transaction date, select a transaction category, create a transaction description. Store the transaction details in a samples transactions lists. Display the sampled transactions. 
    
6. Convert to Python - ample_transactions = {
    'Date':        ['2026-08-01', '2026-08-02', '2026-08-03', '2026-08-04', '2026-08-05',
                    '2026-08-06', '2026-08-07', '2026-08-08'],
    'Amount':      ['$45.50', '$12.00', '$89.95', '$3.50', '-$25.00', '$1,250.00', '$68.40', '$7.20'],
    'Category':    ['Groceries', 'Transport', 'Entertainment', 'Coffee', 'Refund',
                    'Rent', 'Utilities', 'Dining'],
    'Description': ['Woolworths Canning Vale', 'Transperth SmartRider', 'Ticketek Concert',
                    'Campus Cafe Curtin', 'Kmart Returned Item', 'Ray White Rent',
                    'Synergy Electricity', 'Boost Juice Garden City'],
}

7. Test with a variety of data - All tests passed
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
