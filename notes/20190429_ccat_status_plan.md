Journal, Rasmus Groth
Started: *20190429, Utterslev, Copenhagen, Denmark*
Edited: *20190703, Utterslev, Copenhagen, Denmark*

# CCAT status
## What is the big idea?
Develop a crypto trading platform that generates return on investment to:

a) Sustain me financially before August 1st 2019
b) Generate the equivalent of $20,000,000 in current value buying power by Jan 1st, 2023
c) Secure the girls a place at the table in a possible post-wellfare state world by generating sustainable generational family wealth before I retire/die (Jan 1st 2060)
d) Enable a directed effort to ensure mankinds survival, wellbeing, prosperity and trancendence via trusts, endowments and investments - direct and indirect involvement. (< 1,000,000,000 years from now)

Naturally, down the line, CCAT will not be the only activity to achieve these goals, but it is the first and the current focus. See the investment thesis for more on this.

## What did we do?
We built a trading bot that runs a trading strategy that is based on one pair (BTCUSD), one timeframe(1d) and one exchange(Bitmex).

### We learned how to:
- Program in python
- Work with Postgres
- write SQL queries
- Work with servers
- Discipline ourselves and manage our time
- Set up and work in the environments needed.


## What would we like to do now?
Make a living from CCAT before August 1st.

## What do we need to reach that goal?
We should divide our money into two buckets
|Fund |Allocation| Description|
|:--|:--|:--|
| Reserve | 50%| Protect this capital at all cost to prevent wiping out|
| Growth | 50% | Allocate as much capital as possible to high yield strategies. We are after maximum roi and will accept high risk.|

Ok, so we leave 50% on Coinmarketcap in EUR and put 50% onto Bitmex and other exchanges to enable active management. We rebalance this every week on Fridays.


## How do we spend the remaining time we have before we run out of money?
We have one month left to prove that this will work. How do we spend it?

- We need one strategy that works on the hour timeframe that yields comparable results to the ones on the daily.
- Put half the growth capital towards the auto-strategies and half towards manual trading based on Tradingview strategies.
- Develop a 1h candle algo strategy and deploy live on CCAT.
- Optional: Develop one additional manual strategy and trade it manually.



## QA
**Q:** Should I do this in Jupyter Notebooks and implement the TA-lib library to keep the engagement with CCAT going?
**A:** Yes! Do it.

**Q:** Should I do platform improvements and refactoring - for example Docker, workers, queuing, reports?
**A:** No. What we have built works. You will have to make do with what there is at this point. 100% focus on growing our capital

**Q:** Ok, so I should focus all my efforts on building a new 1h strategy now and then deploying it?
**A:** Yes.


## To do
- [ ] Test the current reversal strategy with a shorter ema length
- [ ] Develop and test a new 1hr strategy
- [x] Implement one strategy on CCAT
- [x] Create a bot for that strategy
- [x] Deploy




Later:
Make the system better








How may we:
- Prevent catastrophic failure?
- Protect our capital?
- Grow our capital?
- Live off our capital?
- Monitor the performance of the overall platform?
- Monitor the performance of each strategy?
- Backtest current and new strategies?
- Run machine learning based strategies
- Improve deploy process
- Assign and regulate allowance to each strategy dynamically
- Re-allocate funds to buckets according to the investment thesis we are working from

Next version:
Goal: Demonstrate significant growth to justify assigning more capital
Approach: Create a strategy that works on the one hour timeframe




LOOK AT:
- time indication and presentation
- database id's as UUIDs
- Use a json file to configure the bot
- Redis as task-queue
    - update database with candles
    - trades to be exectuted
    - ?
- Use Django or SQLalchemy as an ORM?


# Reduce complexity
- Use TAlib for indicators
-



# New functionality
- Log trades in database
- Execute several strategies concurrently
-


# Later
- Add exchange

### Packages we might use

#### [Freqtrade](https://github.com/freqtrade)
License:
Looks like freqtrade

PRO:

CON:
If I use freqtrade, I have to open source ccat


[TAlib](https://github.com/mrjbq7/ta-lib)




TRADING RULES

open position + close position = one trade

trade log:

bot-name, open timestamp, close timestamp

close all short positions when prior to going long for a given strategy
close all long positions when prior to going short for a given strategy


## Scrum meeting
**Project manager**: Hi guys. Good to see you here. Thank you for coming and joining this status and planning session. Before we start, I would just like to say that I am really super excited that we deployed the first version of CCAT and it looks like it is running as it should. Well done everyone. We didn't always follow the plans that I was responsible for making, but I have to admit that I am an absolute beginner like many of us, so I found it really enriching to learn more about how to manage this team of talented and unruly characters. What really impressed me is the spirit in which it was done. It was very hard to learn all the things we had to learn and there was a lot of resistance in some places, but it feels like it was resolved in a really generous, kind and ultimately pretty efficient way. I am grateful. Thank you all.
Ok. I suggest we do a round where we summarize what we all learned. Please share if you can.

### Learnings

**Python dev**: Hi everyone :)  
Thank you for those words, PM. Here is what I learned:
- How to actually program in Python
- How to work with modules and packages
- How to structure imports
- How good structural paradigms are incredibly rewarding to work with and save a lot of thinking and work
- How to use Pandas dataframes
- How to interface with the database
- How to work with unit-tests
- How to debug code

**Dev ops**: Hi guys!
Here is what I learned:
- How to set up our local machine to enable development work
- How to work with the AWS dashboard
- How to set up an Ubuntu server on AWS
- How to set up an RDS server on RDS
- How to set up security groups and zones on AWS
- How to work with Linode dashboard
- How to set up an Ubuntu server on Linode
- How to install postgres on the Ubuntu Linode server
- How to SSH tunnel
- How to mount a remote in the filesystem
- How to write basic shell commands
- How to work with Git
- How to work with Github
- How to work with virtual environments
- How to work with environment variables
- How to work with Crontab

**Database admin**:
- How to design a database
- The basics of the SQL language so that I now have the ability to write simple SQL queries
- The basics of working with the database through psql and pgcli

**Journalist**:
- How to take good technical notes
- How to make good cheat-sheets for later reference
- How to publish technical articles online

**Planner**:
- How to motivate everyone to be really disciplined and accountable
- How too much rigidity works against productivity if there isn't room for spontaneity
- How scheduling is often superior to goals and objectives.

Awesome, those are impressive learnings given we only had six months to do it. Now let us look at what we each accomplished. Please share if you can

### Accomplishments

**Python dev**:
- A set of scripts that enable us to trade on one exchange(Bitmex), one timeframe(1d) and one pair(BTCUSD).
- A module structure for the project
- A single strategy
- A set of signal scripts that the strategy depends on
- A set of indicator scripts that the signals depend on
- A feature script that the indicators depend on
- a single bot script to execute the trades

**Dev Ops**:
- A server running Postgres and Python on Linode
- A cronjob that executes every day at midnight
- A public github repo
- A private github repo
- An unfinished package on Pypi.

**DB admin**:
- A minimal but well structured Postgres database

**Journalist**:
- An article on how to merge postgres tables using a triple composite key
- A Medium article on how to calculate the age of the universe
- A Medium article on how to extract playlist information as csv from a Traktor
- An article on personal time management
- An article on Why we are here.
- An article on my career as a founder.
- Copious notes on CCAT
- Copious notes on Python programming
- Our first Stackoverflow answer.

**Planner**:
- A daily routine that has made us very much more disciplined
- A spreadsheet to track activity and progress
- A planning paradigm - blocks etc

It is great to see these accomplishments line up like this. We did a lot. We grew a lot. I am impressed by the earnestness of this effort.

Ok - next is what we can do to **simplify** the platform?

### Insights
**Python dev**:
- It was good to build a bunch of stuff to learn how to code, but I also understand now that code comes with maintenance, so better to use well-maintained open source code when possible.

**Dev Ops**:
- Less is more. After doing the AWS EC2+RDS setup, and then the Linode after, I would conclude that smallest thing you can do that will work for the given stage is the best thing to do.

**DB admin**:
- Taking the time to think through your infrastructure will pay off quickly.
- Don't do sequential integer id's

**Planner**:
- Self-doubt does not help. If I am spending time on something, it is probably because it is a good idea. It is better to respect each one of us and avoid second guessing and instead have really frank discussions like this where we look at how we might improve with the understanding that each of us are doing our best and really work for the benefit of the group.
- Testing in the wild is better than simulating.
- 80/20 rule applies!


### Biggest gamechanger going forward
**Quant**: Doubling our capital over the next month


### How to simplify
**Quant**:
- Use freqtrade?

**Python dev**:
- We could Use TA-lib for indicators (check if license allows this)
- We could use Django or SQLalchemy as an ORM to simplify the migration process
- Generally use well maintained public packages like TAlib instead of writing our own modules.
- We might even use [freqtrade](https://github.com/freqtrade) instead of CCAT

**Dev Ops**:
- We could look at using Docker
- We could work on a single database to avoid replication (would require backup and possibly a separate database server)

**DB admin**:
- We could use an ORM that allows for migration
- We could move the database to it's own server to avoid future complications


### Enhancements
**Quant**:
- Better simulation

**Planner**:
- Clearly defined objectives broken down into weekly deliverables.


### Biggest personal roadblocks
**Python dev**:
- Fear of making mistakes takes more time than making mistakes and correcting them.
- Fear of having to redo something

**Planner**:
- Clearly defining what success looks like
- Creating good milestones and deliverables so we don't end up in a never ending build.

### Biggest general roadblocks
**Python dev**:
- Lack of trading insight - might blow our money before we figure this out
- Lack of capital - Might erode our capital before we figure this out

**Dev ops**:

**Planner**:
- Lack of capital. Even if it does work, we will have to go our and find an income to avoid eroding the capital base.
- Lack of clear success-criteria

### Fun
What would be really fun for you to do?

**Python dev**:
- Make money!
- Reports
- Great simulation

**Quant**:
- Make Money
- A strategy that works on the one hour timeframe or smaller and trades at least twice per day to get more feedback




# PARKING LOT

**Condition**: Defcon 1
**State:** Maximum alert
**Description:** All systems set to ensure survival and removal of threats. This level of alertness will deplete resources if sustained for too long
**Time Allocation**: 100% money management

**Condition: Defcon 2**
**State:** High alert
**Description:**
**Time Allocation**: 50% money management, 50%


| Readiness condition | State | Description | Time allocation | Current state |
| :-- | :-- | :-- | :-- | :-- |
| Defcon 1 | Maximum alertness | All systems set to ensure survival and removal of threats. This level of alertness will deplete resources if sustained for too long |
| Defcon |
| Defcon 5 | Normal alertness | All systems are working and no threats or emergencies are registered. This state consumes the least amount of resources and yields the most | 1/3 platform improvements






Write plan and put it on wall / screen



## Time management - Defcon 5
- $\frac{1}{3}$ on platform improvements
- $\frac{1}{3}$ on strategies
- $\frac{1}{3}$ on money management

## Time management - Defcon 1
- As much as possible on strategy?



What are areas where we might run into trouble down the road if we make poor decisions now?
- It might be a good idea to look at using Django or SQLalchemy and Flask now if we are going to be using an ORM system?

What would be really fun for you to work on?

What are things you'd like to do?
- Set up a github based webpage for bit.io

Aspirations
I tried to make the system as ready to extend beyond that as I knew how without overthinking things at my current level.


## SWOT
### Strengths
### Weaknesses / vulnerabilities
### Opportunities
### Threats / risks
