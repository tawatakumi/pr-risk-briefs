# PVRB-003: Node.js PR #64311

## Purpose
This brief organizes possible review focus areas for a public pull request.

It is not an official review and is not affiliated with the target project.

## PR
Repository: nodejs/node

PR: #64311

PR URL: https://github.com/nodejs/node/pull/64311

PR Type: Bug fix / HTTP / perf_hooks / Observability

## PR Summary
This PR appears to fix how HTTP client request URLs are reported in `perf_hooks` performance entry details.

The review focus is not whether the HTTP request succeeds, but whether the observed URL remains faithful for observability consumers.

## Must-Review Changes
- How `detail.req.url` is built for HTTP client performance entries.
- Whether non-default ports are preserved.
- Whether IPv6 authorities keep the expected bracket form.
- Whether proxy absolute-form request paths are reported without duplicating protocol or authority.
- Whether captured connection authority matches what `perf_hooks` users would expect to observe.

## Potentially Missed Risks
- A syntactically valid URL may still be semantically misleading if it drops a port.
- Proxy paths that are already absolute-form may be accidentally combined with protocol and authority again.
- IPv6 host formatting may regress if authority handling differs from Host header generation.
- Observability tools may group, filter, or alert on the wrong endpoint if `detail.req.url` is not faithful.
- Tests may cover normal requests while missing proxied request paths, or the reverse.

## Impact Areas
- HTTP client `perf_hooks` performance entries.
- Monitoring, tracing, and diagnostics tools that read `detail.req.url`.
- Debugging workflows for requests through local ports, proxies, or IPv6 hosts.
- User trust in observed request metadata.

## Test Focus
- HTTP requests with non-default ports.
- HTTP requests through a proxy where the request path is absolute-form.
- IPv6 host and port combinations.
- Comparison between captured authority and the generated Host header behavior.
- Regression checks for both normal and proxied requests.

## Docs / README Update Needed
Probably no.

This appears to correct reported metadata rather than introduce a new user-facing API.

## Questions for Reviewer
- Does the new authority source preserve all expected port and IPv6 bracket cases?
- Is absolute-form proxy handling tested separately from normal path handling?
- Could any consumer depend on the previous malformed value?
- Are the tests close enough to the `perf_hooks` consumer surface rather than only the HTTP request path?
- Do normal and proxied requests now produce faithful but distinct observed URLs?

## Existing Review Coverage
Existing review coverage appears meaningful.

The target PR has approval and public discussion around CI and the intended fix. This brief is intended as a concise focus aid, not a claim that review was insufficient.

## Noise Check
Low.

The risk is narrow, observable from the public PR and issue, and tied to specific URL fidelity cases.

## Decision
Published Candidate
