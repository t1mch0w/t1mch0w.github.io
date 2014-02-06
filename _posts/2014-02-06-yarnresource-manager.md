---
layout: post
title: "Yarn:Resource Manager"
description: ""
category: 
tags: []
---
{% include JB/setup %}
There are 6 parts in YARN ResourceManager: User Service, Security, Manage APPs, Manage AMs, Manage NMs and Resource Scheduler.

1. User Service: there are ClientRMService, AdminService and WebApp, respectively for client, admin and web.
2. Security, There are some parts for Security. (Skip, no so important.)
3. Manage APPs: RMAppManager controls the start and end of applications; ApplicationACLsManager controls the right to applications. ContainerApplocationExpirer closes containers which aren't used after allocated.
4. Manage NMs: NMLivenessMonitor tracks to know whether nodes are still alive; NodesListManager maintains node lists including normal node list and expection node list. ResourceTrackerService handles the requirements from NodeManager; The main two requrests are register and heart-beatn. IN heart-beaten, the information provided by nodemanager includes the running situation of each container, running applications list, health condition of each container and so on. The return information includes waiting-closed container list and waiting-closed application list.
5. In Manage AMs: AMLivelinessMonitor tracks to know whether the application is still working. If not, all containers of this applicaiton will be treated as die; ApplicationMasterLauncher is used to communicate with NodeManager to run application on node; ApplicationMasterService is also the similar functions as ResourceTrackerService in Manage NMs.
6. ResourceScheduler (Most Important): It's what I'm read.

Next, I'll track how user submit a job into system and what's the changes in resource manager.