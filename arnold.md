For any targeted performance enhancement run, Blitzy MUST commit a reproducible benchmark test covering each modified code path before applying the change and MUST re-execute the same benchmark after modification, persisting both result sets to benchmarks/results/<task-id>/{pre,post}.json. 

Each benchmark MUST report at minimum: operation name, sample count (≥30), mean, median, p95, and standard deviation, measured under identical hardware, dataset, and configuration conditions across both runs. If a modified code path has no pre-change equivalent (newly introduced code), the pre-result entry MUST record "baseline": "none" with the reason, rather than being omitted. Any modified code path whose post-run mean and p95 are not both strictly lower than its pre-run mean and p95 (excluding entries with "baseline": "none") MUST be reverted to its pre-change state before the pull request is opened, and the reverted paths MUST be listed in benchmarks/results/<task-id>/aborted.json. 

Verification: pre.json and post.json both exist with one entry per modified code path containing all required statistical fields; for every entry where post mean or p95 is greater than or equal to pre, the corresponding source change is absent from the PR diff and the path is recorded in aborted.json. 

Scope: applies exclusively to targeted performance enhancement runs — work items with an explicit performance objective — and the methods changed during code generation or any dependent routes invoked by them. Does not apply to general code changes, bug fixes, or refactors; for general code modification benchmarking, see cross-fit.md.



