
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SPOT INSTANCE MANAGER IN GOOGLE CLOUD
============================================================================

Proposal
------------------
Like most cloud providers, Google Cloud provides spot instances for businesses and individual use. Depending on the type of instance, these spot instances come at different prices and with different efficiency. Google Cloud provides what are called "Preemptible VMs". These have fixed prices and the customer acknowledges that they will be terminated after 24 hours with a 30 seconds notice. Using these, they aim to make the market for ephemeral instances less complex and less fragmented. Basing on the fact that they provide a 30-second notice before eviction, in this project I aim to create an architecture that manages our google cloud instances. 

In this project, I aim implement a manager with a series of fault tolerance mechanisms to limit work loss during revocation of instances by Google Cloud. Among others, I aim to implement a mechanism that frequently checks for health and available instances where we can move our work to in cases of eviction. This means that, as soon as we receive the eviction notice, we should be able to migrate our work to a healthy instance almost instantaneously. In addition to that, to prevent work loss, I aim to implement a check-pointing mechanism. Since Google Cloud is guaranteed to terminate our instance after 24 hours, my manager tries to makes sure that regardless of whether we are evicted or not the work gets saved and moved to another instance. I will look through publications on cloud computing to find other mechanisms that could be added to my manager.

In my implementation, I will provide the design of my proposed architecture. I will also write source code and run experiments to gauge the performance of the manager.



Abstract
---------
Cloud service providers offer their unused resources for leasing in the spot market$^7$. One such service is provided by Google Cloud's Preemptible Virtual Machines. Preemptible VMs are Virtual Machines that offer lower costs in exchange for reduced reliability. Due to their below standard demand cost, they  can be used to compute resource intensive applications. The instances can however, be revoked at anytime depending on the fluctuations in their demand. To mitigate the impact of revocation, there is need to implement fault torelance-mechanism. In this paper, we propose a manager for Google Cloud spot instances that aims to reduce the impact of spot instance revocation. The manager implements state of the art mechanisms like continuous batch check-pointing, Virtual Machine replication and Virtual Machine health checking. To take an advantage of Preemptible VMs 24-hour window, the manager implements a scheduler that prioritizes migration of work from VMs with expiring leases.

Introduction
------------
### Motivation ###
Cloud computing has evolved continuously over the years. Cloud service providers now offer a wide variety of compute resources to their customers that are both cost effective and efficient. However, in some cases, there is a trade off between cost effectiveness and efficiency of the service. One such service that offers low cost compute resources at the expense of reliability is spot instances like Google Cloud's Preemptive VMs. Preemptive VMs are instances that you can create and run at a lower cost that normal instances$^8$. These instances require that your application has a fault tolerant mechanism because they can can be terminated at anytime depending on their demand. These instances are good for batch processing jobs because if the machine is terminated when processing one batch, the whole job does not completely stop.\\
\\
Unlike Amazon's Elastic Computer Cloud(EC2), Google's Preemptible instances always terminate after they run for 24 hours and they can not live migrate to other VM instnaces. However, the machines can be restarted to renew the 24 hours lease, though they can not be restarted automatically. Even after migration, the discs need to be deleted to avoid incurring storage charges.\\
\\Looking at the features of the instances, there is need for models and mechanisms to minimize the amount of work lost when the instances terminate while at the same time taking advantage of the low costs. Effective mechanisms to this have to continuously listen to eviction notices, find healthy machines to migrate to and have a proper scheduling mechanism that migrates works depending on their priorities

### Preemption process. ###

Google's Compute Engine is guaranteed to terminate these instances after 24 hours. However, due to fluctuations in their demand they can be terminated at anytime. Compute Engine send an eviction notice 30 seconds before instance termination. The 30 second warning is intended to allow clean up before migration. Once the 30s period elapses, the instances if terminated. The instance can be stopped and restarted manually. This allows Compute Engine to create a new lease for the tenant.

Background works
-----------------

Preemptible Virtual Machines manager
-------------------------------------
### Overview ###

### Fault tolerance mechanism ###

### Architecture and Implementation ###

references
-----------
    1. A Workflow Scheduling Technique to Consider Task Processing Rate in        Spot Instance-Based Cloud
        https://link.springer.com/chapter/10.1007/978-94-017-8798-7_59

    2. Time-Series Analysis for Price Prediction of Opportunistic Cloud           Computing Resources
        https://link.springer.com/chapter/10.1007/978-981-10-6520-0_23
    
    3. Reducing Costs of Spot Instances via Checkpointing in the Amazon           Elastic Compute Cloud
        https://ieeexplore.ieee.org/abstract/document/5557987
    
    4. Towards Optimal Bidding Strategy for Amazon EC2 Cloud Spot Instance
        https://ieeexplore.ieee.org/abstract/document/6253493
    
    5. An Efficient Checkpointing Scheme Using Price History of Spot Instances     in Cloud Computing Environment
        https://link.springer.com/chapter/10.1007/978-3-642-24403-2_16

    6. SpotOn: A Batch Computing Service for the Spot Market

    7. W. Voorsluys and R. Buyya, "Reliable Provisioning of Spot Instances for Compute-intensive Applications," 2012 IEEE 26th International Conference on Advanced Information Networking and Applications, Fukuoka, 2012, pp. 542-549.
    https://ieeexplore.ieee.org/abstract/document/6184917

    8.Preemptible VM instances
        https://cloud.google.com/compute/docs/instances/preemptible
    
    9. preemption_process
        https://cloud.google.com/compute/docs/instances/preemptible#preemption_process

