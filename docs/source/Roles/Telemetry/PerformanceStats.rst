Performance stats of telemetry acquisition service
+++++++++++++++++++++++++++++++++++++++++++++++++++

Omnia telemetry testing is conducted on a cluster under 3 different conditions:

    1.	Omnia Telemetry service running on all nodes provided in the inventory file before running MPI jobs.
    2.	Omnia Telemetry service running on all nodes provided in the inventory file while running MPI jobs.
    3.	Omnia Telemetry service running on all nodes provided in the inventory file post MPI job execution.

For this performance testing, the below cluster and parameters are considered:

+----------------------------------+-------------------------------------------------+
|  **Cluster**                     | 1 manager node, 1 login node, 3   compute nodes |
+----------------------------------+-------------------------------------------------+
| **Omnia_collection_interval**    | 60 seconds                                      |
+----------------------------------+-------------------------------------------------+
| **Fuzzy_offset**                 | 60                                              |
+----------------------------------+-------------------------------------------------+
| **Metric_collection_timeout**    | 5 seconds                                       |
+----------------------------------+-------------------------------------------------+
| **Scheduler_type**               | Slurm and Kuberenetes                           |
+----------------------------------+-------------------------------------------------+

With the above parameters, CPU and memory utilization on nodes are as below:

+-------------------+-------------------------------------+------------------------------------+-------------------------------------+
|                   | Pre MPI jobs                        | While running MPI jobs             | Post MPI jobs                       |
+===================+=====================================+====================================+=====================================+
| **Compute node**  | Avg Cpu Utilization: 24.05%         | Avg Cpu Utilization: 26.34%        | Avg Cpu Utilization: 31.63%         |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Average memory utilization: 7.7674% | Average memory utilization: 2.903% | Average memory utilization: 2.910%  |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Max number of processes: 5          | Max number of processes: 6         | Max number of processes: 5          |
+-------------------+-------------------------------------+------------------------------------+-------------------------------------+
| **Login node**    | Avg Cpu Utilization: 24.42%         | Avg Cpu Utilization: 0.37%         | Avg Cpu Utilization: 0.35%          |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Average memory utilization: 99.98%  | Average memory utilization: 2.6%   | Average memory utilization: 2.65    |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Max number of processes: 6          | Max number of processes: 5         | Max number of processes: 5          |
+-------------------+-------------------------------------+------------------------------------+-------------------------------------+
| **Manager Node**  | Avg Cpu Utilization: 26.14%         | Avg Cpu Utilization: 27.03%        | Avg Cpu Utilization: 29.22%         |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Average memory utilization: 14.307% | Average memory utilization: 15.572%| Average memory utilization: 15.500% |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Max number of processes: 7          | Max number of processes: 7         | Max number of processes: 8          |
+-------------------+-------------------------------------+------------------------------------+-------------------------------------+
| **Control Plane** | Avg Cpu Utilization: 3.17%          | Avg Cpu Utilization: 3.27%         | Avg Cpu Utilization: 3.19%          |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Average memory utilization: 18.68%  | Average memory utilization: 24.85% | Average memory utilization: 24.93%  |
+-------------------+-------------------------------------+------------------------------------+-------------------------------------+
| **Overall**       | Avg Cpu Utilization: 24.87%         | Avg Cpu Utilization: 84.58%        | Avg Cpu Utilization: 20.40%         |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Average memory utilization: 7.69%   | Average memory utilization: 7.02%  | Average memory utilization: 7.003%  |
|                   +-------------------------------------+------------------------------------+-------------------------------------+
|                   | Max number of processes: 7          | Max number of processes: 7         |                                     |
+-------------------+-------------------------------------+------------------------------------+-------------------------------------+


