Girocount Billing
Billing
Resellers / merchants
Collect money, deduct fees, pay out the rest
Sometimes we don’t collect money

Girocount determines fees, configurable per customer
Also rules e.g. tiered pricing, countries etc.; pricing can be inherited from a reseller

GC determines price
Produces bill document, reports
Internal reporting for financial team
Originate payouts -> mess for CM to help out; to SEPA/non-SEPA/urgent…
Overview prior to bill
Taxation etc.

Task management:
Import from Girogate
Cutoff, then aggregate, generate bills etc.
Big batch of tasks to run after midnight

Tech stack
Originally Monolith c++
Now Services / Tools / Tasks that do one job - modular C++ apps
Database as point of synchronisation / coupling
Optimus task written in Kotlin
Testing
Integration tests - start up services; check the database output; task level but also pipeline
E.g. test with a complex pricing setup ->
Runnable locally, packaged into a docker container that can be run

Deployment
K8s cluster AWS
AlgoCD
Engineers in control; small deployments from master

Clear out old transactions after around 200 days
1.3mln customers
Few hundred mln txns at any time
Bills kept forever

Database
R5 large (memory optimised)
UI -> real time usage
ACID
Integrity

GC not real time
Dependencies
In
Txns from Girogate (real time)
ICE old framework - a bit like gRPC (TCP)
Out
Sort txnx into buckets (Daily aggregates) - buckets per day, customer, payment method etc.
Then run processing tasks (billing, reports etc.)

Import hourly, copy from Girogate, a bit of ETL, store this (MySQL) as events;
On daily run aggregates (buckets) (summary) -> pricing comes in here (one bucket -> one set of pricing)
Generate bills into DB
Generate PDFs to send out, reports

Scheduler application

New features:
Done Taxation
Done Currency conversion
PPRO business entities
Improvements -> e.g. millions merchants (shift from big merchant with millions of txns)
Scalability (improvements in performance -> mostly changing the DB queries; memory)
In memory objects for customer etc.

New import service
Kinesis 
