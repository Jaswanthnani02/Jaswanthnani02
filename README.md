# Jaswanth Gaddam

I build data platforms that make messy operational reality answerable.

Most of my production work is in a private repository, so what is here is the part that
travels: the architecture, the decisions and the failures, written up so they are useful to
someone who will never see the code.

---

## Start here

**[client-intelligence-platform](https://github.com/Jaswanthnani02/client-intelligence-platform)** — architecture case study

A platform that continuously reconciles four disconnected operational systems into one queryable
model and exposes it to an LLM as a set of authorized tools. Five decision records, each with the
tradeoff and what I would reconsider. Five production failures and what each one changed.

The decision I would defend hardest: deleting a working, well-liked feature because a value stored
apart from its inputs is a cache with no invalidation strategy. Scores are now composed at read
time, where the inputs are visible next to the result.

---

## Also here

**[doc-link-check](https://github.com/Jaswanthnani02/doc-link-check)** — a tool that came out of the above

Verifies that every relative link in a project's Markdown resolves. One file, no dependencies, no
network. It exists because reorganizing a documentation tree quietly invalidated a dozen paths
cited in source comments, where no test and no compiler knows a comment is a reference.

Relative links only, on purpose. External URL checking needs the network, gets rate-limited, and
produces false failures until people ignore the results.

**[mcp-rbac-demo](https://github.com/Jaswanthnani02/mcp-rbac-demo)** — authorization for LLM tool servers

A tool server with two authentication paths and three permission tiers, against mock data. The
runnable version of a pattern I describe in [decision 0005](https://github.com/Jaswanthnani02/client-intelligence-platform/blob/main/docs/decisions/0005-per-call-authorization.md)
of the case study: authorize every call rather than every session, on both what a caller may do
and whose data they may see.

**[ticket-dispatcher-demo](https://github.com/Jaswanthnani02/ticket-dispatcher-demo)** — assignment under load

Round-robin and weighted-load ticket assignment against a mock PSA API. Fake tickets and
technicians throughout.

---

## What I care about

**Failures that are silent.** Four of the five production incidents I have written up produced no
error at all — the system kept reporting success while doing less than it should. That changed how
I monitor things more than any individual fix: absence and staleness are better signals than
errors, because a job that does not run cannot report that it failed.

**Invariants that execute.** A constraint in a comment is a hope. A constraint with a test behind
it is a guarantee. The rules that broke in production were, without exception, the ones documented
rather than asserted.

**Choosing the failure direction.** A permission that is forgotten should produce a tool nobody
can call, not one everybody can call. Both are bugs; only one is discovered by an audit.

---

## Elsewhere

Currently building at a managed service provider — ingestion pipelines, a read-only query layer
over them, and the authorization model that lets an LLM touch client data safely.

Happy to talk about any of the above.
