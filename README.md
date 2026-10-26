# Lynctera

Work with your Lynctera cases from a conversation with Claude. Lynctera runs structured work for professional firms as
cases: reviews of documents, research briefs, and matters kept as records. This plugin connects Claude to your
Lynctera workspace and teaches it how cases and email work in Lynctera, so it opens the right kind of case, follows
its run, drafts replies in your voice for you to send, and sends you to the right page in Lynctera for the steps that
happen there.

## What it contains

- **The Lynctera connector**, at `https://app.lynctera.com/api/mcp-b2c`. You sign in with your Lynctera account the
  first time Claude uses it. It acts only as you, in the workspaces you already belong to, and only within the tool
  families your workspace's administrator has turned on.
- **Four skills** that teach Claude how Lynctera works:
  - `lynctera-cases`: choosing a kind of case, opening it, getting documents in, starting and following its run,
    deciding gates, reading what it produced, and keeping records current.
  - `lynctera-email`: drafting a reply in your own voice and saving it to your Outlook Drafts (never sending it),
    filing an email thread into a case, and tracked links in a follow-up.
  - `lynctera-commitments`: checking what you owe and are owed against your Teams chats, calendar and meeting notes
    (Wispr Flow, Granola, Plaud and the like), and closing the ones that were kept, only when you confirm each.
  - `lynctera-help`: working out why something did not work, and when and how to offer to send feedback to the
    Lynctera team.

## Use it

You need a Lynctera account. Connect the Lynctera connector from the plugin's Connectors tab, then ask Claude about
your work, for example:

- "What is waiting for me in Lynctera?"
- "Open a review of the facility agreement for Acme and tell me what documents it needs."
- "Approve the summary gate on that case once you have shown me what it says."
- "Draft a reply to the last email from Acme accepting Tuesday, and put it in my Drafts."
- "What do I still owe the other side on this deal? Check my Teams chats and meeting notes."
- "Send this to the Lynctera team as feedback."

Claude asks before it opens, starts, stops or approves anything, before it saves a draft, and before it sends
feedback. Lynctera never sends an email: you press Send in Outlook.

## Data

The skills themselves send nothing anywhere and store nothing. The connector sends Claude's requests to your Lynctera
workspace at app.lynctera.com and returns case details, statuses, commitments and links:

- **Cases:** files are never uploaded through the connector; you add documents in Lynctera.
- **Email:** when you ask for a reply, Claude passes the email and its thread, which it read with your own mail
  connector, to Lynctera to draft in your style. A draft you approve is saved to your Outlook Drafts in your own
  mailbox. Nothing is sent.
- **Commitments:** Claude reads your other connectors itself, in your conversation. Only what you confirm reaches
  Lynctera: the commitment closed, a short quote or summary of the evidence, and where it came from.
- **Feedback:** when you agree to send feedback, the words you send, and any part of the conversation you choose to
  include, are saved as a feedback record in your own Lynctera workspace, where you can follow it.
- **Memory:** when you agree, what Claude remembers about your work is sent for you to review in Lynctera; nothing is
  kept until you confirm it.

Lynctera's privacy notice is at https://lynctera.com/privacy.

## Support

Email support@lynctera.com, or ask your Lynctera contact.
