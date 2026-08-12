# Reader Quiz

A single-page, self-contained reader quiz for a Wattpad story. Readers answer
20 questions, get a scored result with tailored next steps, and their anonymous
answers are recorded to a Google Sheet.

**18+ only.** The page carries an age gate and adult-content warning.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire quiz — HTML, CSS and JS in one file. No dependencies, no build step. |
| `vercel.json` | Response headers (blocks search-engine indexing, strips referrers). |

The two Apps Script files (`*.gs`) that build the Google Form and send email
notifications are **deliberately not committed** — they contain the response
sheet ID and the form's edit URL. They live locally only.

## How it works

- 20 multiple-choice questions, one per screen, keyboard-navigable (A–F).
- 17 of them are scored out of 85; three are collected but unscored because
  their options aren't a single scale.
- The score splits into three hidden dimensions — Foundation, Desire and
  Willingness — which are never shown to the reader but decide which advice
  they get. Two readers with the same total can receive opposite guidance.
- Results POST to a Google Form via a hidden iframe. No backend, no database,
  no cookies beyond a single `localStorage` flag remembering the age gate.

## Configuration

Everything editable sits in the `CONFIG` block at the top of the `<script>` in
`index.html`: story title, the related-stories link, the share text, and the
Google Form ID plus its field IDs.

Field IDs are stored as bare numbers, exactly as the setup script prints them.
The `entry.` prefix Google requires is added at submit time.

> Note: if you change any question or answer wording here, make the identical
> change in the Apps Script file and rebuild the form. Google matches
> multiple-choice answers by exact string — a changed apostrophe causes that
> answer to be silently discarded with no error.

## Deploying

Static. Vercel serves `index.html` from the repository root with no build
configuration.

## Privacy

No name, email, login or IP is collected. Responses cannot be traced to a
reader. The response sheet is private and must stay that way.
