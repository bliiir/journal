# Order execution

Get last row from strategy
Execute order if strategy says so

Approach 1
Strategy triggers executor
Executor executes order

Approach 2
Strategy creates order
Executor executes order


Approach 3
Scheduler runs strategy at appropriate intervals
Strategy


Scheduler ()
- Run bucket-update modules
- Run strategy modules
- Run status module


Strategy (controller)
- Run signals
- Trigger trader


Trader (controller)
- Execute order on exchange
- Log order in database


...

Status (model)
- Update Orders (model)
- Update Balances (model)


Manager
- Update strategy allocations (model)
