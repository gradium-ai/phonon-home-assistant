# Phonon

Phonon is a text-to-speech model that runs on your Home Assistant machine's
CPU, with nothing sent to the cloud. This app runs it and connects it to Home
Assistant over the Wyoming protocol.

## Setup

1. Set the **Language** to the language your assistant speaks. For English,
   that is all: the app uses Phonon 31m. For French, German, Spanish or
   Portuguese it uses that language's Phonon 40m model, which is gated: accept
   its terms on its Hugging Face page, for example
   [gradium/phonon-40m-fr](https://huggingface.co/gradium/phonon-40m-fr), and
   set the **Hugging Face token** option.
2. Start the app. The first start downloads the model and the voices of your
   language. The log says when the server is ready.
3. Home Assistant finds the app on its own. Accept the **Wyoming Protocol**
   integration it offers under **Settings > Devices & services**.
4. Under **Settings > Voice assistants**, open your assistant and choose
   **Phonon** as the text-to-speech engine, and pick a voice. Home Assistant
   lists the model's default voice and the voices of the
   [Phonon voice catalog](https://huggingface.co/gradium/phonon-voices) in your
   language. The assistant's language must be the app's **Language**.

## Options

- **Model.** Leave it empty for the model of your language. Otherwise a Hugging
  Face repo, such as `gradium/phonon-40m-multilingual` (all five languages in
  one model), with `@commit` after it to keep the same version when the repo
  changes. Or a folder under `/share` holding the checkpoint's `config.json`,
  `tokenizer.json`, weights and voices, for a checkpoint that is not on
  Hugging Face.
- **Language.** The language your assistant speaks: `en`, `fr`, `de`, `es` or
  `pt`. Numbers, dates and symbols are spelled out for it, and Home Assistant
  lists the voices under it.
- **Weights.** `q8` is the fastest on most CPUs. `q4k` is smaller. `f32` is the
  original weights. The checkpoint must include the file for the one you pick.
- **Threads.** How many CPU threads to use. `0` uses them all.
- **Hugging Face token.** For the gated Phonon 40m models, after you accept a
  model's terms on its Hugging Face page, and for a private repo.

## Licenses

Phonon 31m is under Apache 2.0. The Phonon 40m models are under CC BY-NC 4.0,
for non-commercial use. Each model's Hugging Face page has its license.

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
