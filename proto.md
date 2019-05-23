---
layout: default
---

## Webinars
* [The PowerStack Initiative (A Community-driven Effort)](https://eehpcwg.llnl.gov/assets/091218_webinar_powerstack.pdf), EEHPC-WG Webinar Series, October 2018

## News Articles
* [“PowerStack: A global response to the power management problem for exascale”](https://www.hipeac.net/news/6895/powerstack-a-global-response-to-the-power-management-problem-for-exascale/), HIPEAC 2019 Blog Article
* [Power and Performance Optimization at Exascale](https://insidehpc.com/2018/03/podcast-power-peformance-optimization-Exascale/), InsideHPC, March 2018
* [Energy efficiency and the software stack](https://insidehpc.com/2017/12/sc17-energy-efficiency-software-stack-cross-community-efforts/), InsideHPC, December 2017
* [A global survey of HPC center energy and power-aware job scheduling and resource management](https://insidehpc.com/2017/12/first-global-survey-energy-power-aware-job-scheduling-resource-management/), InsideHPC, November 2017

## Publications on System/Site-Level Efficiency Studies
* Ryuichi Sakamoto et al., [“Analyzing Resource Trade-offs in Hardware Overprovisioned Supercomputers”](https://ieeexplore.ieee.org/document/8425206/), IPDPS 2018
* Matthias Maiterth et al., [“Energy and Power-Aware Job Scheduling and Resource Management: Global Survey - Initial Analysis”](https://ieeexplore.ieee.org/document/8425478), HPPAC 2018

## Publications on Application-Level Efficiency Studies
* Eastep et al., [“Global Extensible Open Power Manager: A vehicle for HPC Community Collaboration on Co-Designed Energy Management Solutions"](https://link.springer.com/chapter/10.1007/978-3-319-58667-0_21), ISC 2017

## Strawman Docs
* ["A Strawman for an HPC PowerStack"](strawman.pdf), OSTI Technical Report, August 2018

---

The PowerStack team intends to leverage existing well-engineered solutions when
designing and implementing interfaces that work through various layers of the
stack. Here, we list state-of-the-art software for power management that we are
exploring and intending to extend as a part of this approach. Links to
software/repositories to be added shortly.

## Resource Managers/Schedulers
* SLURM
* PBSPro
* Cobalt
* Flux

## Runtime Systems
* [GEOPM](https://geopm.github.io/)
* [READEX](https://github.com/readex-eu)

## Node-Level Interfaces
* [msr-safe](https://github.com/llnl/msr-safe)/[libmsr](https://github.com/llnl/libmsr) (Intel)
* OPAL/Amester (IBM)
* NVML (NVIDIA)
* Variorum (vendor-neutral)

## Existing Standardization Efforts
* [PowerAPI](https://powerapi.sandia.gov/) (specifications with focus on node-level design)
* [EEHPCWG JSRM](https://eehpcwg.llnl.gov/) (focus on site-level job scheduling policies)


[Back](./)
