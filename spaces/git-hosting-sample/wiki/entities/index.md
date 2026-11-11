# Alternatives and outcomes (values)

* [Blobs plus a relational reference database](/entities/blobs-plus-a-relational-reference-database.md) - Pack data in blob storage and references in a relational database, two stores to keep consistent.
* [Block-level filesystem replication](/entities/block-level-filesystem-replication.md) - The filesystem under Git is replicated block by block between paired machines.
* [Cache servers near the clients](/entities/cache-servers-near-the-clients.md) - Cache servers in each office or region serve objects and forward misses to the origin.
* [Compare-and-swap on the log](/entities/compare-and-swap-on-the-log.md) - Writers append to the log with a compare-and-swap, without a consensus protocol.
* [Durability delegated to object storage](/entities/durability-delegated-to-object-storage.md) - The object store holding the log keeps the data durable; servers hold no unique data.
* [Full clone over the Git protocol](/entities/full-clone-over-the-git-protocol.md) - The client fetches the whole history with standard Git.
* [Nearest up-to-date replica](/entities/nearest-up-to-date-replica.md) - Reads go to the closest replica that has the latest state.
* [Objects in a distributed hash table](/entities/objects-in-a-distributed-hash-table.md) - Git objects are stored individually in a distributed key-value store.
* [One server serializes the updates](/entities/one-server-serializes-the-updates.md) - The single file server holding the repository applies updates one at a time.
* [Partial clone with sparse checkout](/entities/partial-clone-with-sparse-checkout.md) - The client fetches only the history and files it needs, with standard Git features.
* [Repository files on server disks](/entities/repository-files-on-server-disks.md) - Plain Git repositories on the servers' local disks are the authoritative state.
* [Single copy on a file server](/entities/single-copy-on-a-file-server.md) - One file server holds each repository, reached by RPC, with no replica.
* [Stateless servers with a local disk cache](/entities/stateless-servers-with-a-local-disk-cache.md) - Any server can serve any repository, rebuilding a warm copy on its local disk from the log.
* [Three Git replicas with majority writes](/entities/three-git-replicas-with-majority-writes.md) - Each repository has three plain Git replicas; a write succeeds once a majority has it.
* [Three-phase commit across replicas](/entities/three-phase-commit-across-replicas.md) - Reference updates run as a transaction that all replicas vote on.
* [Virtualized filesystem with on-demand objects](/entities/virtualized-filesystem-with-on-demand-objects.md) - A virtual filesystem shows every file and downloads objects only when a file is opened.
* [Write-ahead log in object storage](/entities/write-ahead-log-in-object-storage.md) - An append-only log in object storage is the authority; repositories on disk are derived from it.
