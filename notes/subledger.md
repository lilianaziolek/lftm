Mid 2020 (Saul since Oct 2020)
Objective: track detailed accounting of all transactional operations
Vs General accounting ledger - not to replace, but to use detailed info to feed into general ledger
Why?
Compliance - financial auth ; near real time “how much money you’re holding for a specific customer” (you may know at the end of the month)
Billing system (Girocount) - we didn’t have a system that tells us how much we need to pay out LPMs fees (some subtract , some invoice at the end); a lot of effort to reconcile/calculate; cost engine we can configure to calculate cost of transactions + book these costs
Manual flows from finance dept that relies on data (recons, profit margins)
Platform to enable more products in the future (faster payouts - lend money for short periods)

Struggle: used to focus on features, less on “what’s the value” , now better
PM: Sumit, reporting Taka

Team:
Saul - dev first
At first 2 teams: ledger team and cost of sales team
(calculate cost and then book it in the ledger)
Saul Team Lead on ledger 2-3 eng
Ken Team Lead on cost of sales 2-3 eng
First milestone: to have booking achieved in Mar 2021
Started to build more features
Pricing can be very simple (1c / txn) or based on volume, or retroactively lowering previous ones

Strong inter-dependencies, building things a bit with a wall between
Merged two teams -> formed a single Subledger team
Team of 7engs + EM (Saul) + PEng (Ken)
2-3 really senior
Most middle
2 junior
Assignments individual; code reviews, if very complex 2 reviewers;

Change estimation mechanism

Architecture:
Txn -> stores into Keyspace (== Cassandra)
Enriches with history and  republishes
Consumers
Txn Agg [how many txns, what was volume so far etc] -> postgres
Cost for ppro and customer -> publish fee on kafka
Transaction fee

Txn will pick this up, enrich, republish to a different topic


Publish all, book in Ledger (Postgres) + writeahead log to BQ


Cost of Sales - how much we need to pay to LPM
Transaction Fee - how much we charge the customer


Kotlin -> Micronaut; some no framework; no Spring Boots
https://miro.com/app/board/o9J_lXEBCro=/

https://ppro.atlassian.net/wiki/spaces/ENG/pages/3925770243/RFC+Funds+Flow+Gateway+Agnostic+Model
https://docs.google.com/presentation/d/1DxoaeirjYu1X2hWpLrZaq2Y2eVX0Zd4TNfIxm4B9IA0/edit#slide=id.g135b8ef5ceb_2_20
https://docs.google.com/document/d/1fwy_lUAizrZVeWPvo8Y6UGblnBpn2lxrgsZwd04aGP8/edit


Feeds of girogate data => determine cost, fees => book in ledger


Ledger not very good at balance calculations

Real-time visibility vs near-real-time
But only for some use cases

E.g. recon doesn’t need realtime
Moving balances out of postgres


