---
name: lynctera-help
description: What to do when Lynctera does not work as the user expects through the Lynctera connector - working out why (sign-in, environment, workspace, a feature not turned on, a step that is done in Lynctera itself) and, when it is a gap or a fault in Lynctera, offering to send feedback to the Lynctera team. Use whenever a Lynctera tool refuses, fails, returns an error or is missing, when Lynctera cannot do what the user asked, when the user is stuck, frustrated or working around Lynctera, when they say Lynctera should work differently, or when they praise something Lynctera did.
---

# When Lynctera does not do what the user expected

First work out why. Many refusals have a plain cause the user can fix in a minute. When the cause is a gap or a fault
in Lynctera itself, offer to tell the Lynctera team with `send_feedback_to_lynctera`.

## Work out why

Call `whoami` if you have not in this conversation. Then match what happened:

| What you see | What it means | What to do |
|---|---|---|
| A sign-in link (link_url) comes back | The user's sign-in is not linked to their Lynctera account yet | Give them the link to open in a browser, then try again |
| The environment is dev when they mean their real work, or the other way round | The wrong Lynctera connector is in use | Say which environment you acted on; they switch connector |
| A case is not found, or the answer lists several workspaces | The case is in another of their workspaces, or you need to pick one | Use the workspace that holds it, or ask which workspace they mean |
| A family is not enabled, or a tool you expect is not there | The workspace has not turned that part of the connector on | Tell them; their Lynctera admin turns it on. Do not work around it |
| The role is not permitted | Their role in that workspace can look but not act | Tell them; an admin of the workspace can change their role |
| The action is offered only in Lynctera, with a link | That step is done in the Lynctera app, not over the connector (uploading documents, reading most outputs, some gate decisions) | Give them the link |
| An email is not ingested | Lynctera has not received that email; its mailbox may not be connected | Tell them; do not retry in a loop |
| A run failed or is stuck | Something went wrong inside the case | Show the status and the failed step from `case_get`; a restart picks up at the first step with no output |

If the cause is one of these and the user can fix it, help them fix it. That is not feedback.

## When to offer feedback

Offer to send feedback, once per issue in a conversation, when:

- Lynctera cannot do something the user reasonably expected ("can it...?", and the answer is no);
- a tool fails or refuses for a reason the user did not cause, such as an error, a timeout, or a result that is plainly
  wrong;
- the user has to work around Lynctera: copying things by hand, repeating steps, or doing in another tool what they
  expected Lynctera to do;
- the same problem has happened twice;
- the user says how Lynctera should work, or that something is confusing;
- the user is pleased with something Lynctera did. Praise is feedback too.

Do not offer it:

- for a cause in the table above that the user has fixed;
- in the middle of urgent work. Help with the task first, and offer at the end;
- again for an issue you have already offered on, or that the user has already sent.

## How to send it

1. **Ask first.** For example: "Do you want me to send this to the Lynctera team?" Send only on a yes.
2. **One issue per feedback.** Two problems are two calls.
3. **Write feedback as the user put it**: what they expected, what happened, and what they would like. Add the kind if
   it is clear: bug, request, confusion or praise.
4. **Name the case** with caseId when it is about one, and quote what Lynctera's tool answered (its status and message).
   That is usually what the team needs most.
5. **Ask separately before sharing any of this conversation** as recentChat. Include only the turns that show what
   happened, and leave out client names, counterparties and the content of confidential documents unless the user asks
   for them to be included.
6. **Do not list the Lynctera tool calls you made.** Lynctera adds its own record of them.
7. **Give the user the record link** it returns. They can follow what happens to it there.

If `send_feedback_to_lynctera` is not available, tell the user to pass it to their Lynctera contact, and offer to write
it up for them to send.

## Things to avoid

- Do not promise a fix, a date or a feature. The team decides.
- Do not send feedback the user has not agreed to, or chat they have not agreed to share.
- Do not blame the user, and do not guess at Lynctera's internals; say what you saw.
