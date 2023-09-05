# database

<details>
  <summary>
    Acid Property
  </summary>

  [lec12Notes.pdf](https://github.com/sachit914/database/files/12513565/lec12Notes.pdf)
  [lec12Notes (2).pdf](https://github.com/sachit914/database/files/12522752/lec12Notes.2.pdf)

  ## Transaction
A transaction is a series of operations against a database that's treated as a single unit. It either fully completes or is entirely undone in case of errors.

## ACID Properties
Databases use ACID properties to maintain data integrity:

Atomicity: A transaction completes entirely or not at all.
Consistency: The database remains consistent before and after a transaction.
Isolation: Transactions occur independently without interference.
Durability: Committed transaction changes are permanent.
## Transaction States
Active: Initial phase where operations are executed.
Partially Committed: Changes are in a buffer, pending confirmation.
Committed: Changes are permanent; rollback isn't possible.
Failed: Transaction halts due to errors.
Aborted: After a failure, changes are reversed.
Terminated: Transaction has either committed or aborted

</details>
