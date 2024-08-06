# Durability

In [database systems](https://en.wikipedia.org/wiki/Database_system), **durability** is the [ACID](https://en.wikipedia.org/wiki/ACID) property that guarantees that the effects of [transactions](https://en.wikipedia.org/wiki/Database_transaction) that have been committed will survive permanently, even in case of failures, including incidents and catastrophic events.

For example, if a flight booking reports that a seat has successfully been booked, then the seat will remain booked even if the system crashes.

Formally, a database system ensures the durability property if it tolerates three types of failures:

1. **Transaction**
A transaction fails if its execution is interrupted before all its operations have been processed by the system.
These kinds of interruptions can be originated at the transaction level by data-entry errors, operator cancellation, [timeout](https://en.wikipedia.org/wiki/Timeout_(computing)), or application-specific errors, like withdrawing money from a bank account with insufficient funds.
2. **System**
At the system level, a failure occurs if the contents of the [volatile storage](https://en.wikipedia.org/wiki/Volatile_memory) are lost, due, for instance, to system [crashes](https://en.wikipedia.org/wiki/Crash_(computing)), like [out-of-memory](https://en.wikipedia.org/wiki/Out_of_memory) events.
3. **Media**
At the media level, where media means a stable storage that withstands system failures, failures happen when the stable storage, or part of it is lost.
These cases are typically represented by [disk failures](https://en.wikipedia.org/wiki/Hard_disk_drive_failure).

Thus, to be durable, the database system should implement strategies and operations that guarantee that:

- the changes of transactions that **have been committed** before the failure will survive the event (even by reconstruction)
- the changes of incomplete transactions, which have **not been committed yet** at the time of failure, will be reverted and will not affect the state of the database system

These behaviours are proven to be correct when the execution of transactions has respectively the [resilience](https://en.wikipedia.org/wiki/Resilience_(engineering_and_construction)) and [recoverability](https://en.wikipedia.org/wiki/Recoverability) properties.

---

## Mechanisms

![A simplified [finite state automaton](https://en.wikipedia.org/wiki/Finite-state_machine) showing possible DBMS after-failure (in red) states and the transitions (in black) that are necessary to return to a running system to achieve durability.](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Database_failure_states_and_relations.png/350px-Database_failure_states_and_relations.png)

A simplified [finite state automaton](https://en.wikipedia.org/wiki/Finite-state_machine) showing possible DBMS after-failure (in red) states and the transitions (in black) that are necessary to return to a running system to achieve durability.

In transaction-based systems, the mechanisms that assure durability are historically associated with the concept of [reliability](https://en.wikipedia.org/wiki/Reliability_engineering) of systems, as proposed by [Jim Gray](https://en.wikipedia.org/wiki/Jim_Gray_(computer_scientist)) in 1981.

This concept includes durability, but it also relies on aspects of the [atomicity](https://en.wikipedia.org/wiki/Atomicity_(database_systems)) and [consistency](https://en.wikipedia.org/wiki/Consistency_(database_systems)) properties.

Specifically, a reliability mechanism requires [primitives](https://en.wikipedia.org/wiki/Statement_(computer_science)) that explicitly state the beginning, the end, and the [rollback](https://en.wikipedia.org/wiki/Rollback_(data_management)) of transactions, which are also implied for the other two aforementioned properties. 

The mechanisms strictly related to durability are divided into three levels: 
transaction, system, and media level.

This can be seen as well for scenarios where failures could happen and that have to be considered in the design of database systems to address durability.

---

**Transaction level**

Durability against failures that occur at transaction level, such as cancelled calls and inconsistent actions that may be blocked before committing by [constraints](https://en.wikipedia.org/wiki/Constraint_(database)) and [triggers](https://en.wikipedia.org/wiki/Database_trigger), is guaranteed by the S[erializability](https://en.wikipedia.org/wiki/Serializability) property of the execution of transactions.

The state generated by the effects of precedently committed transactions is available in main 
memory and, thus, is resilient, while the changes carried by non-committed transactions can be undone.

In fact, thanks to Serializability, they can be discerned from other transactions and, therefore, their changes are discarded.[[3]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:1-3)

In addition, it is relevant to consider that in-place changes, which overwrite old values without keeping any kind of history are discouraged.

There exist multiple approaches that keep track of the history of changes, such as [timestamp](https://en.wikipedia.org/wiki/Timestamp-based_concurrency_control)-based solutions or [logging](https://en.wikipedia.org/wiki/Logging_(computing)) and [locking](https://en.wikipedia.org/wiki/Locking_(computer_science)).

---

**System level**

At system level, failures happen, by definition,[[3]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:1-3) when the contents of the volatile storage are lost. This can occur in events like system crashes or [power outages](https://en.wikipedia.org/wiki/Power_outage). Existing database systems use volatile storage (i.e. the [main memory](https://en.wikipedia.org/wiki/Computer_memory)
 of the system) for different purposes: some store their whole state and
 data in it, even without any durability guarantee; others keep the 
state and the data, or part of them, in memory, but also use the [non-volatile storage](https://en.wikipedia.org/wiki/Non-volatile_storage) for data; other systems only keep the state in main memory, while keeping all the data on disk.[[6]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-6)
 The reason behind the choice of having volatile storage, which is 
subject to this type of failure, and non-volatile storage, is found in 
the performance differences of the existing technologies that are used 
to implement these kinds of storage. However, the situation is likely to
 evolve as the popularity of [non-volatile memories (NVM)](https://en.wikipedia.org/wiki/Non_Volatile_Memory_Express) technologies grows.[[7]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-7)

In systems that include non-volatile storage, durability can be achieved by keeping and flushing an immutable sequential [log of the transactions](https://en.wikipedia.org/wiki/Transaction_log)
 to such non-volatile storage before acknowledging commitment. Thanks to
 their atomicity property, the transactions can be considered the unit 
of work in the [recovery](https://en.wikipedia.org/wiki/Data_recovery) process that guarantees durability while exploiting the log. In particular, the logging mechanism is called [write-ahead log (WAL)](https://en.wikipedia.org/wiki/Write-ahead_logging)
 and allows durability by buffering changes to the disk before they are 
synchronized from the main memory. In this way, by reconstruction from 
the log file, all committed transactions are resilient to system-level 
failures, because they can be redone. Non-committed transactions, 
instead, are recoverable, since their operations are logged to 
non-volatile storage before they effectively modify the state of the 
database.[[8]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:3-8)
 In this way, the partially executed operations can be undone without 
affecting the state of the system. After that, those transactions that 
were incomplete can be redone. Therefore, the transaction log from 
non-volatile storage can be reprocessed to recreate the system state 
right before any later system-level failure. Logging is done as a 
combination of tracking data and operations (i.e. transactions) for 
performance reasons.[[9]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-9)

**Media level**

At media level, failure scenarios affect non-volatile storage, like [hard disk drives](https://en.wikipedia.org/wiki/Hard_disk_drive), [solid-state drives](https://en.wikipedia.org/wiki/Solid-state_drive), and other types of [storage hardware components](https://en.wikipedia.org/wiki/Computer_data_storage).[[8]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:3-8)
 To guarantee durability at this level, the database system shall rely 
on stable memory, which is a memory that is completely and ideally 
failure-resistant. This kind of memory can be achieved with mechanisms 
of [replication](https://en.wikipedia.org/wiki/Replication_(computing)) and robust writing protocols.[[4]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:2-4)

Many tools and technologies are available to provide a logical stable memory, such as the [mirroring](https://en.wikipedia.org/wiki/Mirroring_RAID) of disks, and their choice depends on the [requirements](https://en.wikipedia.org/wiki/Requirement) of the specific applications.[[4]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:2-4) In general, replication and [redundancy](https://en.wikipedia.org/wiki/Redundancy_(engineering))
 strategies and architectures that behave like stable memory are 
available at different levels of the technology stack. In this way, even
 in case of catastrophic events where the storage hardware is damaged, [data loss](https://en.wikipedia.org/wiki/Data_loss) can be prevented.[[10]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-10) At this level, there is a strong bond between durability and [system and data recovery](https://en.wikipedia.org/wiki/Data_recovery), in the sense that the main goal is to preserve the data, not necessarily in online replicas, but also as offline copies.[[4]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:2-4) These last techniques fall into the categories of [backup](https://en.wikipedia.org/wiki/Backup), [data loss prevention](https://en.wikipedia.org/wiki/Data_loss_prevention_software), and [disaster recovery](https://en.wikipedia.org/wiki/Disaster_recovery).[[11]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-11)

Therefore, in case of media failure, the durability of 
transactions is guaranteed by the ability to reconstruct the state of 
the database from the log files stored in the stable memory, in any way 
it was implemented in the database system.[[8]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:3-8)
 There exist several mechanisms to store and reconstruct the state of a 
database system that improves the performance, both in terms of space 
and time, compared to managing all the log files created from the 
beginning of the database system. These mechanisms often include 
incremental [dumping](https://en.wikipedia.org/wiki/Database_dump), [differential files](https://en.wikipedia.org/wiki/Differential_backup), and [checkpoints](https://en.wikipedia.org/wiki/Database_checkpoint).[[12]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-12)

**Distributed databases**

In [distributed transactions](https://en.wikipedia.org/wiki/Distributed_transaction),
 ensuring durability requires additional mechanisms to preserve a 
consistent state sequence across all database nodes. This means, for 
example, that a single node may not be enough to decide to conclude a 
transaction by committing it. In fact, the resources used in that 
transaction may be on other nodes, where other transactions are 
occurring concurrently. Otherwise, in case of failure, if consistency 
could not be guaranteed, it would be impossible to acknowledge a safe 
state of the database for recovery.  For this reason, all participating 
nodes must coordinate before a commit can be acknowledged. This is 
usually done by a [two-phase commit protocol](https://en.wikipedia.org/wiki/Two-phase_commit_protocol).[[13]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:4-13)

In addition, in [distributed databases](https://en.wikipedia.org/wiki/Distributed_database), even the protocols for logging and recovery shall address the issues of [distributed environments](https://en.wikipedia.org/wiki/Distributed_computing), such as [deadlocks](https://en.wikipedia.org/wiki/Deadlock), that could prevent the resilience and recoverability of transactions and, thus, durability.[[13]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:4-13) A widely adopted family of algorithms that ensures these properties is [Algorithms for Recovery and Isolation Exploiting Semantics (ARIES)](https://en.wikipedia.org/wiki/Algorithms_for_Recovery_and_Isolation_Exploiting_Semantics).[[8]](https://en.wikipedia.org/wiki/Durability_(database_systems)#cite_note-:3-8)