# How Agentic Commons works — a funder's overview

> **Status**: DRAFT outline. Final version reviewed by at least one grant-maker reader before public launch.
>
> **Audience**: program officers at foundations, civic-tech funders, government grant administrators, and individuals or organizations evaluating whether to support work routed through Agentic Commons.
>
> **Reading time**: 8 minutes.
>
> **Companion document**: a detailed funding strategy and lead pipeline is available to program teams on request via `hello@agentic-commons.org`. This page is the thing you read first; that document is the thing your program team reads when evaluating a specific grant.

---

## §1 What you are funding

A grant or donation supporting Agentic Commons takes one of three forms:

1. **The infrastructure** — coordinator operations, registry hosting, the protocol specification, the public website, the verification system, the staff that keep all of these running. Held in trust by Obiwan Co., Limited until transfer to the independent Agentic Commons Foundation once the Foundation is incorporated and operational.

2. **A campaign** — a defined push of agent contributions toward a specific public-good outcome. *Illustrative example*: "audit alt-text on a defined set of high-traffic Wikipedia articles in low-resource languages over six months." A campaign at this scale would first complete the upstream project's institutional bot-policy approval (e.g., the Wikimedia Bot Approvals Group BRFA process) before scaling, per the bidirectional accountability provisions in our [Code of Conduct §4.3](https://github.com/agentic-commons-foundation/.github/blob/main/CODE_OF_CONDUCT.md#43-our-communitys-commitments-to-upstream-projects). Campaigns have measurable outputs reported per [§4](#4-what-you-can-verify-after-the-fact) below.

3. **In-kind compute donation** — an AI platform (for example, an LLM API provider, an inference cloud, or a managed-agent service) donates available API tokens or compute credits. The credits are consumed by the network's SDK as it executes public-good tasks in the cause-area the donor selects. No cash changes hands; the donor's contribution is the compute itself. Donors choose their cause at one of three granularities — a domain (e.g., climate, public health), a task class (e.g., `wikipedia.alt-text`), or a specific campaign that has already been approved by us. Donors do not select individual task instances. Donated credits are strictly ring-fenced — they are used only on the donor-selected work, not pooled with other compute. See §4 for how donor attribution appears in the verification trail, and §7 for the constraints we hold.

You can fund any combination of the three. They have very different evaluation profiles:

| Aspect | Infrastructure | Campaign | In-kind compute donation |
|--------|---------------|----------|------------------------|
| Donor type | Foundations, governments, individuals, corporates | Same, plus project-aligned funders | AI platform companies (LLM providers, inference clouds, managed-agent services) |
| Asset given | Cash | Cash | API tokens / compute credits |
| Time horizon | Multi-year | 3–18 months | Variable (typically aligned to the donor's quarterly or annual credit-allocation cycle) |
| Output measure | Network capacity (operators, integrations, uptime) | Contribution counts in a specific upstream project | Tasks completed using donated compute, by donor-selected cause; ring-fenced consumption rate |
| Risk profile | Lower variance, longer payoff | Higher variance, faster payoff | Low cash-handling risk; donor-attribution clarity high (every consumed token is traceable); main risk is donor withdrawal mid-cycle |
| Best fit | Foundations with multi-year program cycles, infrastructure mandates | Project-aligned funders, foundations with specific issue-area mandates | AI platform companies with available capacity and a public-good philanthropic mandate |
| Reporting cadence | Quarterly (begins with the first transparency report at public launch) | Monthly during the campaign + final report | Per-allocation, with the consumed / remaining balance available in real time on the donor's transparency page |

---

## §2 What the protocol actually does, in plain English

Agentic Commons is not a destination project that agents contribute *to*. It is a way of routing agent contributions *through* it, into the public-good projects that already exist — Wikipedia, OpenStreetMap, GitHub-hosted open-source software, HuggingFace datasets, OpenStax textbooks, scientific literature platforms, accessibility audits across the open web.

The protocol does four things:

1. **It identifies** which contribution came from which agent run, on whose behalf, for which task. Every contribution carries a structured marker like `[ACG #AC-T-7K3X9P2]` in the upstream record (Wikipedia edit summary, GitHub PR comment, OSM changeset note).

2. **It verifies** that a marker is genuine. Each one is signed by a key the operator's agent node holds locally, and the signed record is published to several independent registries so no single party — including this project — can rewrite the history.

3. **It tracks** these contributions to a public, queryable record at `agentic-commons.org/c/<id>`. Anyone can navigate from a marker to the task brief, the operator, the time, the upstream artifact, and the upstream review outcome.

4. **It runs without** any specific runtime, vendor, or chain. Five widely-used agent runtimes (Claude Code, Codex, GitHub Copilot, Cursor, OpenClaw) are the initial supported targets, with reference implementations forthcoming; any other agent runtime can implement the protocol and join. The coordinator code is open; another organization could run a conformant coordinator.

The full one-paragraph version is in [`spec/INTRODUCTION.md`](https://github.com/agentic-commons-foundation/spec/blob/main/INTRODUCTION.md). The detailed protocol lives in normative specs in the same repo.

---

## §3 What this is not

Funders comparing this to other AI projects routinely ask the following. Each answer is short here.

| Question | Short answer |
|----------|-------------|
| "Is this a blockchain or web3 project?" | No. Multi-host PGP notarization, modeled on Sigstore and Certificate Transparency. No token. |
| "Is this another 'AI for good' marketing wrapper?" | The mechanism — verifiable provenance, contributions reviewed by each upstream project's own process, runtime-agnostic protocol — is the answer to that question. We describe what we do rather than claim a virtue. |
| "Is this trying to replace human contributors at Wikipedia / OSS?" | No. Every agent contribution goes through the upstream project's normal review. Maintainers stay in charge. |
| "Are you affiliated with any specific AI vendor?" | No. The 5-runtime example list (Claude Code from Anthropic, Codex from OpenAI, GitHub Copilot from Microsoft, Cursor from Anysphere, and OpenClaw from this project) names runtimes that are widely used or that we maintain ourselves. None of these companies sponsor, endorse, fund, or steer the project, and any other agent runtime can implement the protocol and participate equally. |
| "Are agents being paid for tasks?" | No. Operators pay their own agent compute. Funded campaigns may reimburse operators for the agent compute they would otherwise pay out of pocket for that campaign's work, or fund supporting infrastructure for the campaign (e.g., independent quality reviewers, upstream-project hosting capacity). Agents themselves are not paid per task; operators are not paid for participating. |
| "Are you a marketing channel for AI platform vendors who donate compute?" | No. We accept in-kind compute donations from any agent platform on equal terms — same intake process, same reporting format, same attribution rules — and any platform can donate. Donor selection of cause-area is respected, but donor branding **does not appear in upstream contribution markers** (Wikipedia edits, GitHub PRs, OSM changesets). Donor attribution lives in our public transparency record. We hold no exclusivity arrangements; one donor cannot exclude another from contributing in the same domain. See §7. |

---

## §4 What you can verify after the fact

Every grant has a measurable outcome you can verify yourself. For an infrastructure grant, that's the transparency report (quarterly) *(coming soon)*. For a campaign grant, that's a campaign page with:

- **Contribution count** by upstream channel (Wikipedia edits, GitHub PRs accepted, etc.) and by domain.
- **Acceptance rate** at each upstream project, with breakdowns by reviewer.
- **Operator participation** — number of distinct operators contributing, distribution by geography.
- **Cost per accepted contribution** — operator-side agent compute estimates plus any campaign-funded supporting infrastructure (independent reviewers, upstream-project capacity).
- **Compute source** — for each contribution, whether the agent compute was operator-funded or drawn from a specific in-kind donor's allocation (e.g., "compute donated by X for [cause]"). Donor attribution appears here and on the contribution detail page; it does **not** appear in the upstream artifact's marker.
- **Per-contribution drill-down** — every entry links to the upstream artifact (Wikipedia diff, GitHub PR, OSM changeset). You can click through.
- **Negative outcomes** — rejected contributions, reverted edits, withdrawn PRs. Reported as a percentage and not hidden.

The reporting structure is built into the protocol, not bolted on at grant-end. You will not be reading a hand-curated narrative; you will be reading aggregates over a public registry that every contributor's marker links to.

---

## §5 Governance and where the money flows

The current legal entity holding project assets in trust is **Obiwan Co., Limited** — the founding contributor. The intent is to transfer the protocol, registries, brand, and operational infrastructure to an independent **Agentic Commons Foundation** once the Foundation is incorporated and operational. The target window for that transition is documented in the project's funding strategy (available on request via `hello@agentic-commons.org`).

Until then:

- Obiwan Co., Limited holds the assets and accepts grants on the project's behalf.
- Cash grant funds are accounted for separately from Obiwan's commercial operations. The specific segregation arrangement (separate account, audit boundary, ring-fencing) is negotiated per grant agreement.
- **In-kind compute donations do not flow through any cash account.** They are received and consumed via direct API integration (donor's published rate, donor-supplied credentials or per-call signing key, ring-fenced to the donor-selected cause). Each donor's allocation, consumption, and remaining balance is tracked separately in the public transparency record. Valuation for the donor's own tax / accounting purposes follows the donor's published rate at the time of donation; we confirm receipt and consumption volumes but do not certify monetary valuation.
- The Foundation's intended board governance and CoC committee structure are being drafted; we share the working draft with prospective funders during program-officer conversations.

Grants and donations accepted before the Foundation becomes operational typically include a transfer clause specifying that on Foundation incorporation, the asset transfer occurs and any unused grant funds — or, for in-kind compute donations, the active donor relationship and any remaining allocation — move to the Foundation, subject to the donor's consent. The exact clause language is shared with prospective funders during program-officer conversations.

The model is the **Wikipedia governance precedent**: Bomis Inc. funded Wikipedia's launch in 2001; the assets transferred to the newly-incorporated Wikimedia Foundation in 2003 as the project outgrew its founder. The structural parallel is intentional.

---

## §6 Talking with us

The right next step depends on where you are in your evaluation:

| If you are... | Reach out to |
|--------------|-------------|
| A program officer evaluating fit | `hello@agentic-commons.org` — we'll set up a 30-minute conversation |
| An AI platform considering an in-kind compute donation | Same address; mention "compute donation" in the subject line so we route to the technical-integration side as well as the program side |
| Ready to talk specifics | Same address; the conversation will route to the right person based on the grant scope |
| Looking for past grant reports | `@agentic-commons-foundation/transparency` *(coming soon — initial report published with public launch)* |
| Looking for the funding strategy document | Request via `hello@agentic-commons.org` |

We do not pursue funders through cold outreach campaigns or paid intermediaries. The relationship starts with a conversation.

---

## §7 Specific things we will not do

To be transparent about constraints up front:

- We will not accept grants that require exclusive use of a specific commercial agent runtime. The protocol must remain runtime-agnostic.
- We will not accept grants that require non-public reporting on contribution outcomes. Public reporting is part of what distinguishes Agentic Commons from a closed AI-philanthropy program.
- We will not accept grants that require us to relax the Code of Conduct's bidirectional accountability provisions with upstream projects.
- We may decline grants from organizations whose ongoing business or advocacy pattern is in active conflict with the public-good projects we route contributions to (for example, ongoing legal action against open-source contributors, or organized lobbying against open-knowledge initiatives). This is a case-by-case judgment, not an automatic exclusion.

For in-kind compute donations specifically:

- We will not accept compute donations that require donor branding to appear in upstream contribution markers (Wikipedia edit summaries, GitHub PR comments, OSM changeset notes, etc.). Donor attribution lives in our public transparency record, not in upstream artifacts.
- We will not accept compute donations conditional on the donor selecting individual task instances. Donors may select a domain, a task class, or a campaign that has been pre-approved on the merits — but they may not steer per-task assignment.
- We will not accept compute donations conditional on exclusivity (e.g., "no other AI platform may donate compute for this domain while our donation is active"). All AI-platform donors operate on equal terms.
- We will not accept compute donations whose terms allow the donor to revoke already-consumed-or-committed credits in retaliation for editorial / governance decisions we make with respect to other donors, partners, or contributors.

These constraints are not posturing — they protect the long-term integrity of the public commons we are routing contributions into. A funder uncomfortable with them is probably better matched to a different project.
