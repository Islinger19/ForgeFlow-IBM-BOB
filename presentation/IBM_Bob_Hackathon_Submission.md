# IBM Bob 2.0 Hackathon: submission text

Paste each block into the matching lablab.ai field. Anything in [square brackets] must be replaced with
real values from your bob_sessions/ exports before submitting, or the sentence deleted.

## Links

| Field | Value |
|-------|-------|
| Public code repository | https://github.com/Islinger19/ForgeFlow-IBM-BOB |
| Application URL | https://forgeflow-ecru.vercel.app |
| Demo application platform | Web (PWA), deployed on Vercel |
| Video demonstration | https://youtu.be/cjVYj87INMo |
| Slide presentation | `presentation/ForgeFlow_IBM_Bob_Hackathon.pdf` |
| IBM Bob session screenshots | `bob_sessions/<member>/` |

## Submission Title

ForgeFlow: Self-Healing Test, Repair & Deploy

## Short Description

ForgeFlow turns a web-app idea into a verified live URL. It writes tests from your acceptance criteria, fixes failures in a bounded, diff-aware repair loop, deploys to Vercel, re-tests the live site, and hands stuck cases to IBM Bob.

## Long Description

<!-- LONG-START -->
THE PROBLEM
AI app builders made generating a web app fast, but proving that it works is still manual. Developers write tests after the code, paste CI logs into a chat, retry fixes with no stopping rule, and click through the live site hoping nothing broke. Studies show the cost: two frontier models deployed their generated infrastructure successfully on the first attempt only 30.2% and 26.8% of the time; most of a repair loop's gain arrives in the first one to three iterations; and repeated AI self-refinement can make code less secure. An open-ended fix loop wastes budget and adds risk.

OUR SOLUTION
ForgeFlow is a human-in-the-loop Progressive Web App that carries a web-app idea, given as screenshots or a structured spec, through six stages: requirements, design, build, test and repair, deploy, and live validation. It targets the verify, debug and release workflow.
- Tests come from your acceptance criteria. Each criterion's ID travels into the generated test, its result, the repair context and the live-validation report.
- Failures go to a bounded, diff-aware repair loop. The agent sees only the failing tests, the sources they exercise, the git diff since the last green run and the criterion text. The loop stops at the first of four guards (regression, no progress, iteration cap, budget cap) and escalates with a plain-language summary of what it tried.
- Deployment is infrastructure-aware: the SPA and Node API go to Vercel, data to MongoDB Atlas, and the same suite re-runs against the live URL. Live failures re-enter the same bounded loop.
- Built for IBM Bob: the repo ships AGENTS.md and .bob/rules/, and our Continue in IBM Bob feature (in progress) exports an escalated workspace with a BOB_HANDOFF.md for IBM Bob IDE's Plan mode.

WHO IT'S FOR AND HOW THEY USE IT
Student and indie builders, agencies prototyping for clients, and teams adopting AI coding tools who need proof before they ship. In the browser, they describe the app or drop in screenshots, edit requirements, refine the design in one sentence, watch code and a live preview update in real time, follow each repair iteration, and deploy with one action. Any stage can be entered, skipped or revisited; only deploy needs a build, and validation a deploy.

WHAT MAKES IT DIFFERENT
Most builders treat generation as the finish line. ForgeFlow treats verification as the product: a repair loop designed to terminate, escalation as a normal outcome instead of an error, and tests re-run on the deployed URL. Pairing it with IBM Bob gives every hard case a real next step, with the developer in charge.

EFFICIENCY
Untrusted code runs only in per-project Docker sandboxes with no host network. Models are routed by role, so the expensive model runs only for code, tests and repair, and cost is tracked per project against a budget cap. ForgeFlow ships with 2,148 automated tests across 65 delivered phases, six CI gates, and a 10-app benchmark tracking first-pass versus post-repair pass rate, iterations and cost.
<!-- LONG-END -->

## IBM Bob Usage Statement

<!-- BOB-START -->
ForgeFlow's core pipeline, sandboxes and repair loop were built by our team before the event. We brought it to the hackathon because it is the kind of codebase Bob 2.0 is designed for: about 800 files across a Python control plane, a React PWA, Docker sandboxes and deploy adapters. Everything below was done in IBM Bob IDE during the hackathon. Each session's consumption-summary screenshot and exported task history is in bob_sessions/ in our repository.

1. Onboarding with full repository context. We ran /init to give Bob project context (our AGENTS.md and .bob/rules/ are in the repository), then used Ask mode to trace how a failing test becomes a repair attempt, from the test runner to the loop controller. Bob spawned [N] explore subagents in parallel to map the testing, agents and orchestrator packages, and returned the path with file references.

2. Code review. We ran /review on the repair-loop controller, the sandbox manager and the deploy adapters. The Bob Findings panel reported [N] issues; we confirmed [N] and fixed them with Bob in Code mode, with a test for each fix.

3. Planning from our own documents. In Plan mode, Bob read IMPLEMENTATION_PLAN.md and our loop-controller specs and produced the design for a new feature, Continue in IBM Bob. We saved it as plans/phase-66-bob-handoff.md, following the phase workflow we use for every feature.

4. Building the feature in Agent mode. Bob implemented it end to end: an endpoint that packages the generated app's workspace with AGENTS.md, .bob/rules/forgeflow-stack.md and a BOB_HANDOFF.md rendered from the loop's escalation payload (failing tests, acceptance criteria, patches tried, failing-count trail), and a Continue in IBM Bob button on the escalation panel. Parallel tool calls let Bob read the escalation model, the workspace service and the UI panel in a single turn.

5. Tests. A general subagent wrote [N] pytest and [N] Vitest cases for the handoff renderer, the endpoint and the button. They run in our CI.

How IBM Bob fits the product: ForgeFlow automates the bounded part of verify, repair and release, and IBM Bob is where a developer takes over when the loop stops. The handoff files are written for Bob to read, so a stuck case opens in Bob IDE with the failing tests, the patches already tried and the project's conventions loaded.

Our team used [N] Bobcoins across [N] sessions. We did not use watsonx.ai or watsonx Orchestrate in this submission.
<!-- BOB-END -->

## Categories

Pick the closest options in the dropdown: Developer Tools, DevOps / CI-CD, Testing & QA, AI Agents.

## Technologies Used

IBM Bob (required). Add IBM watsonx.ai only if you actually use it.
Then: React, TypeScript, Vite, Tailwind CSS, Python, FastAPI, MongoDB, Docker, Node.js, Express, Playwright, Vitest, Vercel.
