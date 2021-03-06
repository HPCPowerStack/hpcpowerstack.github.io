---
layout: default
---

<h1 align="center">FAQs</h1>

[What is the goal of the PowerStack efforts?](#goal)
<br/>
[What entity is funding the PowerStack initiative?](#funding)
<br/>
[What is the current status of the PowerStack initiative?](#status)
<br/>
[What was the outcome of the PowerStack seminar?](#outcome)
<br/>
[What is the difference between the PowerAPI and the PowerStack efforts?](#compare)
<br/>
[How does the PowerAPI team plan on contributing to the PowerStack initiative?](#powerapi_contrib)
<br/>
[How does the EPA-JSRM team plan on contributing to the PowerStack initiative?](#epajsrm_contrib)
<br/>
[What are some of the potential next steps for the PowerStack initiative?](#next_steps)
<br/>

---

### [What is the goal of the PowerStack efforts?](#goal)
The initial work towards the PowerStack started in 2017. The work
arose out of the realization that there is no common consensus among the
vendors/labs/academia on what software agents are needed to drive energy/power
management across various layers of the system software stack and how they
should interact to coordinate optimizations to power/energy at different
granularities in the system. In fact, this issue has been floating around ever
since the power challenges to exascale became evident. So the goal of this
initiative was simple -- get the community to agree upon how different software
agents can interoperate with each other, without overstepping on each other's
power/energy control mechanisms. Since getting the entire community on the same
page is difficult without having structured discussions and specific proposals
to build on, the PowerStack core team (LLNL, TUM, Univ of Tokyo, Intel)
decided to work on an initial proposal for a PowerStack strawman architecture
in a small group setting to seed discussions, then bring the proposal forward
to progressively broader groups for review and refinement.

---

### <a name="funding">What entity is funding the PowerStack initiative?</a>
There is no centralized entity that single-handedly funds the PowerStack. The
team is essentially a task-force comprising of members of academia, labs, and
vendors, each specializing in some layer of the system stack. Because there is
no single developer of the entire stack, it is only pragmatic for different
stakeholders to design their individual products such that they are compatible
with a uniform stack that drives robust energy/power management solutions.

---

### <a name="status">What is the current status of the PowerStack initiative?</a>
The steps that have been taken so far include:
1. identify the different software actors that are involved in driving system-side efficiency
2. identify the roles and responsibilities of each of these actors
3. work towards prototyping how each of these actors would behave independently
4. discuss and prototype how each of these actors would interoperate with each other
5. prepare a strawman draft documenting this
6. solicit feedback from some of the key HPC players to get their consensus and then decide the next steps.

For Step 3 -- as a starting point -- the PowerStack team chose to leverage
existing open-source HPC projects like the slurm plugin, msr-safe library, and the
geopm framework. Work on these projects started long before the conception of
the PowerStack. Nevertheless, a conscious effort is being made to ensure that
any further development on these projects is "Power Stack-aware".

Step 4 is still a work-in-progress.

Initial strawman for Step 5 can be found <a href="strawman.pdf">here.</a>

Step 6 took the form of an invitational PowerStack seminar, the week before
ISC18 in Raitenhaslach, Germany. Due to space constraints at the venue, the
attendance was limited to about 40 representatives from labs, academia, and
vendors that have played a key role in designing the different layers of the
HPC stack.

---

### <a name="outcome">What was the outcome of the PowerStack seminar?</a>
<ol>
<li>the attendees came to a consensus on three key software actors that need to
play a role within the PowerStack --</li>
<ol type="a">
<li>system-wide manager (job scheduler/ job resource mgr e.g. slurm, pbspro,
alps),</li>
<li>job-level manager (e.g. geopm, conductor),</li>
<li>physical-node manager (e.g. libmsr, papi, nvml, x86_adapt, hdeem)</li>
</ol>

<br>
For each of these actors, the attendees identified -- the goals, the list of
monitored telemetry, the list of control knobs, and the decision/arbitration
mechanisms in place.

<li>The attendees agreed upon four channels of interoperability among the
actors --</li>
<ol type="a">
<li>job scheduler <--> job-level manager</li>
<li>job scheduler <--> physical node manager</li>
<li>job manager <--> physical node manager</li>
<li>job scheduler <--> site-wide policy manager</li>
</ol>

<br/>
Channel (d) was initially categorized as 'out-of-scope'. Nevertheless, the
attendees felt the need to discuss this briefly during the seminar. Channels (b)
and (c) was where the results of the recent global survey conducted by the
EPA-JSRM team (EEHPC WG) were applied, during the seminar.

<br/>
<br/>

From the global survey conducted by the EPA-JSRM team, it has been evident that
-- at a higher level -- sites have separate mechanisms in place for managing
nodes that were idle and those that actively serviced jobs. These correspond to
Channels (b) and (c), respectively.
</ol>

---

### <a name="compare">What is the difference between the PowerAPI and the PowerStack efforts?</a>
The charter of the PowerAPI community is to design and develop a
*standardized specification* that helps drive energy/power efficiency
among all the layers within the HPC system stack. This specification lists
multiple function definitions that can be invoked by different layers of the
stack. One of the strengths of the current specification is that it is very
flexible in that it enables any two actors within the stack to communicate with
each other via the parameters within these functions. This drives
*portability* among vendors investing in power management.

The charter of the PowerStack community is to design a holistic, flexible and
extensible concept of a *software stack ecosystem* Its charter is to:
1. identify what are the different actors within the software stack that are
responsible for driving energy/power efficiency
2. get a consensus within the community about what are the roles and
responsibilities of each of these actors
3. how can these actors collaborate with each other while implementing an
end-to-end solution for system efficiency
4. aid in software-hardware co-design and engineering that is compatible with
the stack.

*Input from the PowerAPI + PowerStack members:*<br/>
PowerAPI is a specification that allows applications, system software, and
tools to have a portable, hardware/vendor-agnostic interface to the
power/energy monitoring and management capabilities of a system. HPC Power
Stack is a stack of hierarchical software and firmware components that optimize
system-level power/energy consumption through coordinated optimization of
power/energy at different granularities in the system. Where suitable, the
PowerStack efforts will influence and adhere to interfaces in the PowerAPI
specification for information exchange between components.

*Example of a use-case:*<br/>
Assume there exists a system with compute nodes that expose power capping knobs
to the software stack. Assume a site policy where user-jobs are required to
execute under a predetermined power budget.

The PowerAPI spec provides specific function calls that can be used to
implement solutions where either the job scheduler or a job runtime or both
could access the hardware knobs for enforcing the power budget. Since the
actual access to the knobs would vary from one vendor to another, the
PowerAPI's plugin-in interface enables the job scheduler and a job runtime to
remain oblivious of the underlying implementation.

The PowerStack effort, on the other hand, takes the approach of first getting
the community to come to a consensus on -- Whose responsibility is it to access
the hardware knobs, in the first place? The job-scheduler, or a user-level
runtime? One of the strengths of a job scheduler is that it is aware of the
site-wide power policy and the status of the power consumption of the entire
system. It is, however, not aware of the specific design of the jobs and its
power profile. Likewise, a job manager/runtime is aware of application phases,
compute-load distribution, communication patterns, and is capable of
dynamically monitoring its power profile. It is, however, not aware of the
power budget it should run at to ensure system-wide efficiency. This example
was discussed extensively during the PowerStack seminar. The solution that was
agreed upon was that it makes sense for the job scheduler to communicate the
power budget to a job-level runtime. And then, it is the responsibility of the
runtime to distribute the power efficiently among the nodes servicing the job.

This is in perfect alignment with some of the lessons learned from the global
survey conducted by the EPA-JSRM (EEHPC WG) team -- HPC sites treat "Active
node power management" quite differently from "Idle node power management". For
idle nodes, the job scheduler can take up the responsibility of enforcing power
caps. For nodes actively servicing jobs, the job scheduler should be capable of
handing over the power capping responsibility to a job-level agent.

---

### <a name="powerapi_contrib">How does the PowerAPI team plan on contributing to
the PowerStack initiative?</a>
From the PowerAPI spec -- “PowerAPI provides multiple levels of abstractions to
satisfy the requirements of multiple types of users”. In accordance with this,
the team is willing to work with PowerStack on any and all areas where the
PowerAPI function set is found insufficient. During the last two meetings,
members of the PowerAPI team observed that there is a need for improving the
"job-scheduler <--> user application interface" within the PowerAPI spec. To
ensure that the spec does not become incompatible with the design of any of the
existing power-aware job schedulers (or workload managers), it is important to
include the vendors into this discussion. As one of the next steps, the
PowerAPI team is interested in contributing towards a PowerStack working group
(see below) that focuses on the "job-scheduler <--> job-level manager"
interoperability.

---

### <a name="epajsrm_contrib">How does the EPA-JSRM team plan on contributing to the PowerStack initiative?</a>
The EPA-JSRM is in a strong position to share lessons learned from their past
survey of multiple HPC sites that are actively investing in energy- and
power-aware job scheduling and resource management. During the last two meetings,
the EPA-JSRM team expressed interest in helping the PowerStack community by
contributing some bandwidth towards designing bi-directional communication
mechanisms between job schedulers and the job-level manager.

---

### <a name="next_steps">What are some of the potential next steps for the PowerStack initiative?</a>
Towards the end of the PowerStack seminar, the attendees expressed interest in
contributing towards specific working groups that focus on a specific portion
of the stack. If there is enough interest, one direction we can take -- as a
community -- is to have topic-based working groups that meet periodically to
make progress on their assigned tasks.

Some candidate topics include:
* Group 1: Focus on job scheduler <--> job-level manager interoperability
(Active node power management)
* Group 2: Focus on job scheduler <--> node-manger interoperability (Idle
node power management)
* Group 3: Focus on designing solutions for job schedulers to dynamically
switch between communication with the job-level manager and the node-level
manager
* Group 4: Focus on designing solutions for accessing in-band and out-of-band
hardware control knobs accessible via either the node-level manager or the job
scheduler
* Group 5: Focus on the communication of site-level power policy to the job
scheduler


[Back](./)
