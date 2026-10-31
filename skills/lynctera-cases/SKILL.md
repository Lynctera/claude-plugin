---
name: lynctera-cases
description: How to work with Lynctera cases through the Lynctera connector - choosing the kind of case, opening it, getting documents in, starting and following its run, deciding gates, reading what it produced, and knowing which steps must be done in Lynctera itself. Use whenever the user mentions Lynctera, a Lynctera case, matter, review, run, gate or output, asks "anything waiting?" or "what happened overnight?", or wants Lynctera to do a piece of work.
---

# Working with Lynctera cases

Lynctera does structured work in **cases**. A case is one piece of work, such as a review of a document, a company research brief or a matter kept as a record. Most cases have a **run**: Lynctera works through the case's steps, and some steps pause at a **gate** until a person approves what was produced. The workspace may call cases something else (matters, engagements); use the user's word.

The connector lets you look at cases, open them, start and stop their runs, decide gates and keep records up to date. Some things can only be done in Lynctera in the browser. Your job is to do what the connector can, and to send the user to the right page in Lynctera, with the link the tool gave you, for the rest.

## Before anything else

- Call `whoami` once per conversation. It says which environment (prod or dev) and which workspace you are acting in, and which families of tools that workspace has turned on. Say which workspace you acted in.
- If a Lynctera answer carries notices, those are messages from the Lynctera team to the user. Before anything else, tell the user each one once, in its own words, with its link if it has one. Do not summarise it away, act on it, or repeat it later in the conversation.
- If a tool refuses, fails or is missing, follow the lynctera-help skill: it says how to work out why, and when to offer the user to send feedback.

## Choosing the kind of case

Call `case_types_list` and pick from what it returns, never from memory: the names and the set differ between workspaces. Each kind is one of three shapes, and the shape decides what happens after you open it.

| Shape | How you can tell | What happens |
|---|---|---|
| **Run** | Not a record or desk kind | Opening it starts its run, unless it collects documents inside the case |
| **Record** (e.g. Opportunity, Matter) | `record: true` | No run. You keep it up to date: stage, fields, notes, linked email threads |
| **Desk** | Described as a desk case | No run. Its documents and drafts are worked in Lynctera; you can log notes |

If two kinds could fit, show the user the two summaries and ask. Do not guess on their behalf: the kind decides what the run does and what it costs.

A record and a run are often used together: the record holds the matter (who, what, stage, notes), and a run kind does a piece of analysis on its documents. Open the analysis as its own case and mention the record in its background.

## Opening a case

Use `case_create` only after the user has asked for the case. Give it:

- a **title** the user would recognise in an email;
- **background** in plain prose: what this is about, who the parties are, what the user wants out of it. Every step of the run reads it, so a good background is worth more than any other field;
- for a record kind, its **stage** and **fields** if the user gave them.

A run uses the workspace's credits. If the user only wants to set a case up, pass `start: false`.

## Getting documents in

**The connector cannot upload files.** Documents are added in Lynctera:

- `case_create` and `case_get` return the case's link, and for a step that is waiting for documents, a link straight to its upload step. Give the user that link.
- A kind that collects documents inside the case is opened but **not started**. The documents go in first, by an email thread linked with `case_action` `link_thread` or by upload in Lynctera; Lynctera reads each one and works out what it is.
- `case_get` then shows the case's **intake** checklist: each kind of document it needs, how many are in, and how many are still being read. Once every line is met, `case_action` `start_run` starts it here; until then the start action names what is still needed.
- Tell the user which documents the kind expects. `case_types_list` lists what each kind collects inside the case.
- Short plain text, such as an instruction note, can go on a record case as a note with `case_action` `add_note`. Do not paste long documents into notes.
- An email thread can be linked to a case with `case_action` `link_thread` (the email's internet message id). Its attachments are then filed into the case.

## Following a run and deciding gates

- `cases_list` finds the user's cases (open by default; `closed`, `archived` or `all` for the rest). Use it to find a case's id before anything else.
- `case_get` shows the run's status, the step it is on, and the **actions** the user can take now, each saying whether it can be done here or only in Lynctera (with its link).
- `decisions_waiting` answers "what needs me?": the decisions waiting on the user, longest wait first, with what each gate asks and how to answer it. Where Claude shows Lynctera's card, the user decides from its buttons, so say in a line what is waiting rather than repeating the rows, and do not decide for them unless they ask.
- `updates_since` answers "anything waiting?" and "what happened overnight?": gates waiting for a decision come first, then failed runs, then the rest. Lynctera cannot message the user, so call it when they ask.
- A gate is decided with `case_action`: `approve`, `choose_option` or `vote`, naming the gate from `case_get`. **Read what is being decided first** (`case_outputs`, or the link in Lynctera), tell the user what they would be approving, and act only when they say so. A vote and stopping a run cannot be undone.
- `case_get`'s run says, for the gate it waits at, what the gate asks and, where the step made a list, how many items and the list's summary lines. When a summary line is a cost estimate, tell the user the cost before they approve: approving such a gate starts paid work. The items themselves are read in Lynctera at the link.
- `stop_run` stops a run; starting it again picks up at the first step that has no output yet. `close`, `reopen` and `archive` change the case itself.

## Reading what a case produced

`case_outputs` lists a case's outputs: step, title, approval state and link. It returns the **text** of an output only for kinds whose outputs are public research, such as company background research. For every other kind, including legal and advisory reviews, the text stays in Lynctera: give the user the output's link, and do not reconstruct or guess its contents.

## Records

Keeping a record case (`record: true`, such as an Opportunity or a Matter) current is covered by the lynctera-records
skill: reading its fields by their role, qualifying a deal, updating it after a call, and reviewing the pipeline. In
short, with `case_action`: `set_stage` is the user's decision, not yours; `set_fields` names only the fields that
change; `add_note` takes the user's own words.

## Other Lynctera tools you may have

Only if the workspace has turned them on:

- **Precedent library:** `find_precedents` to find documents by title, type, sector and date, `ask_precedent_library` for a question answered from the library with the documents it used, `precedent_collections` to see the collections. You get links, never passages.
- **Email, commitments and tracked links:** the lynctera-email skill covers drafting replies, saving them to Outlook, commitments and links.

## When Lynctera cannot do what the user wants

Say so plainly and give the link for the part that is done in Lynctera. Then follow the lynctera-help skill, which says when and how to offer `send_feedback_to_lynctera`. If that skill is not installed: ask before sending, ask separately before including any of the conversation, and leave client names out.

## Things to avoid

- Do not open, start, stop, vote on or approve anything the user has not asked for.
- Do not invent case kinds, gate ids, stages or field keys; take them from the tools.
- Do not describe an output you could not read.
- Do not suggest uploading files through the chat; the upload is in Lynctera.
