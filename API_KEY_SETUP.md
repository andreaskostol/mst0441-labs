# Getting set up (one time, about ten minutes)

**MST 0441: Consumers, Trade and Business Strategy**

## Opening a lab in Colab

The labs live at **github.com/andreaskostol/mst0441-labs**. Click the lab's
badge there (or the Colab link on It's Learning) and it opens in Colab
directly -- nothing to download. The notebook opens **read-only**: choose
**File -> Save a copy in Drive** first, and do the lab in your copy. If you
reopen the original link later you get the latest version of the lab, not
your work; your work lives in your Drive copy.

Every lab in this course ends with a section called *Work with your
assistant*. From session 2 those sections call a model from code, through a
function called `ask_model()`. To make `ask_model()` work you need a key of your own: a
short string that tells the provider who is asking, so it can meter what you
use.

Do this once. It carries you through all six labs.

You do not need a key to pass the labs. Every prompt in every notebook is an
ordinary Python string, and you can print it and paste it into any chat
window instead. `ask_model()` will tell you when it has no key rather than
failing. But the interesting experiments, the ones where code loops over the
model or hands it a tool, only work over a key.

---

## The course route: an OpenRouter key

You will be given an **OpenRouter key** in class. It has a fixed credit on
it, enough for the whole semester's labs, and it runs a Mistral model.
Store it under the name `OPENROUTER_API_KEY` as described below.

That is all most of you need to do. The rest of this page is the fallback.

## Fallback: a free Gemini key

If your OpenRouter key is missing or has run out, you can mint your own free
key instead:

1. Go to **aistudio.google.com/apikey** and sign in with the Google account
   you already use for Colab.
2. Click **Create API key** and copy it. It looks like `AIza...`.
3. Store it under the name `GOOGLE_API_KEY`.

The notebooks look for `OPENROUTER_API_KEY` first and fall back to
`GOOGLE_API_KEY`, so whichever you have, the code is the same.

## Put the key in Colab Secrets

**Never paste a key into a cell.** A notebook you share, submit, or push to
GitHub carries its cells with it, and a key in a cell is a key you have
published. Colab has a store for exactly this.

1. Open any lab notebook.
2. In the left sidebar, click the **key icon** (Secrets).
3. **+ Add new secret**.
4. Name: `OPENROUTER_API_KEY` (or `GOOGLE_API_KEY` for the fallback).
   The name must match exactly, capitals included.
5. Value: paste the key.
6. Turn on **Notebook access** for the notebook you are in. You have to do
   this per notebook; it is one click each time.

The secret lives in your Google account, not in the notebook file. Anyone
you send the notebook to gets your code without your key.

## Test it

Run the `ask_model()` cell in any lab, then run:

```python
print(ask_model("Reply with the single word: ready"))
```

You should see `ready`. If you see `(no API key found...)`, the secret name
does not match, or notebook access is off for this notebook.

---

## What the labs do with it

| Session | Step | What you build |
|---|---|---|
| 2 | the call | `ask_model()` itself: text in, text out, a string your code can test |
| 3 | the system prompt | the same question with and without standing instructions |
| 8 | pre-registration | a prediction collected before the model can see any output |
| 9 | the role | a system prompt that makes the model argue against you |
| 12 | loops, and a tool | five calls instead of one; then your solver handed over as a tool |
| 15 | the agent | the model inside a loop, playing a repeated game against your code |

By session 15 you will have written the loop that makes a model into an
agent: history in the prompt, a decision back, your code deciding what
happens next. It is about twelve lines. That is the whole trick.

## Not the same as the tutor

The course tutor notebook (`tutor.ipynb`) has its own function called
`ask()`. That one talks to the course tutor, which knows the session's
rubric and problems and will not hand you solutions. `ask_model()` in the
labs talks to a plain model with your own key and no course knowledge. Two
different functions with two different jobs; both can live in one notebook.

## Rules

* Never paste a key into a cell, a chat, or an email.
* Never commit a notebook with a key in it.
* If you think a key leaked, delete it at the provider and make a new one.
  This takes a minute and costs nothing.
* Keys are personal. Do not share one with the person next to you; they can
  mint their own in the same ten minutes.
