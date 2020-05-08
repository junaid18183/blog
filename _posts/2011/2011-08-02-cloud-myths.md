---
layout: post
title: Cloud Myths
categories: [cloud]
tags: [cloud,aws]
image: assets/images/aws.jpg
featured: false
hidden: true
comments: true
---
# Cloud Myths

## Myth #1: "I'm using virtualization/hypervisors in my data center -- I'm already running a cloud."

**Virtualization**, or more properly "operating system virtualization" (typically implemented by a hypervisor) is an important component of a cloud infrastructure, but by itself, does not implement cloud semantics. When a user requests a collection  of virtual machines (VMs) from a cloud, the VMs must be isolated from other VMs on the system in terms of their CPU access, memory access, network access, and access to persistent storage. Furthermore all of these forms of isolated access must be associated  with an authenticated user for security and charging purposes. Operating system virtualization and hypervisors provides unauthenticated isolation of CPUs and memories, but not a private inter-VM network and not per-allocation persistent storage. Thus a cloud  needs virtualization for part of its function, but data center virtualization, by itself, does not implement a cloud.

Clouds also provide a way for a cloud administrator to define either Service Level Agreements (SLAs) or Quality-of-Service (QoS) specifications that categorize the quality of access (and the resulting charging rate) individual users will  experience. Thus, in a cloud, an administrator defines a set of SLAs, groups users according to the SLAs to which they are entitled access, and determines a charging rate for each active SLA. Alternatively, in a virtualized data center, the system administrators  can use virtualization to control allocation of VMs to resources, but the notion of QoS or SLA is not exported to the end user as a way of enabling self-service provisioning.

In short, data center virtualization, alone, does not constitute cloud computing.

## Myth #2: "Cloud Computing is just Grid Computing by a different name."

There are several ways in which Cloud Computing and Grid computing are distinct from a conceptual point of view. First, Grids are architected so that a small number of users can gather and use most, if not all of the resources in the grid.  While those resources are in use, other users must wait (typically in one or more priority queues) for resource access. Because the duration and frequency of individual user resource allocations is highly variable and hard to predict, queuing delays can be  quite substantial, particularly in settings where machine utilization is high.

In contrast, clouds provide the illusion of "infinite scale" by supporting a large number of users, each of which is entitled to only a small fraction of the total cloud resource pool. By ensuring that the cloud is provisioned to support  the total number of possible simultaneous users (each requesting his or her maximum possible allocation), the resource usage pattern of any single user cannot cause a resource shortage. Thus cloud resource allocations are "on-demand" (resources are returned  to the user when they are requested without queuing delay) and atomic (an entire resource allocation request is typically satisfied without the possibility of partial allocation failure).

Another way in which clouds and grids are distinct is that grids support inter-grid federation below the API level. That is, a user of a grid expects that the grid infrastructure will enable him or her to access resources in other grids  somewhat transparently and under the control of the grid. As a result, grids are typically implemented as federated middleware that requires extensive and often complex policy mediation support. This need for policy mediation to be managed by the grid middleware  can lead to non-intuitive or non-deterministic behavior that users may interpret as grid instability.

Currently clouds implement federation at the API level. A user can make requests from multiple clouds simultaneously and if the cloud allocations allow routing to and from an external network, these allocations can be combined under user  control. Thus policy mediation occurs at the application level on a per-user basis making inconsistencies locally scoped and easier to rectify.

Thus, from the perspective of both the end-user and the infrastructure administrators, grids and clouds are distinct.

## Myth #3: "Clouds provide infinite scale."

Public clouds like those operated by Amazon or Google certainly comprise larger resource pools than most individual users or organizations could use effectively. Thus it is tempting to believe that from the perspective of a single user,  the amount of resource available is effectively limitless.</p>

This notion of infinite resource availability would be true, in practice, if each cloud were only to service a small user community and each user were not quota limited. In many application domains, however, individual users do have large  resource needs. So large, in fact, that if many of them (or even several of them) were to make large requests simultaneously even the largest clouds would run short of resources to provide. For these users, the cloud does not appear infinite.

Indeed, public clouds limit the total resource footprint that a "standard" user can control to a small quota, for this reason. Special users (after careful vetting) can have their quota increased but no user will be allowed to consume a  substantial fraction of the total resource pool for fear of causing a resource shortfall. For the vast majority of users who are using the public clouds to implement dynamically scaling web sites, the quota allowed is larger than these web sites typically  require, thereby providing the illusion of infinite scale. As resource-intensive, highly scalable applications begin to use cloud computing as either a public or on-premise platform, however, they will begin to reach the scaling limits imposed by resource  availability.

This difference also obscures the relationship between private and/or hybrid clouds and use of the public clouds. Data center operators occasionally cite the availability of "infinite resources" as a reason to use the public clouds instead  of an on-premise cloud or a hybrid cloud. In practice, most good-sized data centers have resource requirements that will exceed both, particularly if they are striving for high utilization levels. Public clouds offer the ability to "spill out" or "burst" from  a data center into a public cloud utility and vice versa if there is a resource shortfall. Better, more efficient, and user-controlled resource usage is possible through a combination of public and private clouds. Infinite scale, however, is an illusion provided  to users with only small to modest maximum requirements.

## Myth #4: "Clouds only provide 'pay-as-you-go' access."

One of the most attractive features of the public clouds is that they allow users to change their resource usage dynamically in response to customer demand or offered load, and to pay only for the resources being used from moment to moment.  While this type of charging is an important feature, it is by no means the only method a cloud can and should support. In particular, if an allocation is to be shared among several users within a single organization, it may make more sense to offer a maximum  resource quota on a subscription basis to keep conflicting resource needs from causing confusion. If multiple users are to share the VMs within a single allocation, enabling all of them to acquire and release resources dynamically (possible resources in use  by other users of the allocation) can lead to chaos.
