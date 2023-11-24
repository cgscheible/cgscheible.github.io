---
tags: FinOps Cloud Kubernetes
---


Enterprise migrations often take a conservative approach to shifting application workloads from on-premise to public Cloud providers in that they attempt a like-for-like translation of infrastructure resources.

### Guaranteed availability is expensive

* The Cloud infrastructure sizing and availability parameters should be parameterized by environment. Flexibility in configuration translates into cost savings as not every Cloud environment needs the same sizing and availability. Environments that can be classified as development, sandbox, or proof-of-concept rarely need the full availability and sizing as compared with other enviroments that are serving customer traffic (staging, production).
* Reducing compute cost by 30 to 70% by switching from highest provider availability tier to a lower one. The main public Cloud players have a tiered pricing model where compute instances with lower guaranteed availability can be used for substantial discounts. Both, Amazon and Microsoft offer “spot” compute instances with the same capacity as their instances of the highest availability tier, “on demand”.
* The preference for “on demand” compute instances in enterprise migrations is usually based on the outdated availability model that sees application workload availability as a composite of the individual systems reliability of all involved infrastructure components.
* A more efficient allocation of compute capacity in public Cloud accounts would include “spot” instances to a certain percentage and only have “on demand” compute as a hard requirement for hosting the most inflexible and business critical applications.
* Managed Kubernetes clusters can ideally benefit from “spot” instances as the Kubernetes architecture considers compute capacity as ephemeral. Kubernetes workloads react quickly to failure events in cluster nodes as the scheduler reconfigures the workload allocation to the remaining available nodes. This minimizes any workload impact due to disappearing “spot” instances. As these nodes have a lower guaranteed availablity, their failure rate is higher than in the “on demand” nodes. Two features of managed Kuberntes clusters effectively mitigate the lower guaranteed availability of “spot” nodes:
	* Kubernetes cluster scheduler monitors and reallocates the application workloads across all available nodes.
	Kubernetes cluster nodes can be configured with automated recovery and even automated scaling. A good example is the Amazon EKS cluster-autoscaler add-on. 
	* A basic resilience against individual node failure is achieved with defining the nodes as part of autoscaling groups (Amazon) or VM Scale Sets (Azure). These groups automatically reconcile their desired state within minutes.

	
### Non-production environment should not run at production schedule (24/7)

Running non-production managed compute and storage (database) at the same schedule as production is only convenient from administrative perspective and a carryover from legacy on-premise practices. Cloud enviornments can be started and stopped on-demand or via schedule. This allows matching environment availability schedule with the office hours of the systems users, reducing the the system uptime from 24/7 to 18/5 (weekdays work hours across neighboring timeszones) or even lower. Application workloads that require compute capacity in predictable bursts, e.g. batch jobs, can use the on-demand caacity management even more aggressively: Spin-up the compute resources before the batch run and tear them down afterwards.

### Example topologies for different environments


![prod environment]({{site.url}}/assets/images/20231015/dc-prod.png){:style="display:block; margin-left:auto; margin-right:auto"}
{:refdef: style="text-align: center;"}
Production Environment with 2x High Availability and 24/7 uptime (no downtime schedule)
{:refdef }

Production environments typically have the highest resilience and availability requirements and this limits the options to save costs. With a resilience configuration across three availability zones, it is however feasible to evaluate lower guaranteed VM availability tiers, i.e. spot instead of on-demand VMs.

![staging environment]({{site.url}}/assets/images/20231015/dc-stg.png){:style="display:block; margin-left:auto; margin-right:auto"}
{:refdef: style="text-align: center;"}
Staging or Test Environment with 1x High Availability and 9/5 uptime (office hours)
{:refdef }

Production-like non-production environments allow more flexibility and can benefit from cost savings with reduced resilience (configuration across two availability zones instead of three) and a reduced VM availability of office hours (9h x 5 days) using a shutdown schedule.

![dev environment]({{site.url}}/assets/images/20231015/dc-dev.png){:style="display:block; margin-left:auto; margin-right:auto"}
{:refdef: style="text-align: center;"}
Development Environemnt with no High Availability and 9/5 uptime (office hours)
{:refdef }

Development environments can safely be scaled down even further with only automated recovery (configuration within only one availability zone and enabled autoscaling). Availability only during office hours using a shutdown schedule.


![legend]({{site.url}}/assets//images/20231015/dc-legend.png){:style="display:block; margin-left:auto; margin-right:auto"}
{:refdef: style="text-align: center;"}
Diagram legend
{:refdef }

### Unmanaged data is expensive

Data lifecycle should include a retention and access policy that meets the business requirements and at the same time is cost-effctive. On the flipside, this means that unmanaged data is expensive, especially when it is billed as periodic operating expense instead of capital cost. Both, shared filesystem storage and managed database storage are quite expensive in Cloud environments so an ever-growing application data volume should be a big concern. Many applications do not have built-in data management and instead rely on the application owners to come up with data housekeeping measures.

An application data lifecycle contains different data phases which balance the data access availability against data storage costs. The most expensive data availability is “live data” in that it needs to be available at all times with minimal query time. These are the frequently-accessed data files and database records that the business users need for their operations. Depending on the application performance requirements, some of this data might even be stored temporarily in a cache, e.g. using an in-memory database such as Redis. Older data should be archived to long-term storage and only restored on-demand.
