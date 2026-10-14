# Evidence, comparison, and verification workflows

Evidence-producing tools return the complete Evidence record directly in MCP
`structuredContent` and CLI JSON. Read `normalized_result` for operation data,
and cite `evidence_id` when another tool or your explanation needs a stable
reference. Preserve authority, limitations, coverage, and residual unknowns. If a result
is incomplete or paginated, continue only when the remaining data matters to
the task; do not fetch a bundle or resource merely to read a result already
returned inline. When complete `inspect_binary_layout` or
`analyze_javascript_application` Evidence is already retained, call
`inspect_analysis_view` for a summary, one section/symbol/module, or a stable
page instead of repeating the producer.

Completed `inspect_artifact` inventory also supports a summary and
`view: {kind: "inventory", collection: "occurrences", logical_paths: ["package.json", "main.js"]}`.
Omit `logical_paths` to page all available occurrences; `[]` selects none.
Other inventory collections are `nodes`, `edges` and
`integrity_contradictions`. Keep `source_complete` separate from page exhaustion:
a missing match in partial source Evidence does not establish absence. Use the
returned parent Evidence ID for subsequent views and export before closing the
session when the source must survive it.
When `tools/list` advertises `inspect_artifact.detail`, request `"summary"` to
retain its complete source and receive that view immediately. Without that
advertised choice, keep the existing complete call. CLI inspection returns
portable complete Evidence; save it before projecting a selected inline view.

Use `record_unknown` to track unresolved questions in the user's investigation
and name the authority or environment still required. Supply supporting and
contradicting evidence IDs. It updates the session registry directly.
Use `update_unknown` with the current revision; reread after a stale revision
instead of retrying blindly. Only qualifying observed evidence can verify a
resolution.

Use comparisons with complete, compatible page sets when claiming equivalence
or absence:

- `compare_artifacts` compares inventory pages by occurrence path, content,
  metadata, and graph relations.
- `compare_functions` compares explicit function Evidence, not fuzzy
  whole-binary matches.
- `compare_bundles` compares canonical bundle membership and unknown history.
- `find_changed_behavior` combines existing comparisons; static differences
  remain candidates, not causal proof.
- `build_call_path` needs explicit function dossiers from one artifact/provider;
  an incomplete frontier makes absence unknown.
- `correlate_static_and_runtime` uses explicit mappings; matching patterns are
  hypotheses, not causality.
- `verify_reconstruction` evaluates a finite typed specification. A pass covers
  only declared comparable claims, not global equivalence.

Process captures are opt-in behavioral evidence, not a security sandbox. V3
captures cannot be upgraded to V4; rerun the original scenario. Distinguish root
exit from descendant settlement and require freshness when the task needs it.
A timed-out target that must write a final report needs `finalization_ms`: REA
sends SIGTERM to the captured root, keeps observing, and sends SIGKILL once
only if the target has not exited by the end of the interval.
`exit.finalization.signals` lists each attempt with its delivery result; the
observed exit signal stays in `exit.signal`, `exit.code` is null for every
deadline exit, and the code of a finalizer that exited on its own is in
`exit.finalization.exit_code` (null on a signal exit or when no exit was
observed).

Use `inspect_analysis_view` with `view: {kind: "api-surface"}` on retained
`inspect_web_network_capture` HAR Evidence to group observed request lines by
method, origin and path template. Format matches are inferences, not handler
identity or schemas. Group pages cite parent record ordinals; consult record
coverage and exclusions before claiming completeness. No requests are replayed.
When the connected schema advertises `include_query_parameter_names`, select
it in the view for distinct observed names with original record ordinals. Query
values are omitted; the names establish neither required parameters nor a
complete server schema. Keep the original parent Evidence for exact URLs.

## Compare a working and failing case

Start with the requested outcome and the strongest existing successful and
failed observations. A static implementation is a candidate working case until
the relevant behavior has been observed. If runtime access is unavailable,
continue useful static analysis and leave runtime success explicitly unknown.

1. Separate stages before choosing the next experiment: transport connection,
   protocol acceptance, operation acknowledgement, application data, and the
   user's required coverage or freshness. Use the stages the target actually
   exposes. A connection log does not prove data delivery; a combined display
   can hide polling, cache, or another fallback source.
2. Record a small comparison table: exact artifact/library identity, environment,
   selected options, observed stage/result, capture window, and unmeasured
   differences. Preserve relevant non-sensitive values and provenance when
   available. Configured values and page properties are not captured wire
   values; do not reconstruct missing headers from them.
3. Distinguish user constraints and service access rules from investigator-chosen
   controls. Holding a value fixed improves a comparison; it does not prove the
   value is accepted or make it a permanent implementation requirement. Revisit
   a control when evidence implicates it, within the existing authorization.
   Compatibility testing does not authorize copying another client's identity,
   evading an access restriction, or cycling identities after refusals.
4. Choose a bounded experiment that discriminates between the remaining
   hypotheses. Where useful, hold the environment and real library constant
   before replacing a component. Name confounders such as concurrent clients,
   duplicate-session replacement, server state, timing, or incomplete capture.
   A second attempt with unchanged conditions is not a new explanation.
5. Verify a successful candidate in the intended client and through the user's
   actual outcome. Keep transport, subscription/operation, data attribution,
   coverage, and freshness claims separate. Stop redundant probing once that
   outcome is established; record remaining production or causal unknowns.

Report a working configuration separately from the exact cause of rejection.
One changed identifier that succeeds does not establish a prefix rule or a
specific denylist. A generic refusal code can represent several causes.
Replace stale handoff conclusions when new observations contradict them, and
retain enough evidence to explain why the conclusion changed.
