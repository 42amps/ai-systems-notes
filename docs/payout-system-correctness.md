# Payout System Correctness

PayRail is a demo payout engine for studying backend correctness in money-movement-style workflows. It does not integrate with real banks and does not move real money.

## Why Payout Systems Are Tricky

A payout system has to handle retries, duplicate client requests, background processing, state transitions, and concurrent balance checks. The hard part is not only creating a payout row. The hard part is preserving money integrity when requests arrive twice, workers retry, or two actions race against the same balance.

## Duplicate Requests and Idempotency

Clients retry requests when networks fail. Without idempotency, a user clicking once can accidentally create two payout requests if the first response is lost and the client retries.

PayRail uses an `Idempotency-Key` header and stores the response for each merchant/key pair. If the same key appears again, the API returns the stored response instead of creating another payout.

## Ledger-Derived Balances

A mutable `balance` column is simple, but it can drift from reality if updates are missed or applied twice. PayRail uses append-only ledger accounting:

- Credits add funds.
- Debits reserve or remove funds.
- Reversing credits refund failed payouts.
- Balance is derived from ledger entries.

This makes reconciliation easier because every movement is an inspectable row.

## Row-Level Locking

PayRail uses PostgreSQL row-level locking with `SELECT FOR UPDATE` on the merchant row. The critical section is:

1. Lock merchant row.
2. Check idempotency key.
3. Calculate ledger-derived balance.
4. Create payout.
5. Write debit ledger entry.
6. Store replayable response.

That serialization prevents two concurrent requests from both reading the same pre-debit balance.

## Explicit State Transitions

Payouts should not move through arbitrary statuses. PayRail models explicit transitions:

- `pending -> processing`
- `processing -> completed`
- `processing -> failed`

Terminal states do not move again. This prevents impossible transitions such as `failed -> completed`.

## Failure Refund Flow

When a payout fails, the system writes a reversing credit in the same transactional flow as the failure state transition. The goal is that status and accounting move together: either both are recorded, or neither is.

## Concurrent Double-Spend Example

Tiny Studio starts with INR 100. Two simultaneous INR 60 payout requests arrive.

Without locking, both requests could read INR 100 and both could succeed, reserving INR 120 against INR 100.

With row-level locking:

1. Request A locks the merchant row, sees INR 100, creates a payout, and writes an INR 60 debit.
2. Request B waits.
3. Request B then sees the updated INR 40 balance and is rejected.

The expected result is one successful payout reservation and one insufficient-balance response.

## Practical Lesson

Correct payout demos should make the invariants visible: no duplicate payout for the same idempotency key, no overdraft under concurrent requests, no hidden mutable balance drift, and no invalid payout state transition.
