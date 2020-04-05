
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SPOT INSTANCE MANAGER IN GOOGLE CLOUD
============================================================================

Abstract
------------------
Like most cloud providers, Google Cloud provide spot instances for bussiness and individual use. Depending on the type of instance, these spot instances come at different prices and with different efficiency. Google Cloud provides what are called "Preemptible VMs". These have fixed prices and the customer acknoledges that they will be terminated after 24 hours whith a 30 seconds notice. Using these, they aim to make the market for ephemeral instances less complex and less fragmented. Basing on the fact that they provide a 30-second notice before getting eviction, in this project I aim to create an architecture that manages our google cloud instances. 

In this project, I aim implement a manager with a series of fault torelance mechanics to limit work lost during revocation of instances by Google cloud. Among others, I aim to implemenet a mechanism that frequently checks for health and available instances where we can move our work to in cases of eviction. This means that, as soon as we receive the eviction notice, we should be able to migrate our work to a healthy instance almost instateneously. In addition to that, to prevent work loss, I aim to implement a check-pointing mechanism. Since Google Cloud is guaranteed to terminate our instance after 24 hours, my manager tries to makes sure that regardless of whether we are evicted or not the work gets saved and moved to another instance. I will look through publications on cloud computing to find other mechansms that could be added to my manager.

In my implemenation, I will provide the design of my proposed architechure. I will also write source code and run experiments to gauge the perfomance of the manager. 


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


