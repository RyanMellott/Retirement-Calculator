# Retirement-Calculator
import math

print("Welcome to the Retirement Calculator!")


# Input: Current age and goal retirement age
age = input("Enter your age: ")
retirement_age = input("Enter your goal retirement age: ")
#Input: Current investment and monthly investment
current_investment = input("Enter the amount you have saved for retirement: ")
monthly_investment = input("Enter the amount that you can save every month: ")
# Input: Annual rate of return (in percentage)
rate = float(input("Enter the annual rate of return - 4% is risk free, 8% is moderately risky, and 12% is risky (Don't put %): "))

# Determine if user knows there retirement goal
answer = input("Do you know how much money ou will need in retirement? (yes or no):")
if answer == "yes": investment_goal = input("Enter your retiremnt goal amount: ")
else: 
    yearly_amount = input("How much money will you need to live off of every year (in today's dollars)?")
    yearly_amount = float(yearly_amount)
    yearly_amount_inflation_adjusted = yearly_amount *1.03 ** (int(retirement_age) - int(age))
        
    investment_goal = yearly_amount_inflation_adjusted * 25
    print(f"Your investment goal is ${round(investment_goal, 2):,}. This is the amount of money you need to retire at {retirement_age}!")

# Used on line 65 as a fun fact
def time_to_double(rate_of_return):
    # Convert the rate of return to a decimal by dividing by 100
    rate_of_return_decimal = rate_of_return / 100
    
    # Calculate the time to double using the exact formula
    time = math.log(2) / math.log(1 + rate_of_return_decimal)
    return time

def retirement_calculator(age, retirement_age, current_investment, monthly_investment, investment_goal, rate):
    # Convert the inputs to integers
    age = int(age)
    retirement_age = int(retirement_age)
    current_investment = float(current_investment)
    monthly_investment = float(monthly_investment)
    investment_goal = float(investment_goal)

    # Calculate the number of years until retirement
    years_until_retirement = retirement_age - age

    # Calculate the future value of the investment
    for i in range(years_until_retirement):
        count = 0
        while count <12:
            current_investment = current_investment + monthly_investment
            current_investment *= 1+(rate/100/12)
            count += 1
    print(f"At your current rate of investing, your investment will be worth ${round(current_investment, 2):,} in {years_until_retirement} years.")
    if current_investment >= investment_goal:
        print("Congratultations! You will reach your retirement goal.")
    else: print("You will not reach your retirement goal. Try saving more!")

retirement_calculator(age, retirement_age, current_investment, monthly_investment, investment_goal, rate)

# Ask the user if they would like to see the assumptions or fun facts
answer_2 = print(input("If you would like to see the assumptions this calculator makes type 1, if you want some fun facts type 2"))    
if answer_2 == 1:
    print("This calculator assumes an inflation rate of 3% and a 4% withdrawal rate. It also assumes that you will live for 30 years after retirement.")
elif answer_2 == 2:
    time = time_to_double(rate)
    print(f"It will take approximately {time:.2f} years to double your investment at a {rate}% rate of return. This can be used to roughly know how much money you will have!")
    print("Also, did you know that the average retirement age in the US is 62 years old?")
else: print("Thanks for using the calculator!")










