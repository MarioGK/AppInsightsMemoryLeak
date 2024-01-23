# README

There are two projects in this repository to reproduce the Memory Leak Bug.

Both projects are identifical apart from one having app insights installed and the other doesnt.

You can simply start both of them and use "dotnet-counters monitor --refresh-interval 1 -p XXX" on the running process and you will see that the one with AppInsights the memory will slowly increase, and it is right after an App Insights event.
