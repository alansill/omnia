Adding new nodes
+++++++++++++++++

**Provisioning the new node**

While adding a new node to the cluster, users can modify the following:

    - The operating system
    - CUDA
    - OFED

A new node can be added using the following ways:

1. When the discovery mechanism is ``switch-based``:

    * Edit or append JSON list stored in ``switch-based-details`` in ``input/provision_config.yml``.

    .. note::
        * All ports residing on the same switch should be listed in the same JSON list element.
        * Ports configured via Omnia should be not be removed from ``switch-based-details`` in ``input/provision_config.yml``.


    * Run ``provision.yml``.

2. When the discovery mechanism is ``mapping``:

    * Update the existing mapping file by appending the new entry (without disrupting the older entries) or provide a new mapping file by pointing ``pxe_mapping_file_path`` in ``provision_config.yml`` to the new location.

    * Run ``provision.yml``.

3. When the discovery mechanism is ``snmpwalk``:

    * Run ``provision.yml`` once the switch has discovered the potential new node.

4. When the discovery mechanism is ``bmc``:

    * Run ``provision.yml`` once the node has joined the cluster using an IP that exists within the provided range.


Alternatively, if a new node is to be added with no change in configuration, run the following commands: ::

            cd provision
            ansible-playbook discovery_provision.yml


**Adding the new node to the cluster**
1. Get the IPs of the new nodes using the following commands: ::

    psql -U postgres
     \c omniadb
     select * from cluster.nodeinfo;

2. Insert the new IPs in the existing inventory file following the below example.

*Existing inventory*

::

    [manager]
    10.5.0.101

    [compute]
    10.5.0.102
    10.5.0.103

    [login]
    10.5.0.104

*Updated inventory with the new node information*

::

    [manager]
    10.5.0.101

    [compute]
    10.5.0.102
    10.5.0.103
    10.5.0.105
    10.5.0.106

    [login]
    10.5.0.104

In the above example, nodes 10.5.0.105 and 10.5.0.106 have been added to the cluster as compute nodes.

.. note::
    * Do not change the manager node in the existing inventory. Simply add the new node information in the compute group.
    * Do not change the parameters present in ``/input/omnia_config.yml`` except ``scheduler_type``.
    * Do not change the  parameters in ``/input/security_config.yml``.
    * New storage mount points can be added by updating ``input/storage_config.yml``. However, if the existing configuration is required to be replicated, do not remove the values in ``input/storage_config.yml``.

3. To install `security <BuildingClusters/Authentication.html>`_, `job scheduler <BuildingClusters/installscheduler.html>`_ and storage tools (`NFS <BuildingClusters/NFS.html>`_, `BeeGFS <BuildingClusters/BeeGFS.html>`_) on the node, run ``omnia.yml``: ::

    ansible-playbook omnia.yml -i inventory



