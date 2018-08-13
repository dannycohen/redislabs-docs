---
Title: Removing a Node
description: $description
weight: $weight
alwaysopen: false
---
There are various reasons why you may want to remove a node in Redis
Enterprise Software (RS):

-   You no longer need the extra capacity, meaning you wish to
    permanently remove the node.
-   You would like to replace a faulty node with a healthy node.
-   You would like to replace a healthy node with a different node.

The following section explains how each of these actions can be
achieved, as well as their impact and considerations.

**Make sure to read through these explanations thoroughly before taking
any action.**\

Permanently removing a node
---------------------------

Permanently removing a node means you are decreasing cluster capacity.
Before trying to remove a node, ensure that the cluster has enough
capacity for all resources without that node, otherwise you will not be
able to remove the node.

If there is not enough capacity in the cluster to facilitate removing
the node, you can either delete databases or add another node instead of
the one you would like to remove.

During the removal process, the cluster migrates all resources from the
node being removed to other nodes in the cluster. In order to ensure
database connectivity, and database high availability (when replication
is enabled), the cluster first creates replacement shards or endpoints
on one of the other nodes in the cluster, initiates failover as needed,
and only then removes the node.

If a cluster has only two nodes (which is not recommended for production
deployments) and some databases have replication enabled, you will not
be able to remove a node.

Replacing a faulty node
-----------------------

If the cluster has a faulty node that you would like to replace, you
only need to add a new node to the cluster. The cluster recognizes the
existence of a faulty node and automatically replaces the faulty node
with the new node.

For guidelines, refer to [Replacing a faulty
node](/redis-enterprise-documentation/cluster-administration/replacing-a-faulty-node).

Replacing a healthy node
------------------------

If you would like to replace a healthy node with a different node, you
must first add the new node to the cluster, migrate all the resources
from the node you would like to remove, and only then remove the node.

For further guidance, refer to [adding a new node to a
cluster](/redis-enterprise-documentation/administering/cluster-operations/adding-node/).

You can migrate resources by using the *rladmin* command-line interface
(CLI). For guidelines, refer to [*rladmin* command line interface
(CLI)](/redis-enterprise-documentation/references/cli-reference/rladmin/).

**Note**: The DNS records must be updated each time a node is added or
replaced. For additional details, refer to
[DNS](/redis-enterprise-documentation/administering/installing-upgrading/configuring/cluster-name-dns-connection-management/).

To remove a node:
-----------------

1.  Click **Remove** at the top of the **Node** page for the node to be
    removed.
2.  Approve the action.
3.  RS examines the node and the cluster and takes the actions required
    to remove the node.
4.  At any point, you can click the **Abort** button to stop the
    process. When aborted, the current internal action is completed, and
    then the process stops.
5.  Once the process finishes, the node will no longer be displayed in
    the UI.

You can choose to receive email alerts related to this process, as
described in [Managing cluster
alerts](/redis-enterprise-documentation/cluster-administration/viewing-and-defining-cluster-settings/managing-cluster-alerts).

**Note**: Once you remove a node, if you need to add it back to a
cluster, you must first
[uninstall](/redis-enterprise-documentation/administering/installing-upgrading/uninstalling/)
and
[reinstall](/redis-enterprise-documentation/administering/installing-upgrading/downloading-installing/)
the software on that node.