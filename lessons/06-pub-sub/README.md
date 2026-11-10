# Section 6: Pub/Sub and Data Publishing

_Planning outline preserved from the source notebook (written in the author's own markdown-style shorthand):_

> ### Module 6 — Pub/Sub and Data Publishing
> *~45 min*
> Connects the loader to the tick-plant processes built in Module 4.
> - Add a Messaging Service (MS) to the workflow and explain why MS is required for interprocess discoverability (IPC Utils vs. GW Connections).
> - Configure pub/sub from FileWatcher to TP, including a custom `upd` for reference data.
> - Validate the data flow: check subscriptions in MS, confirm data reaches the RDB.
>
> Lesson 6.1 Overview of MS
> Lesson 6.2 Messaging Configuration via instance parameter
> Lesson 6.3 Messaging Configuration via messaging apis
> Lesson 6.4 Handy functions/utils for debugging
