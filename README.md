# Cinatra HITL Prompt Drive Skill

When an agent run pauses on an open human-in-the-loop (HITL) gate and the operator answers in the chat prompt window instead of the embedded form, this bundle is the extraction instruction that turns that free-text reply into typed gate field values — and nothing else. It is an internal prompt: never absorbed into an injectable bundle, never uploaded, and absent from every injection set.

**Install:** Install `@cinatra-ai/hitl-prompt-drive-skill` in your Cinatra instance. No credentials or external accounts are required — the bundle operates entirely within the Cinatra chat runtime.

**Usage:** You do not invoke this skill yourself. The chat HITL consumer resolves it through the `chat.hitl-prompt-drive` capability, hands it the gate's flattened field schema plus the operator's chat message, and takes back a single JSON object containing only the gate fields the message actually supplies.

**Configuration:** None.

**Development:** Clone the repository and run `node extension-kind-gate.mjs --package-root .` to validate the manifest. The bundle lives in `skills/chat-hitl-prompt-drive/`.

**Troubleshooting:** If chat replies to an open gate never fill gate fields, the consumer may not be resolving the capability — confirm this package is installed and active in the workspace. An empty result can also be intentional: approvals and non-responses map to `{}` by design.

## Works with

- Cinatra chat prompt-window HITL drive

## Capabilities

- Extract typed gate field values from an operator's free-text chat reply
- Coerce values conservatively — booleans, numbers, URLs — never inventing data
- Map approval-only messages to an empty object so the caller adds the envelope
- Return an empty object for new tasks and questions so the caller can route them to normal chat
