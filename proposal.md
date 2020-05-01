Like most cloud providers, Google Cloud provides spot instances for businesses and individual use. Depending on the type of instance, these spot instances come at different prices and with different efficiency. Google Cloud provides what are called "Preemptible VMs". These have fixed prices and the customer acknowledges that they will be terminated after 24 hours with a 30 seconds notice. Using these, they aim to make the market for ephemeral instances less complex and less fragmented. Basing on the fact that they provide a 30-second notice before eviction, in this project I aim to create an architecture that manages our google cloud instances. 

In this project, I aim implement a manager with a series of fault tolerance mechanisms to limit work loss during revocation of instances by Google Cloud. Among others, I aim to implement a mechanism that frequently checks for health and available instances where we can move our work to in cases of eviction. This means that, as soon as we receive the eviction notice, we should be able to migrate our work to a healthy instance almost instantaneously. In addition to that, to prevent work loss, I aim to implement a check-pointing mechanism. Since Google Cloud is guaranteed to terminate our instance after 24 hours, my manager tries to makes sure that regardless of whether we are evicted or not the work gets saved and moved to another instance. I will look through publications on cloud computing to find other mechanisms that could be added to my manager.

In my implementation, I will provide the design of my proposed architecture. I will also write source code and run experiments to gauge the performance of the manager.

### Refernces:####
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