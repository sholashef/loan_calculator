def calculate_loan_amortization(loan_amount, interest_rate, loan_tenure):
    # Convert interest rate to monthly interest rate
    monthly_interest_rate = interest_rate / 12 / 100
    
    # Calculate monthly installment (EMI)
    monthly_installment = loan_amount * (monthly_interest_rate * (1 + monthly_interest_rate) ** loan_tenure) / ((1 + monthly_interest_rate) ** loan_tenure - 1)
    
    # Initialize variables for the table
    outstanding_balance = loan_amount
    table = []
    
    for month in range(1, loan_tenure + 1):
        # Calculate interest for the current month
        interest_payment = outstanding_balance * monthly_interest_rate
        
        # Calculate principal payment for the current month
        principal_payment = monthly_installment - interest_payment
        
        # Update outstanding balance
        outstanding_balance -= principal_payment
        
        # Append the data to the table
        table.append((month, monthly_installment, principal_payment, interest_payment, outstanding_balance))
    
    return table

def display_amortization_table(table):
    # Display table header
    print("{:<5} {:<15} {:<15} {:<15} {:<15}".format("Month", "EMI", "Principal Payment", "Interest Payment", "Outstanding Balance"))
    
    for row in table:
        # Display each row of the table
        month, emi, principal, interest, balance = row
        print("{:<5} {:<15.2f} {:<15.2f} {:<15.2f} {:<15.2f}".format(month, emi, principal, interest, balance))

# Input values
loan_amount = float(input("Enter the loan amount: "))
interest_rate = float(input("Enter the annual interest rate (%): "))
loan_tenure = int(input("Enter the loan tenure (in months): "))

# Calculate the loan amortization schedule
amortization_table = calculate_loan_amortization(loan_amount, interest_rate, loan_tenure)

# Display the amortization table
display_amortization_table(amortization_table)
