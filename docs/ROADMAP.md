# Orion + Mira --- Project Roadmap and Delivery Plan

**Plan version:** 1.0\
**Project start:** Monday, 16 November 2026\
**Target release:** Sunday, 3 January 2027\
**Duration:** 7 weeks\
**Working capacity:** 2--3 hours per working day\
**Primary outcome:** A usable Mira v0.1 companion integrated into the
existing Orion desktop browser.

> This is a delivery plan, not a promise that every task will take
> exactly the time estimated. If a technical dependency fails or a task
> needs more time, move the affected task forward and update the dates.
> Do not skip verification to preserve the calendar.

------------------------------------------------------------------------

## 1. Product goal: Mira v0.1

By the end of this plan, Mira should:

1.  Appear on Orion's home screen as an animated 2D character.
2.  Have a consistent idle state and a small set of expressions.
3.  Welcome the user and display conversation text.
4.  Generate spoken responses through a replaceable text-to-speech
    provider.
5.  Accept spoken input through speech recognition.
6.  Use an AI model to understand requests and formulate responses.
7.  Perform a small, explicitly permitted set of browser actions.
8.  Keep basic settings and conversation history locally where
    practical.
9.  Fail safely when an API, model, microphone, or browser action is
    unavailable.

**Not part of v0.1:** a complete 2D town, free-roaming character
movement, voice cloning, complex long-term memory, autonomous
unrestricted computer control, multiple agents, or a fully offline AI
stack. These can be considered for v0.2 or later.

## 2. Fixed initial technology choices

  -----------------------------------------------------------------------
  Area                    Initial choice          Decision
  ----------------------- ----------------------- -----------------------
  Desktop shell           Existing Orion /        Keep the existing app;
                          Electron                inspect before changing

  Application language    TypeScript              Use consistently where
                                                  practical

  Character rendering     Live2D Cubism Web SDK   First choice for Mira's
                                                  anime character

  Home-screen UI          Existing UI stack + CSS Keep the first
                                                  interface simple

  Advanced scene          Rive or PixiJS          Deferred until a
  animation                                       concrete need exists

  AI access               OpenRouter API          Provider/model must
                                                  remain replaceable

  First AI candidate      LFM3-1.7B               Benchmark; do not
                                                  assume it wins

  Speech generation       HeyGen Voice Turbo, if  Experimental provider;
                          accessible and suitable keep replaceable

  Speech recognition      Whisper-compatible      Confirm runtime and
                          implementation          hardware fit before
                                                  committing

  Local settings/history  SQLite, if needed by    Keep data local where
                          the existing app        practical

  Browser actions         Orion-owned,            No unrestricted model
                          allow-listed functions  access to Electron or
                                                  the OS
  -----------------------------------------------------------------------

### Technology and asset gates

Before buying or integrating a Live2D model, verify: - It includes
runtime-ready files compatible with the intended SDK. - Its licence
permits the intended personal desktop use. - Whether the editable source
project is included is clearly stated. - The model can be tested in a
small standalone page before integration.

Before relying on a hosted AI or voice service, verify: - Current
availability, pricing, rate limits, and provider terms. - Data retention
and whether prompts or audio may be used for training. - Whether the
free tier is temporary. - API behaviour, latency, and error handling.

Do not commit API keys, private voice samples, or licensed model assets
to a public Git repository. Use environment variables or a local secrets
file excluded by `.gitignore`.

## 3. Weekly milestones

  --------------------------------------------------------------------------------------
  Milestone         Dates             Outcome           GitHub milestone
  ----------------- ----------------- ----------------- --------------------------------
  M1 --- Foundation Nov 16--22        Existing Orion    `M1 Foundation & Character`
  and character                       documented;       
  proof                               Live2D candidate  
                                      tested and        
                                      selected          

  M2 --- Character  Nov 23--29        Mira loads and    `M2 Character Integration`
  integration                         animates inside   
                                      Orion             

  M3 --- Mira home  Nov 30--Dec 6     Home screen and   `M3 Home Experience`
  experience                          companion states  
                                      work              

  M4 --- Voice      Dec 7--13         Mira speaks using `M4 Voice`
                                      a selected        
                                      provider/voice    

  M5 --- AI brain   Dec 14--20        Text conversation `M5 AI Brain`
  and personality                     works through a   
                                      replaceable model 
                                      interface         

  M6 --- Listening  Dec 21--27        Basic speech      `M6 Listening & Browser Tools`
  and browser                         input and safe    
  actions                             browser tools     
                                      work              

  M7 ---            Dec 28--Jan 3     End-to-end        `M7 v0.1 Release`
  Integration and                     testing and Mira  
  release                             v0.1 release      
  --------------------------------------------------------------------------------------

**Working rhythm:** Monday--Friday are planned build days. Saturday is a
planned buffer/test/documentation day. Sunday is a rest day or optional
catch-up; it is not required for the baseline plan. Aim for 2--3 hours
per session.

------------------------------------------------------------------------

# 4. Day-by-day execution plan

## Week 1 --- Foundation and character proof

**Monday, 16 November -- Sunday, 22 November 2026**

### Monday, 16 Nov --- Inspect Orion and define the baseline

-   Open the current Orion project and run it without making feature
    changes.
-   Record the framework, Electron version, renderer structure, build
    commands, and current working features.
-   Identify where the home screen and main window are implemented.
-   Record existing bugs or fragile areas that must not be disturbed.

**Deliverable:** `docs/ORION_BASELINE.md`\
**Acceptance check:** Orion still runs as before; the baseline document
identifies the relevant entry points and commands.

### Tuesday, 17 Nov --- Create the Mira project workspace

-   Create or confirm the Git repository and default branch.
-   Create a feature branch: `feature/mira-foundation`.
-   Add the initial `docs/` structure and `.gitignore` checks.
-   Decide whether Mira lives inside the existing Orion repository or in
    a separate repository. Prefer the existing Orion repository if Mira
    is tightly coupled to Orion.

**Deliverable:** repository structure and initial commit.\
**Acceptance check:** clean clone/install instructions are documented;
no secrets or restricted assets are committed.

### Wednesday, 18 Nov --- Learn and prove the Live2D runtime

-   Read the Live2D Cubism Web SDK setup requirements.
-   Create a tiny isolated test page or experiment.
-   Load a known sample model supplied for SDK testing.
-   Confirm rendering works in the development environment.

**Deliverable:** `experiments/live2d-lab/` with a working sample.\
**Acceptance check:** sample model renders and the setup steps are
documented.

### Thursday, 19 Nov --- Research candidate Mira models

-   Shortlist up to three models from legitimate marketplaces or
    creators.
-   For each, record price, runtime files included, licence, permitted
    use, and whether source files are included.
-   Do not purchase based on preview images alone.

**Deliverable:** `docs/CHARACTER_SHORTLIST.md`.\
**Acceptance check:** at least one technically plausible candidate has
complete licence and file information; otherwise record the blocker and
continue with a sample model.

### Friday, 20 Nov --- Test the selected candidate

-   Obtain the selected model only if the licence and contents are
    clear.
-   Load it in the isolated Live2D test.
-   Check texture quality, scaling, expressions/motions supplied, and
    performance.
-   If purchase or licence information is unclear, do not buy yet; use a
    sample model and keep the selection open.

**Deliverable:** tested candidate or documented reason for deferring
purchase.\
**Acceptance check:** a model loads successfully, or a specific blocker
and next action are recorded.

### Saturday, 21 Nov --- Week 1 verification and upload

-   Re-run the sample from a clean start.
-   Fix setup/documentation issues.
-   Update `docs/PROGRESS.md` and close only completed GitHub issues.
-   Push the week's tested work.

**Deliverable:** Week 1 review and pushed commits.\
**Acceptance check:** another developer could follow the notes to
reproduce the Live2D proof.

### Sunday, 22 Nov --- Rest / optional buffer

No required task. Use only if a Week 1 task slipped.

**Week 1 exit gate:** Orion baseline documented, repository organised,
and Live2D rendering proven in isolation. A paid character is not
mandatory if licensing or compatibility is uncertain.

------------------------------------------------------------------------

## Week 2 --- Character integration

**Monday, 23 November -- Sunday, 29 November 2026**

### Monday, 23 Nov --- Plan the integration boundary

-   Identify the renderer component that will host Mira.
-   Define a small character interface: load, resize, set expression,
    play motion, and dispose.
-   Keep Live2D implementation behind that interface.

**Deliverable:** `docs/CHARACTER_INTEGRATION.md` and interface
skeleton.\
**Acceptance check:** the integration boundary is clear and does not
require broad changes to Orion.

### Tuesday, 24 Nov --- Load Mira in the Orion renderer

-   Add the Live2D runtime using the verified setup.
-   Load the selected/test model from the intended local asset location.
-   Handle loading and failure states.

**Deliverable:** Mira renders in a development build of Orion.\
**Acceptance check:** character appears reliably after restarting the
app.

### Wednesday, 25 Nov --- Sizing and layout

-   Make the character scale correctly at supported window sizes.
-   Avoid covering essential browser controls.
-   Check high-DPI and ordinary display scaling.

**Deliverable:** responsive character placement.\
**Acceptance check:** resizing the window does not crop or distort Mira
unexpectedly.

### Thursday, 26 Nov --- Idle animation and expressions

-   Add an idle motion and blinking if supplied by the model.
-   Add a small expression set, such as neutral, happy, thinking, and
    listening, only where supported by the model.
-   Define sensible fallbacks if an expression is unavailable.

**Deliverable:** basic expression controller.\
**Acceptance check:** each supported state can be triggered without
errors.

### Friday, 27 Nov --- Lifecycle and performance

-   Ensure the renderer releases resources when the view is closed or
    reloaded.
-   Check CPU/GPU use and memory during a short session.
-   Verify no duplicate animation loops are created.

**Deliverable:** stable character lifecycle.\
**Acceptance check:** repeated navigation/reload does not create visible
duplicate rendering or steadily growing resource use.

### Saturday, 28 Nov --- Week 2 test and upload

-   Test startup, resize, idle, expressions, and reload.
-   Fix high-priority bugs.
-   Update screenshots or a short demo recording if useful.
-   Push tested work and update progress.

**Deliverable:** integrated character demo.\
**Acceptance check:** Mira appears and animates reliably in Orion.

### Sunday, 29 Nov --- Rest / optional buffer

**Week 2 exit gate:** Mira loads inside Orion, resizes correctly, and
has at least one working idle state.

------------------------------------------------------------------------

## Week 3 --- Mira home experience

**Monday, 30 November -- Sunday, 6 December 2026**

### Monday, 30 Nov --- Define the home-screen layout

-   Sketch the main home screen and Mira's placement.
-   Identify the essential controls: conversation input, microphone
    control placeholder, settings, and status.
-   Keep the screen focused; avoid building a large virtual world.

**Deliverable:** home-screen wireframe or design notes.\
**Acceptance check:** layout and primary interactions are defined before
implementation.

### Tuesday, 1 Dec --- Build the home-screen shell

-   Implement the home screen using Orion's existing UI framework.
-   Add Mira's character area and basic layout.
-   Keep browser navigation and essential controls accessible.

**Deliverable:** first home-screen implementation.\
**Acceptance check:** home screen loads without breaking existing
browser navigation.

### Wednesday, 2 Dec --- Define companion states

-   Implement explicit states: `idle`, `listening`, `thinking`,
    `speaking`, and `error`.
-   Show a clear visual indicator for the current state.
-   Connect state changes to character expressions where available.

**Deliverable:** companion state controller.\
**Acceptance check:** states can be changed in a test harness and the UI
reflects them.

### Thursday, 3 Dec --- Welcome and text interaction

-   Add a welcome message.
-   Add a text input and submit action.
-   Use a temporary local/mock response; AI integration comes later.
-   Prevent repeated submission while a request is processing.

**Deliverable:** working text interaction shell.\
**Acceptance check:** user can submit text and see a mock response.

### Friday, 4 Dec --- Polish and accessibility

-   Improve spacing, typography, focus states, and keyboard navigation.
-   Add loading and error visuals.
-   Check window resizing and contrast.

**Deliverable:** usable home-screen prototype.\
**Acceptance check:** the interface remains usable at supported window
sizes.

### Saturday, 5 Dec --- Week 3 review and upload

-   Test all companion states and text interaction.
-   Fix issues and push the week's work.
-   Record what is still mocked and what is real.

**Deliverable:** home-screen demo and progress update.\
**Acceptance check:** the interface works without requiring an AI or
voice provider.

### Sunday, 6 Dec --- Rest / optional buffer

**Week 3 exit gate:** Mira has a functional home screen and visible
companion states.

------------------------------------------------------------------------

## Week 4 --- Voice generation

**Monday, 7 December -- Sunday, 13 December 2026**

### Monday, 7 Dec --- Build the Voice Lab

-   Create a standalone experiment that accepts text and plays generated
    audio.
-   Define a provider-neutral interface such as
    `synthesize(text, voiceConfig)`.
-   Keep API credentials outside the repository.

**Deliverable:** `experiments/voice-lab/`.\
**Acceptance check:** the lab can call a configured provider and play
returned audio, or records the exact provider/API blocker.

### Tuesday, 8 Dec --- Verify provider availability and terms

-   Check current HeyGen Voice Turbo availability, API requirements,
    pricing, limits, and data policy.
-   Confirm whether the OpenRouter route actually supports the needed
    audio output and voice selection.
-   Do not assume the number of voices or free access remains unchanged.

**Deliverable:** `docs/VOICE_PROVIDER_REVIEW.md`.\
**Acceptance check:** provider choice is based on current documentation
and a successful test, not an old listing.

### Wednesday, 9 Dec --- Compare voice candidates

-   Generate the same short test sentences using available voices.
-   Compare clarity, naturalness, pronunciation, latency, and emotional
    range.
-   Avoid using a real person's voice as a clone without permission.

**Deliverable:** voice comparison notes and selected test voice.\
**Acceptance check:** a voice is selected for testing, or the team
records why another provider is needed.

### Thursday, 10 Dec --- Connect speech to Mira

-   Connect the voice provider to the companion response flow.
-   Play the generated audio reliably.
-   Handle empty text, API errors, timeouts, and playback completion.

**Deliverable:** Mira can speak a generated sentence.\
**Acceptance check:** audio plays from a response initiated in Orion.

### Friday, 11 Dec --- Add speaking state and basic lip movement

-   Trigger `speaking` while audio plays and return to `idle` when it
    ends.
-   Add simple audio-amplitude-driven mouth movement if the
    model/runtime supports it.
-   Ensure mouth animation stops when playback ends.

**Deliverable:** basic speech animation.\
**Acceptance check:** character speaking state follows actual audio
playback.

### Saturday, 12 Dec --- Voice test and upload

-   Test repeated playback, interruptions, provider failure, and long
    responses.
-   Record voice choice and known limitations.
-   Push tested work and update progress.

**Deliverable:** voice-enabled Mira demo.\
**Acceptance check:** Mira can speak a short response reliably.

### Sunday, 13 Dec --- Rest / optional buffer

**Week 4 exit gate:** one selected provider can generate speech and the
character's speaking state follows playback. Perfect lip-sync is not
required.

------------------------------------------------------------------------

## Week 5 --- AI brain and personality

**Monday, 14 December -- Sunday, 20 December 2026**

### Monday, 14 Dec --- Define the AI interface

-   Create a provider-neutral model interface.
-   Keep model names and provider configuration outside UI components.
-   Define request, response, timeout, and error types.

**Deliverable:** AI adapter interface.\
**Acceptance check:** UI code does not depend directly on one model's
response format.

### Tuesday, 15 Dec --- Connect OpenRouter

-   Configure the API securely.
-   Send a simple text request and display the response.
-   Add timeout and error handling.

**Deliverable:** first live AI response in the development environment.\
**Acceptance check:** a request succeeds without exposing the API key in
source control or renderer logs.

### Wednesday, 16 Dec --- Benchmark candidate models

-   Test LFM3-1.7B and at least one alternative available through the
    chosen gateway.
-   Use a fixed set of representative Mira prompts.
-   Record response quality, latency, tool-call format, reliability, and
    cost.

**Deliverable:** `docs/MODEL_BENCHMARK.md`.\
**Acceptance check:** model selection is supported by repeatable tests.

### Thursday, 17 Dec --- Define Mira's personality

-   Write a concise system prompt covering warmth, tone, honesty,
    boundaries, and when to ask clarifying questions.
-   Separate personality instructions from browser permissions.
-   Avoid making personality prompts the only security control.

**Deliverable:** `src/mira/personality/` configuration and prompt
documentation.\
**Acceptance check:** test prompts produce a reasonably consistent tone
without inventing actions.

### Friday, 18 Dec --- Connect conversation flow

-   Connect text input, model request, response display, and voice
    output.
-   Add a simple conversation history for the current session.
-   Handle slow responses and request cancellation.

**Deliverable:** text conversation with optional spoken response.\
**Acceptance check:** user can exchange several messages without losing
the conversation state.

### Saturday, 19 Dec --- AI test and upload

-   Test ambiguous requests, failures, long responses, and inappropriate
    tool suggestions.
-   Update benchmark and progress documents.
-   Push the tested integration.

**Deliverable:** Mira AI conversation demo.\
**Acceptance check:** conversation works reliably for a defined set of
ordinary requests.

### Sunday, 20 Dec --- Rest / optional buffer

**Week 5 exit gate:** Mira can hold a basic text conversation through a
replaceable model adapter and speak the response through the voice
adapter.

------------------------------------------------------------------------

## Week 6 --- Listening and safe browser actions

**Monday, 21 December -- Sunday, 27 December 2026**

### Monday, 21 Dec --- Define the browser tool contract

-   List the exact actions Mira may request.
-   Start with low-risk actions: open a URL, search, list tabs, switch
    tabs, and create a tab.
-   Define input schemas and validation for every action.
-   Require confirmation for actions with meaningful side effects.

**Deliverable:** `docs/BROWSER_TOOLS.md`.\
**Acceptance check:** every supported action has a schema, validation
rule, and permission expectation.

### Tuesday, 22 Dec --- Implement basic browser actions

-   Implement the allow-listed actions in Orion.
-   Keep privileged Electron operations in the appropriate main-process
    boundary.
-   Do not expose arbitrary shell, filesystem, or unrestricted
    JavaScript execution to the model.

**Deliverable:** working browser tool handlers.\
**Acceptance check:** actions work when called by a local test harness.

### Wednesday, 23 Dec --- Connect AI tool calling

-   Convert model tool requests into validated Orion tool calls.
-   Reject unknown tools and malformed arguments.
-   Return action results to the model for a user-facing response.

**Deliverable:** model-to-browser tool bridge.\
**Acceptance check:** Mira can request a supported action and Orion
executes only validated actions.

### Thursday, 24 Dec --- Add speech recognition

-   Test a Whisper-compatible speech-to-text route.
-   Confirm whether it runs locally or through a hosted service and
    document the privacy/cost implications.
-   Add microphone permission and clear recording indicators.

**Deliverable:** speech-to-text experiment integrated into the input
flow.\
**Acceptance check:** a spoken test phrase becomes usable text.

### Friday, 25 Dec --- Connect voice input to the conversation

-   Connect recognised text to the AI conversation.
-   Add listening, processing, and error states.
-   Add a clear way to stop listening.
-   Do not record continuously by default.

**Deliverable:** basic voice conversation loop.\
**Acceptance check:** user can speak a request and receive a response.

### Saturday, 26 Dec --- End-to-end browser test and upload

-   Test spoken and typed requests for opening a website, searching, and
    tab management.
-   Test malformed requests and denied actions.
-   Push tested work and update progress.

**Deliverable:** voice-to-browser demo.\
**Acceptance check:** the assistant can complete the defined low-risk
browser actions and explain failures.

### Sunday, 27 Dec --- Rest / optional buffer

**Week 6 exit gate:** spoken or typed instructions can trigger a small,
safe, allow-listed set of browser actions.

------------------------------------------------------------------------

## Week 7 --- Integration, hardening, and release

**Monday, 28 December 2026 -- Sunday, 3 January 2027**

### Monday, 28 Dec --- Full integration

-   Run the complete flow: input → AI → tool (if needed) → response →
    voice → character animation.
-   Fix integration defects that prevent the main flow from working.
-   Record any remaining mocked components.

**Deliverable:** integrated release candidate.\
**Acceptance check:** at least one complete end-to-end scenario works.

### Tuesday, 29 Dec --- Reliability and failure handling

-   Test missing network, API errors, timeouts, microphone denial, and
    unavailable voice service.
-   Ensure Mira returns to a sensible state after failure.
-   Confirm the browser remains usable if Mira's services fail.

**Deliverable:** failure-handling fixes.\
**Acceptance check:** a failed Mira service does not crash or disable
Orion's core browsing.

### Wednesday, 30 Dec --- Privacy and security review

-   Check API key storage and logs.
-   Check microphone permission and recording indicators.
-   Review browser tool allow-list and confirmation rules.
-   Check that private user data is not sent unnecessarily to external
    providers.

**Deliverable:** `docs/PRIVACY_AND_SECURITY_REVIEW.md`.\
**Acceptance check:** no known critical secret exposure or unrestricted
tool path remains.

### Thursday, 31 Dec --- Performance and usability

-   Check startup time, character rendering, audio delay, and memory
    use.
-   Test the app during a normal browsing session.
-   Fix only release-blocking issues; log noncritical improvements for
    v0.2.

**Deliverable:** performance and usability test notes.\
**Acceptance check:** the core browsing experience remains usable while
Mira is active.

### Friday, 1 Jan --- Documentation and release preparation

-   Write setup instructions and configuration requirements.
-   Document known limitations and provider dependencies.
-   Confirm assets and licences are recorded.
-   Prepare release notes.

**Deliverable:** updated `README.md` and `CHANGELOG.md`.\
**Acceptance check:** the project can be set up using the documented
instructions.

### Saturday, 2 Jan --- Release candidate test and upload

-   Run the v0.1 acceptance checklist below.
-   Fix critical issues.
-   Push final candidate commits.
-   Create a Git tag only if the release checks pass.

**Deliverable:** `v0.1.0-rc1` or documented list of blockers.\
**Acceptance check:** release candidate is reproducible and critical
flows pass.

### Sunday, 3 Jan --- Release decision

-   Review the acceptance checklist.
-   If all critical checks pass, tag `v0.1.0`.
-   If not, move the release date and list remaining issues. Do not
    label an incomplete build as finished.

**Deliverable:** Mira v0.1 release or a revised release plan.\
**Acceptance check:** release status is truthful and documented.

------------------------------------------------------------------------

## 5. Mira v0.1 release acceptance checklist

A release is complete only when these checks pass:

-   [ ] Orion starts and core browsing works.
-   [ ] Mira's character loads reliably.
-   [ ] Character scales correctly when the window changes size.
-   [ ] Idle animation works.
-   [ ] At least a small set of expressions works, where supported by
    the model.
-   [ ] Home screen displays Mira's current state.
-   [ ] User can submit a text message.
-   [ ] AI response is displayed.
-   [ ] Voice provider generates and plays a response.
-   [ ] Character speaking state follows audio playback.
-   [ ] Speech recognition works, or a documented decision is made to
    defer it.
-   [ ] At least three basic browser actions work through validated
    tools.
-   [ ] Unknown or malformed tool requests are rejected.
-   [ ] Sensitive actions require confirmation.
-   [ ] API keys are not committed to Git.
-   [ ] Failure of an AI/voice service does not break normal browsing.
-   [ ] Setup instructions and known limitations are documented.

If speech recognition or another noncritical feature cannot be completed
safely within the time available, release a narrower v0.1 and list the
deferred feature explicitly. Do not fake a passing checklist.

## 6. GitHub setup and delivery convention

Create these GitHub milestones with the dates above:

1.  `M1 — Foundation & Character` --- due 22 Nov 2026
2.  `M2 — Character Integration` --- due 29 Nov 2026
3.  `M3 — Home Experience` --- due 6 Dec 2026
4.  `M4 — Voice` --- due 13 Dec 2026
5.  `M5 — AI Brain` --- due 20 Dec 2026
6.  `M6 — Listening & Browser Tools` --- due 27 Dec 2026
7.  `M7 — v0.1 Release` --- due 3 Jan 2027

Suggested labels: - `milestone` - `frontend` - `live2d` - `voice` -
`ai` - `browser-tools` - `documentation` - `testing` - `blocked` -
`good-first-task`

### Required end-of-week upload

At the end of each Saturday session: 1. Push working code to the feature
branch. 2. Update `docs/PROGRESS.md` with completed work. 3. Link
relevant commits or pull requests to the GitHub issues. 4. Record
blockers and the next concrete task. 5. Do not mark an issue complete
until its acceptance check passes.

Suggested commit format:

`feat(mira): load Live2D character in Orion`

`test(voice): verify speech playback and error handling`

`docs(roadmap): update week 3 progress`

## 7. Suggested repository structure

Adapt this to the existing Orion codebase rather than moving or
rewriting working files unnecessarily.

``` text
orion/
├── apps/
│   └── desktop/
├── src/
│   ├── mira/
│   │   ├── character/
│   │   ├── animation/
│   │   ├── voice/
│   │   ├── speech/
│   │   ├── brain/
│   │   ├── personality/
│   │   └── memory/
│   ├── browser/
│   │   └── tools/
│   └── shared/
├── assets/
│   └── mira/
├── experiments/
│   ├── live2d-lab/
│   ├── voice-lab/
│   └── model-lab/
└── docs/
    ├── ORION_BASELINE.md
    ├── ROADMAP.md
    ├── ARCHITECTURE.md
    ├── DECISIONS.md
    ├── PROGRESS.md
    └── CHANGELOG.md
```

Do not move existing Orion files just to match this example. First
understand the current structure and make the smallest safe changes.

## 8. Daily session format

For each 2--3-hour session:

  Activity                                         Suggested time
  ---------------------------------------------- ----------------
  Review last session and choose today's issue             10 min
  Learn the specific concept needed                    25--35 min
  Implement                                            70--90 min
  Test and debug                                       20--30 min
  Commit and update progress                               10 min

A learning task must end with a practical experiment or a written note.
Avoid spending the whole session watching tutorials without producing a
project result.

## 9. Scope-change rule

New ideas are welcome, but they do not automatically enter the current
milestone.

When a new idea appears: 1. Write it in a GitHub issue labelled
`future-idea`. 2. State what user problem it solves. 3. Estimate its
complexity. 4. Decide whether it is essential for v0.1. 5. If not
essential, move it to the v0.2 backlog.

A milestone can be re-planned when a real technical blocker appears.
Record the reason and the changed date in `docs/PROGRESS.md`.

## 10. First session checklist --- Monday, 16 November

-   [ ] Open the existing Orion project.
-   [ ] Run it and confirm the current working state.
-   [ ] Inspect the Electron main process and renderer.
-   [ ] Locate the home screen and current navigation components.
-   [ ] Record build, test, and run commands.
-   [ ] Identify fragile areas that must not be changed.
-   [ ] Create `docs/ORION_BASELINE.md`.
-   [ ] Commit the baseline notes.
-   [ ] Create the first GitHub issue for the Live2D proof of concept.

**First-session definition of done:** Orion still works, its
architecture and important entry points are documented, and the next
task is clear. Do not begin a broad refactor on day one.

------------------------------------------------------------------------

## 11. Progress log template

Append one entry after each working session:

``` md
### YYYY-MM-DD
- Planned issue:
- What I completed:
- What I learned:
- Tests performed:
- Commit / PR:
- Blockers:
- Next task:
```

**Project principle:** Build one working layer at a time. Keep the scope
visible, record decisions, and prefer a small verified result over a
large unfinished feature.
