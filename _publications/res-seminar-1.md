---
title: "Hybrid Datacenter Scheduling"
collection: publications
permalink: /publications/res-seminar-1
venue: "BITS Pilani Research Seminar, BITS G649"
date: 2016-11-25
citation: '<b>Abhimanyu Rawat</b>, Arpit Srivastava'
---
This paper was presented as a part of garded subject BITS G649 related research seminar.

[Download paper here](https://ABresting.github.io/files/RES_SEMINAR.pdf)

## ABSTRACT

With the emergence of large data-centers, scheduling of workload has
become more challenging. Initially, centralized approach for scheduling
was widely used, but it had drawbacks of sub-optimal scheduling for the
small task as they were queued behind the large tasks.
Then models for fully distributed scheduling were proposed that has
other problem of performing badly for large task sets as required amount
of the data-center resources was not controlled by a distributed scheduler
hence resources were not allocated optimally. In our model, long jobs
are scheduled using the centralized scheduler while the short ones are
scheduled using the fully distributed scheduler. The distinction of a long
job from a short job varies based on the jobs arriving to scheduler. Along
with this to avoid queuing of the short jobs behind the long ones a partition
of the cluster is always reserved for the small jobs. The reserved size of the
partition varies as well depending on the inclination of size of jobs coming
for execution. Another feature of our model is that when a task is to be
scheduled by the distributed scheduler it probes the nodes for availability,
so when sending their response back the nodes could advertise their load
and other parameters to facilitate the scheduling decision.
We compare our results with the state-of-the-art fully Distributed
Sparrow scheduler, Hybrid scheduler Hawk and Eagle. We have evalu-
ated our model using trace-driven simulation, using traces with mixed
types of jobs with heavy load on cluster. On analysis, we were able to
achieve a good percentage of improvement over other schedulers.