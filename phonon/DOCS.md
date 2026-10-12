# Phonon

Phonon is a text-to-speech model that runs on your Home Assistant machine's
CPU, with nothing sent to the cloud. This app runs it and connects it to Home
Assistant over the Wyoming protocol.

## Setup

1. Set the **Model** option to a Phonon checkpoint on Hugging Face, such as
   `OWNER/MODEL`, and the **Language** to the language your assistant speaks.
2. Start the app. The first start downloads the checkpoint. The log says when
   the server is ready.
3. Home Assistant finds the app on its own. Accept the **Wyoming Protocol**
   integration it offers under **Settings > Devices & services**.
4. Under **Settings > Voice assistants**, open your assistant and choose
   **Phonon** as the text-to-speech engine. Pick a voice if the checkpoint has
   several. The assistant's language must be the app's **Language**.

## Options

- **Model.** A Hugging Face repo, or a folder under `/share` holding the
  checkpoint's `config.json`, `tokenizer.json`, weights and voices. A folder is
  for a checkpoint that is not on Hugging Face.
- **Revision.** The branch, tag or commit to download. A commit keeps the voice
  the same when the repo changes.
- **Language.** The language your assistant speaks: `en`, `fr`, `de`, `es` or
  `pt`. Numbers, dates and symbols are spelled out for it, and Home Assistant
  lists the voices under it.
- **Weights.** `q8` is the fastest on most CPUs. `q4k` is smaller. `f32` is the
  original weights. The checkpoint must include the file for the one you pick.
- **Threads.** How many CPU threads to use. `0` uses them all.
- **Hugging Face token.** Only for a private repo.

## Hardware

Phonon needs a 64-bit CPU: x86-64 or ARM64. It is fastest on x86 CPUs with
AVX2 and on recent ARM cores. Older x86 CPUs without AVX2, such as many
Celeron and Pentium Silver chips, get a slower build. The log says when that
happens.

## Use from other devices

The app answers on port 10200 inside Home Assistant. To use it from another
Wyoming client on your network, set a host port for `10200/tcp` under the
app's **Network** settings. There is no password on that port, so only do this
on a network you trust.
