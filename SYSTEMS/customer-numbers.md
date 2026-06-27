# 🔢 Customer Number System
_Updated: 2026-06-27_

- **Format:** `AIAX-####` — branded prefix + zero-padded 4-digit sequential.
- **Field:** `customer_number` on the Customer entity.
- **Appears on:** invoices, account details, admin customer list, billing statements.

## Existing customers
| Number | Company | Contact |
|---|---|---|
| `AIAX-0001` | Summit Ridge Dental | Dr. Jordan Avery |
| `AIAX-0002` | Harbor Point Law | Marcus Webb |

## Rule
When generating ANY document (PDF invoice, statement, etc.), always pull `customer_number` from the live Customer record so it matches the portals exactly.