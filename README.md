# Build receipts

One line for every sent proposal on [Build](https://www.builderslive.org/research): the day it went out, the company letter, a size band, whether it was recorded the day it went or filed later from the sent mail, and the SHA-256 fingerprint of the exact PDF that was sent.

The file is refreshed every night from <https://www.builderslive.org/api/public/proof-ledger>. Git keeps every version, so anyone can see when each line first appeared. A bid can't be added later with an earlier date without it showing in the history.

## Check a proposal

Take a proposal PDF exactly as it was sent and fingerprint it:

```
sha256sum proposal.pdf          # macOS: shasum -a 256 proposal.pdf
grep <the fingerprint> receipts.csv
```

A match means that exact file is on the record, with the date it went. A re-saved or re-printed copy has a different fingerprint. The research page does the same check in the browser without uploading the file.

## What's in it, and what isn't

| Column | Meaning |
|---|---|
| `sent` | The day the proposal went out, Pacific time |
| `company` | A letter per company: A and B are the two steel subcontractors sending bids from Build |
| `size_band` | under $25K, $25K-$100K, $100K-$250K, $250K-$1M, or $1M and up |
| `recorded` | `live` when Build recorded the send the day it went; `filed` when it was filed later from the sent mail |
| `sha256` | The fingerprint of the exact PDF sent |

No company, contractor, client or job name is in this file. Two jobs are held off it for client confidentiality. The same PDF sent to two contractors appears twice.

`receipts.sha256` is the fingerprint of `receipts.csv` itself on the night it was written.
