# database

<details>
  <summary>
    Acid Property
  </summary>

  [lec12Notes.pdf](https://github.com/sachit914/database/files/12513565/lec12Notes.pdf)
  [lec12Notes (2).pdf](https://github.com/sachit914/database/files/12522752/lec12Notes.2.pdf)

  ## Transaction
A transaction is a series of operations against a database that's treated as a single unit. It either fully completes or is entirely undone in case of errors.

```
-- Start the transaction
BEGIN TRANSACTION;

-- Do some work
UPDATE Account SET Balance = Balance - 100 WHERE AccountId = 1;
UPDATE Account SET Balance = Balance + 100 WHERE AccountId = 2;

-- Commit the transaction if everything went well
COMMIT TRANSACTION;

```


## ACID Properties
Databases use ACID properties to maintain data integrity:

Atomicity: A transaction completes entirely or not at all.

```
BEGIN TRANSACTION;

-- Assume we are transferring money between two bank accounts
TRY
{
    UPDATE BankAccounts SET Balance = Balance - 100 WHERE AccountNumber = 'A123';
    UPDATE BankAccounts SET Balance = Balance + 100 WHERE AccountNumber = 'B456';
}
CATCH
{
    ROLLBACK TRANSACTION;
    THROW;
}

COMMIT TRANSACTION;

```

Consistency: The database remains consistent before and after a transaction.

Isolation: Transactions occur independently without interference.

```
Definition: Isolation ensures transactions are processed independently and securely, preventing interference from concurrent transactions.

Transaction Levels:

Read Uncommitted: Lowest level; transactions may see uncommitted changes from others (can lead to "dirty reads").
Read Committed: Transactions only read committed data, preventing dirty reads.
Repeatable Read: Blocks other transactions from modifying or inserting data being read, guarding against non-repeatable reads.
Serializable: Highest level; ensures full transaction separation, typically using row locks.
Locking:

Shared Locks: Multiple transactions can read, but not modify, a data piece.
Exclusive Locks: Only one transaction can read and write a data piece, blocking all others.
Optimistic Locks: Checks for conflicts only at commit time, assuming rare conflicts.
Pessimistic Locks: Locks data immediately upon access, anticipating conflicts.
MVCC (Multi-Version Concurrency Control): Allows transactions to interact with different versions of the same data piece, improving concurrency by reducing locking needs.

Timestamp Ordering: Assigns timestamps to transactions and orders them accordingly to ensure serializability.

Application-Level Isolation: Designing applications to manage concurrency, e.g., by retrying transactions that encounter concurrency conflicts.

Database Configuration: Adjusting database settings, like maximum locks or lock timeouts, to fine-tune isolation levels and behaviors.
```

Durability: Committed transaction changes are permanent.

<details>

  <summary>
    click
  </summary>

  Definition: Durability guarantees that once a transaction is successfully committed, its changes to the database are permanent and will not be lost.

Write-Ahead Logging (WAL): This technique involves logging changes before applying them to the database. If a crash occurs, the system can recover by replaying the log.

Backup and Recovery: Regular backups (full, differential, incremental) ensure that data can be restored to a consistent state after a failure. Recovery mechanisms utilize these backups to restore data.

Redundancy: Using replication or clustering, databases store copies of data on multiple machines or disks. If one fails, another can take over, ensuring durability.

Atomic Commit Protocols: Ensure that a transaction's changes are saved only if every part of the transaction succeeds. If any part fails, changes aren't saved.

Checkpoints: Periodic checkpoint processes save the current state of the database to disk, minimizing the amount of data that needs to be recovered in case of failures.

Database Journaling: A sequential log where all changes are recorded. This can be used to replay actions to bring a database to its current state after a crash.

Disk Write Strategies: Techniques like buffering and cache management control how and when changes are written to disk, ensuring data integrity and durability.

Fail-Safe Measures: Features like battery-backed RAM or uninterruptible power supplies (UPS) ensure that committed transactions are saved even in power outages.

Cloud and Distributed Systems: Modern distributed systems provide durability by ensuring data is consistently stored across multiple physical locations or even across data centers.
</details>

## Transaction States
Active: Initial phase where operations are executed.

Partially Committed: Changes are in a buffer, pending confirmation.

Committed: Changes are permanent; rollback isn't possible.

Failed: Transaction halts due to errors.

Aborted: After a failure, changes are reversed.

Terminated: Transaction has either committed or aborted

</details>
