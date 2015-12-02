# Lifecastor Command Line

Usage: ruby lifecastor.rb [options] [plan property file of your choice]

    Options are explained below. They can be combined.

    To make a simplest run, type the following, then hit enter key.

        ruby lifecastor.rb

        This uses the default parameters from the included file plan.properites.
        Feel free to modify the parameters as you wish.

    To run on your own plan property file named 'my_plan_properties', type:

        ruby lifecastor.rb my_plan_properties

    To combine the above run with option -v, type:

        ruby lifecastor.rb -v my_plan_properties

**Options:**

    -b, --brief                      Output brief resutls of bankrupt info. Use -v to see more detaills.

    -c, --chart                      Chart the resutls as configured by your plan.propreties file.

    -d, --diff                       Show the difference between last and current results.

    -q, --quiet                      Output nothing to the standard output.

    -t, --taxed_savings              Tax savings at short term capital gain tax rates which are the same as regular income tax rates.

    -v, --verbose                    Output the complete resutls.

    -h, --help                       Show this message


# Features

This is an application for [*Personal Finance Life-long Forcaste*](http://tranquil-headland-5582.herokuapp.com/).

* Easy to modify input parameters in file plan.properties allow you to run endless what-if simulations so that you can understand your financial future. 

* See the big pictures of your financial future under dynamic probabilistic income, expense, and savings. 

* Analyze the impact of inflation, social security, and retirement age on your financial future. 

* Statistically forecast your estate and wealth. 

* Display you simulated wealth paths into the future.

Please send comments and suggestions to John at johnzhu00@gmail.com.

# Sample Plan Property File

```
# All parameters are grouped into two sets for the primary bread maker and his spouse. 
# Those of the spouse are suffixed by an underscore '_'.
#
age=40
age_to_retire=65
# discount factor after retirement for BOTH spouses: the expense after retirement is dropped to this percentage of the expense before retirement
expense_after_retirement = 0.8

# this models your senior year baseline annual health cost: your health cost will grow upwards non-linearly based on this base in such a way that it starts to grow upwards non-linearly at age 55, double at 70, triple at 80, six times at 90; set it to zero if you don't want to simulate senior year health cost by Lifecastor
health_cost_base = 1000.0
# this allows you to shift when senior year health cost starts to grow upwards non-linearly: 0 means that the cost starts to grow at age 55; -10 means 10 years sooner at age 45, 15 means 15 years later at age 70; if you are healthy, set it to positive value;
shift = 0

life_expectancy = 95
# discount factor for the surviving spouse after the primary is passed away: assuming that life_expectancy is the shorter than life_expectancy_ of the spouse
expense_after_life_expectancy = 0.7

# annual income
income=100000
# income growth mean annual rate and standard deviation: the yearly salary growth percentage is normally distributed with a mean and standard deviation (sd)
increase_mean=0.03
increase_sd  =0.005

##### spouse data #####
age_=38
age_to_retire_=62
# this models your senior year baseline annual health cost: your health cost will grow upwards non-linearly based on this base in such a way that it starts to grow upwards non-linearly at age 55, double at 70, triple at 80, six times at 90; set it to zero if you don't want to simulate senior year health cost by Lifecastor
health_cost_base_ = 1000.0
# this allows you to shift when senior year health cost starts to grow upwards non-linearly: 0 means that the cost starts to grow at age 55; -10 means 10 years sooner at age 45, 15 means 15 years later at age 70; if you are healthy, set it to positive value;
shift_ = 0

# this is supposed to be greater or equal to life_expectancy specified above and determines the length of the planning hozizon.
life_expectancy_ = 98
# if spouse doesn't have income, set these three parameters to 0 and give the spousal SS benefit factor a non-zero value like 0.3 (30%)
income_=0
increase_mean_=0.00
increase_sd_  =0.000
# if the spouse has her own income and claims her own ss, set this to 0; this is non-zero only when claiming spousal ss benefits instead of spousal's own ss
spousal_ss_benefit_factor = 0.3

# normally distributed expense: this is the most controllable factor in personal financial planning! To carefully control your spending is the most important and fundamental part of personal financial planning.
expense_mean=40000
expense_sd  =10000

# existing known MONTHLY expense: eg mortgage, car payment, child support, ...;  it will be converted into a yearly expense automatically
monthly_expense=1000
start_year     =1995
end_year       =2025

# Only one of these 5 filing status should be selected. Select one by uncommenting it and commenting out the currently uncommented one.
#filing_status=single
#filing_status=married_filing_separately
filing_status=married_filing_jointly
#filing_status=head_of_household
#filing_status=qualifying_window

# the total savings at the beginning of the planning horizon: this is the total available fund for any shortfall going forward
savings=100000
savings_rate_mean=0.04
savings_rate_sd  =0.003

# normally distributed inflation: adjust it to see its effect on you!  Currently, it inflates only your expenses.
inflation_mean=0.028
inflation_sd  =0.005

total_number_of_simulation_runs=100

# Choose charts from the following columns in any order:
# ["Income", "Taxable", "Federal", "State", "Expense", "Shortfall", "Net Worth"]
#
# For example: 
# what_to_chart1="Expense", "Income"
# will chart two lines, one for expense and the other for income on chart 1.
#
# For another example: 
# what_to_chart2="Net Worth"
# will chart only one line for Net Worth on chart 2.
#
#what_to_chart1="Income", "Taxable", "Federal", "State", "Expense", "Shortfall"
what_to_chart1="Income", "Federal", "State", "Expense", "Shortfall"
what_to_chart2="Net Worth"

# Changing this to any other positive integer results statistically 
# the same output, only with a different random sampling
seed_offset=3330

# Discount factor for the first two years of the planning horizon 
# to avoid unrealistic premature bankrupt
# Set it to 1.0 if you don't want use it
first_two_year_factor = 1.0
```

# Sample Outout

```

ruby lifecastor.rb 

SUMMARY
  Bankrupt probability:      17.0%
  Average bankrupt age:      97.0
  Avg horizon wealth:     454,216
```


