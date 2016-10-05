# sharestore
Simplistic Globally Distributed Multi-Master Storage Server


# Scribbled thoughts
* HTTP API based
* API endpoints for:
  * store
  * retrieve
  * check-replication
  * send-replication

* Features
  * Time-based checkpointing of data
  * Compaction of checkpoints once all nodes have the referenced data; place all data under the one checkpoint for new node bootstrapping
  * Identify closest peers for replication
  * Self-identify upload/download capacity and current available capacity
  * Steering for even bandwidth consumption
  * Weighting for bandwidth/latency per-node (to prefer the use of cheaper locations)
  * Allow for internal communication if present (configurable -- looks for LAN-based nodes to replicate with)
  * UUID based host identification
  * Store data via POST/PUT HTTP requests
  * Allow to secure the service simply with a standard web frontend (NGinX w/SSL etc)
  * Eventual consistancy replication
  * Basic conflict resolution
  * Deleted data marked for deletion - to be actioned in X days for time for failed nodes to replicate (or immediately if all configured nodes say OK?)
  * Full-mesh not required (host call-back to report unreachable hosts)
  * Admin server(s) - HA - manage active servers, supporting APIs for:
    * Register
    * De-register
    * List hosts
    * Node-to-node communication status to identify downed or disconnected units (and network segregation)

* Goals
  * Simplistic replication
  * Auto-peer-discovery (automated registration)
  * Globally distributed data
  * Multiple 'bucket' support per cluster for data isolation
  * Multi-master write-to-any architecture
  * Backend-less (No backing DB - status retained in status files and metadata?, no B-Trees; just simplistic file storage on disk -- can be expanded later)
  * Straight-forward searches (filename searches on disk, grep file contents)
