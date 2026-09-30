RETAIL LOAN UNDERWRITING PROJECT (EXCEL)
=====================================================================
 
A simple Excel project that screens 120 loan applications against a
lending policy and shows the result on a dashboard. It also has an EMI
calculator with a full amortisation schedule.
 
Built as a learning project for a banking / credit analyst role.
 
IMPORTANT NOTE
--------------
- All applicant data (names, cities, income, credit score, etc.) is
  SYNTHETIC and randomly generated. It is not real customer data.
- The lending policy (interest rates, FOIR limits, score cut-offs) is
  my own illustrative assumption. It is NOT the actual rate card or
  credit policy of ICICI Bank.
- This project is not affiliated with or endorsed by ICICI Bank.
 
 
---------------------------------------------------------------------
1. WHAT THIS PROJECT DOES
---------------------------------------------------------------------
For every loan application, the workbook:
  1. Assigns a credit score band (Poor to Excellent)
  2. Calculates the interest rate = product base rate + score premium
  3. Calculates the new EMI and the FOIR
  4. Calculates the maximum loan amount the customer is eligible for
  5. Gives a final decision: Approve / Refer to Manager / Reject
     (with the reason for rejection)
 
All decisions are formula driven. If you change a value on the Policy
sheet, every decision, table and chart updates automatically.
 
 
---------------------------------------------------------------------
2. FILE STRUCTURE
---------------------------------------------------------------------
ICICI_Loan_Underwriting_Project.xlsx   (main file)
README.txt                             (this file)
 
Sheets inside the Excel file:
 
  Dashboard       KPI cards, 4 charts and an auto-updating "quick read"
  Data            120 applications. Columns A-J are input data, columns
                  K-P are formulas (score band, rate, EMI, FOIR,
                  max eligible amount, decision)
  Policy          All assumptions in one place (base rates, max tenure,
                  max FOIR, min credit score, score band premiums,
                  max age at maturity, refer buffer)
  Summary         Product-wise, decision-wise, score-band-wise and
                  city-wise tables using COUNTIFS / SUMIFS / AVERAGEIFS
  EMI_Calculator  EMI, total interest, yearly view and month-by-month
                  amortisation schedule (up to 30 years) with a chart
 
 
---------------------------------------------------------------------
3. LENDING POLICY USED (ASSUMPTIONS)
---------------------------------------------------------------------
Product         Base Rate   Max Tenure   Max FOIR   Min Credit Score
Home Loan       8.75%       30 yrs       50%        700
Auto Loan       9.25%       7 yrs        50%        690
Personal Loan   11.50%      5 yrs        45%        720
Education Loan  9.50%       15 yrs       55%        650
Business Loan   12.00%      7 yrs        50%        700
 
Score band premium added to the base rate:
  0   - 649   Poor        +2.50%
  650 - 699   Fair        +1.50%
  700 - 749   Good        +0.75%
  750 - 799   Very Good   +0.25%
  800+        Excellent   +0.00%
 
Other rules:
  - Max age at loan maturity = 65 years (age + tenure must be <= 65)
  - "Refer to Manager" buffer = 5% above the max FOIR of the product
 
 
---------------------------------------------------------------------
4. DECISION LOGIC (IN ORDER)
---------------------------------------------------------------------
  1. Credit score below product minimum      -> Reject - Low Score
  2. Age + tenure greater than 65            -> Reject - Age
  3. Tenure more than product maximum        -> Reject - Tenure
  4. FOIR <= product max FOIR                -> Approve
  5. FOIR within 5% above the max FOIR       -> Refer to Manager
  6. FOIR higher than that                   -> Reject - High FOIR
 
  FOIR = (New EMI + Existing EMIs) / Monthly Income
  EMI  = PMT(rate/12, tenure*12, -loan amount)
 
 
---------------------------------------------------------------------
5. KEY RESULTS (FROM THE SAMPLE DATA)
---------------------------------------------------------------------
  Total applications        : 120
  Total amount requested    : Rs 14.79 crore
  Approved amount           : Rs 9.34 crore
  Overall approval rate     : 66.7%  (80 approved)
  Referred to manager       : 5
  Rejected                  : 35
  Average interest rate     : 10.6%
  Average FOIR              : 29.6%
 
  Decision breakdown:
    Approve               80
    Refer to Manager       5
    Reject - Low Score    20
    Reject - High FOIR    10
    Reject - Age           5
    Reject - Tenure        0
 
  Approval rate by product:
    Education Loan   100%
    Auto Loan        92.6%
    Personal Loan    63.0%
    Home Loan        50.0%
    Business Loan    40.0%
 
  Observations:
    - Low credit score is the most common reason for rejection.
    - Business loans have the lowest approval rate (highest FOIR).
    - Risk based pricing works as expected: average rate is 11.3% for
      Poor scores vs 9.8% for Excellent scores.
 
 
---------------------------------------------------------------------
6. HOW TO USE
---------------------------------------------------------------------
  1. Download ICICI_Loan_Underwriting_Project.xlsx and open it in
     Microsoft Excel (formulas also work in Google Sheets / LibreOffice).
  2. Go to the Dashboard sheet to see the overall picture.
  3. To test a different policy, change the blue input cells on the
     Policy sheet (for example, reduce Max FOIR of Home Loan to 40%).
     All decisions, tables and charts will update.
  4. To try your own applicant, edit or add a row in columns A-J of the
     Data sheet (copy the formulas in K-P down for new rows).
  5. Use the EMI_Calculator sheet: pick a product from the drop-down,
     fill loan amount, tenure and credit score in the yellow cells.
 
 
---------------------------------------------------------------------
7. EXCEL FUNCTIONS AND SKILLS USED
---------------------------------------------------------------------
  - INDEX + MATCH (exact and approximate match) for policy lookups
  - Nested IF for the decision engine
  - PMT and PV for EMI and loan eligibility
  - COUNTIF / COUNTIFS / SUMIF / SUMIFS / AVERAGEIF for summary tables
  - Dynamic text formulas for the auto-updating insights
  - Charts: bar, pie and stacked bar
  - Conditional formatting and data validation (drop-down, limits)
  - Banking concepts: EMI, FOIR, risk based pricing, credit score
    bands, loan eligibility, amortisation
 
 
---------------------------------------------------------------------
8. LIMITATIONS
---------------------------------------------------------------------
  - Data is synthetic, so results are only for demonstration.
  - A real credit policy also checks employment type, bureau history
    (DPD, enquiries), collateral / LTV, KYC and income documents.
  - Interest rates are fixed assumptions, not market linked.
 
