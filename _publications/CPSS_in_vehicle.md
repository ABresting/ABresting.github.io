---
title: "Decentralized Firmware Attestation for In-Vehicle Networks"
collection: publications
permalink: /publications/CPSS_in_vehicle
venue: "CPSS ’19, July 8, 2019, Auckland, New Zealand"
date: 2019-05-27
citation: 'Mohammad Khodari, <b>Abhimanyu Rawat</b>, Andrei Gurtov, Mikael Asplund'
---

[Download paper here](https://ABresting.github.io/files/CPSS_19_in_vehicle.pdf)

## ABSTRACT

Today’s vehicles are equipped with a large number of electronic
control units (ECUs), which control everything from heating to
steering and braking. Due to the increasing complexity and inter-
dependency of these units, it has become essential for an ECU to
be able to ensure the integrity of the firmware running on other
ECU’s to guarantee its own correct operation. Existing solutions
for firmware attestation uses a centralized approach which means
a single point of failure. In this article, we propose and investigate
a decentralized firmware attestation scheme for the automotive
domain. The basic idea of this scheme is that each ECU can attest
the state of those ECU’s on which it depends. Two flavors of ECU
attestation i.e. parallel and serial solution were designed, imple-
mented and evaluated. The two variants were compared in terms
of both detection performance (i.e., the ability to identify unautho-
rized firmware modifications) and timing performance. Our results
show that the proposed scheme is feasible to implement and that
the parallel solution showed a significant improvement in timing
performance over the serial solution.