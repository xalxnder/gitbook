# Longhorn

#### 🧱 1.&#x20;

#### Components

* Longhorn Manager (Pod): Runs on each node, controls volume lifecycle and operations.
* Longhorn Engine (Pod per volume): Manages the data path and handles read/write operations.
* Longhorn Replica (Pod per volume per replica): Stores actual volume data. Each replica runs on a separate node.
* UI / CLI / CRDs: Interfaces to interact with Longhorn.

***

#### 🔄 2.&#x20;

#### Volume Replication

* When a volume is created, Longhorn:
  * Spawns a Longhorn engine pod on the node where the workload runs.
  * Creates multiple replicas (as specified) across different nodes.
* The engine synchronously writes data to all replicas.
* If a replica/node fails, the volume stays available as long as the quorum is intact (majority of replicas).
