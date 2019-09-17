**Title: DeepJS: Job Scheduling Based on Deep Reinforcement Learning in Cloud
Data Center**

**Publication: Proceeding ICBDC 2019 Proceedings of the 2019 4th International
Conference on Big Data and Computing Pages 48-53**

The aim of ICBDC 2020 is to present the latest research and results of
scientists related to Big Data and Computing topics. This conference provides
opportunities for the different areas delegates to exchange new ideas and
application experiences face to face, to establish business or research
relations and to find global partners for future collaboration.

**Author： Fengcun Li, State Key Laboratory of Networking and Switching
Technology, Beijing University of Posts and Telecommunications, Beijing, China**

>   **Bo Hu, State Key Laboratory of Networking and Switching Technology,
>   Beijing University of Posts and Telecommunications, Beijing, China**

**Paper Review**

-   Research Background

    -   Focused on solving scheduling problem based on neural network and
        machine learning algorithm

-   Problem to Solve

    -   Most of schedulers in this field are short on optimization their product
        DeepJS is intended to fitness calculation method which will minimize the
        makespan (maximize the throughput) of a set of jobs directly from
        experience.

-   Key Design and Algorithm Proposed

    -   Reinforcement Learning

        -   Based on agent and environment design

        -   Works with basic Monte Carlo method

    -   Algorithm

        -   Consist of five setups

            -   State space Machine task pair

            -   Action space 𝑁 pending tasks and 𝑀 machines in the cluster

            -   Rewards In order for the agent to learn effectively and obtain
                an effective scheduling policy that optimizes a specific
                performance metric -1 will be assigned to completed jobs

        -   Agent design tasks and machines are passing to a neural network then
            after running the algorithm the highest task machine pair will be
            assigned to run

        -   Training algorithm is based on neural network training and they
            fixed alpha which is either is best to run the training or to
            improve it we need to update alpha based on each training batch

-   Major Contribution

    -   The approach for using ML and neural network based on deep learning
        algorithm

-   Major limitation

    -   Similar jobs with similar weight can result in non-optimized solution

    -   Fixed alpha can cause an issue over different cloud infrastructure

    -   Their experiment was on Alibaba data set which can be different on other
        cloud infrastructure

-   Something you don’t understand

    -   Need to investigate more about the correctness of method

-   Your view on the research domain/topic/approach/data/solution (positive or
    negative)

    -   Combination of last paper and this one could be a better solution to
        scheduling task more properly.
