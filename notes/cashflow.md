Cash Flow
Bring transparency on payouts and settlements; when we pay / receive money to/from customers; mostly to be used in treasury

[Node-RED]

Info from Girocount about money we need to pay
Possible adjustments
Then submit payout => generate SEPA and non-SEPA payouts to go to GEVA or someone else
Then we get MT940 files that allow us to confirm that payout happened

Then we book into ledger
Put into archive


Payouts:
We send invoices
When they pay we mark as received


Audit trail for user’s actions (changes by user or processes)


Postgres in dev in pod

Lambda function consuming mt940 (and other) files => converts to events that now go into dynamoDB


Gitlab pipeline in project => generate some magic file into a special (separate) gitlab repo => picked up by Argo CD

Auto-kustomize -> alternative to helm charts

Kubectl



OMG the overengineering
Kill it with fire
