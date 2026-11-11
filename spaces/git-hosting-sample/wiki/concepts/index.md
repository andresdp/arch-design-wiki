# Design decisions (dimensions)

* [Client data transfer](/concepts/client-data-transfer.md) - What a developer's machine downloads to work on a repository.
* [Reference update coordination](/concepts/reference-update-coordination.md) - How concurrent updates to a repository's references are ordered and made atomic.
* [Replication for durability](/concepts/replication-for-durability.md) - How copies of a repository are kept so that a lost machine loses no data.
* [Serving reads](/concepts/serving-reads.md) - Where read traffic (fetches, clones, CI checkouts) is served from.
* [Source of truth for repository state](/concepts/source-of-truth-for-repository-state.md) - Where the authoritative copy of each repository's objects and references lives.
