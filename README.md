# Lynctera

Work with your Lynctera cases from a conversation with Claude. Lynctera runs structured work for professional firms as
cases: reviews of documents, research briefs, and matters kept as records. This plugin teaches Claude how cases and
email work in Lynctera, through the Lynctera connector, so it opens the right kind of case, follows its run, drafts
replies in your voice for you to send, and sends you to the right page in Lynctera for the steps that happen there.

## What it needs

**The Lynctera connector**, at `https://app.lynctera.com/api/mcp-b2c`, added to your Claude account first. The
plugin does not add it for you: Lynctera's sign-in needs the client ID Lynctera gives you. You sign in with your
Lynctera account, and the connector acts only as you, in the workspaces you already belong to, and only within the
tool families your workspace's administrator has turned on.

**Skills turned on in Claude.** Under **Settings › Capabilities**, turn on **Code execution and file creation** (called
**Create and edit files** in the newer layout). On a Claude Team or Enterprise plan, an owner turns on **Cloud code
execution and file creation** and **Skills** (being renamed **Plugins**) under **Policy** in Organization settings.
Without them, plugins do not load in Claude.

## What it contains

- **Five skills** that teach Claude how Lynctera works:
  - `lynctera-cases`: choosing a kind of case, opening it, getting documents in, starting and following its run,
    deciding gates, and reading what it produced.
  - `lynctera-records`: keeping records such as opportunities and matters current: their stage and fields, qualifying
    a deal criterion by criterion with evidence from your mail and meeting notes, and reviewing your pipeline.
  - `lynctera-email`: drafting a reply in your own voice and saving it to your Outlook Drafts (never sending it),
    filing an email thread into a case, and tracked links in a follow-up.
  - `lynctera-commitments`: checking what you owe and are owed against your Teams chats, calendar and meeting notes
    (Wispr Flow, Granola, Plaud and the like), and closing the ones that were kept, only when you confirm each.
  - `lynctera-help`: working out why something did not work, and when and how to offer to send feedback to the
    Lynctera team.

## Use it

You need a Lynctera account.

1. **Add the Lynctera connector first.** In Lynctera, open **Settings › Connected apps**: it shows the connector's
   address and client ID. In Claude, add a custom connector with that address: connectors are under **Plugins**, or
   **Customize** if your account has not moved to the new page yet. Under **OAuth client**, choose **Use your own OAuth
   client** (on older screens, open **Advanced settings**) and paste the client ID. Sign in when Claude asks. On a
   Claude Team or Enterprise plan, a Claude owner adds the connector once in Organization settings, and each person
   then connects.
2. **Add the plugin** from the Claude directory, or from **Plugins › Add › Add marketplace** (**Customize › Plugins** on
   older screens) with `Lynctera/claude-plugin`.

Then ask Claude about your work, for example:

- "What is waiting for me in Lynctera?"
- "Open a review of the facility agreement for Acme and tell me what documents it needs."
- "Approve the summary gate on that case once you have shown me what it says."
- "Review my pipeline: what is still unqualified, and what do my emails and meeting notes say about it?"
- "Draft a reply to the last email from Acme accepting Tuesday, and put it in my Drafts."
- "What do I still owe the other side on this deal? Check my Teams chats and meeting notes."
- "Send this to the Lynctera team as feedback."

Claude asks before it opens, starts, stops or approves anything, before it changes a record, before it saves a
draft, and before it sends feedback. Lynctera never sends an email: you press Send in Outlook.

## Data

The skills themselves send nothing anywhere and store nothing. The connector sends Claude's requests to your Lynctera
workspace at app.lynctera.com and returns case details, statuses, commitments and links:

- **Cases:** files are never uploaded through the connector; you add documents in Lynctera.
- **Email:** when you ask for a reply, Claude passes the email and its thread, which it read with your own mail
  connector, to Lynctera to draft in your style. A draft you approve is saved to your Outlook Drafts in your own
  mailbox. Nothing is sent.
- **Records:** Claude reads your other connectors itself, in your conversation, to find evidence for a deal's
  qualification. Only the changes you accept reach Lynctera: the fields, criteria and notes written to the record.
- **Commitments:** Claude reads your other connectors itself, in your conversation. Only what you confirm reaches
  Lynctera: the commitment closed, a short quote or summary of the evidence, and where it came from.
- **Feedback:** when you agree to send feedback, the words you send, and any part of the conversation you choose to
  include, are saved as a feedback record in your own Lynctera workspace, where you can follow it.
- **Memory:** when you agree, what Claude remembers about your work is sent for you to review in Lynctera; nothing is
  kept until you confirm it.

Lynctera's privacy notice is at https://lynctera.com/privacy.

## Support

Email support@lynctera.com, or ask your Lynctera contact.
