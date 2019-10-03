
The recurssive function I wrote runs at a constant rate regardless of input size but is Big-Theta(n). The lack of iteration helps make the function constant.

The topic I chose to demonstrate was to design a recursive algorithm that calculated the number of months a ponzi scheme could function without breaking the bank. A brief explanation of a ponzi scheme is when someone makes promises of a low risk/high reward investment opportunity. Investments are not actually backed by anything but rather paid by future investor's investments. This can only work as long as there is a continuous flow of new investors. Generally, the sooner you fall victim to a ponzi scheme the better off you are. It is the investors at the tail end of a ponzi schemes life that usually lose the most.

In our scenario, our ponzi scheme operator is asking people to invest 1000 dollars promising an 8 percent return each month. However, with every new investor, recruitment grows increasingly difficult taking twice as long to get the next investor as it did the last. Assuming each investor has an initial investment of 1000 dollars and they were each promised an 8 percent return each month. How long would it take for the ponzi scheme to collapse given zero initial investors and zero available funds?


```python
def run_ponzi_scheme(investors=0, months_until_next_recruit=1, months_to_recruit=1, available_funds=0):
    current_month = months_to_recruit - (months_until_next_recruit-months_to_recruit)
    print(f'Month {current_month} started!')
    
    months_until_next_recruit -= 1
    new_investor = False
    
    if months_until_next_recruit == 0:
        new_investor = True
        
        initial_investment = 1000
        available_funds += initial_investment    
        print(f'Received investment: ${available_funds} (+${initial_investment})')
        
        months_to_recruit *= 2        
        months_until_next_recruit = months_to_recruit
    
    required_earnings_funds = investors * 80
    
    if required_earnings_funds > available_funds:
        busted = True
        
        print("Ponzi scheme busted!!!")
    else:
        busted = False
        available_funds -= required_earnings_funds
        
        print(f'Paid investor earnings: ${available_funds} (-${required_earnings_funds})')
    
    if new_investor and not busted:
        investors += 1
        
    if not busted:
        print(f'Month {current_month} complete! \n')
        run_ponzi_scheme(investors, months_until_next_recruit, months_to_recruit, available_funds)
    
    
run_ponzi_scheme()    
```

    Month 1 started!
    Received investment: $1000 (+$1000)
    Paid investor earnings: $1000 (-$0)
    Month 1 complete! 
    
    Month 2 started!
    Paid investor earnings: $920 (-$80)
    Month 2 complete! 
    
    Month 3 started!
    Received investment: $1920 (+$1000)
    Paid investor earnings: $1840 (-$80)
    Month 3 complete! 
    
    Month 4 started!
    Paid investor earnings: $1680 (-$160)
    Month 4 complete! 
    
    Month 5 started!
    Paid investor earnings: $1520 (-$160)
    Month 5 complete! 
    
    Month 6 started!
    Paid investor earnings: $1360 (-$160)
    Month 6 complete! 
    
    Month 7 started!
    Received investment: $2360 (+$1000)
    Paid investor earnings: $2200 (-$160)
    Month 7 complete! 
    
    Month 8 started!
    Paid investor earnings: $1960 (-$240)
    Month 8 complete! 
    
    Month 9 started!
    Paid investor earnings: $1720 (-$240)
    Month 9 complete! 
    
    Month 10 started!
    Paid investor earnings: $1480 (-$240)
    Month 10 complete! 
    
    Month 11 started!
    Paid investor earnings: $1240 (-$240)
    Month 11 complete! 
    
    Month 12 started!
    Paid investor earnings: $1000 (-$240)
    Month 12 complete! 
    
    Month 13 started!
    Paid investor earnings: $760 (-$240)
    Month 13 complete! 
    
    Month 14 started!
    Paid investor earnings: $520 (-$240)
    Month 14 complete! 
    
    Month 15 started!
    Received investment: $1520 (+$1000)
    Paid investor earnings: $1280 (-$240)
    Month 15 complete! 
    
    Month 16 started!
    Paid investor earnings: $960 (-$320)
    Month 16 complete! 
    
    Month 17 started!
    Paid investor earnings: $640 (-$320)
    Month 17 complete! 
    
    Month 18 started!
    Paid investor earnings: $320 (-$320)
    Month 18 complete! 
    
    Month 19 started!
    Paid investor earnings: $0 (-$320)
    Month 19 complete! 
    
    Month 20 started!
    Ponzi scheme busted!!!


You can see that in this specific example, it took 20 months before our ponzi scheme collapsed. At this point it took too long to find new recruits to make up for the losses being paid out to the scheme's previous investors.
