# Phonon for Home Assistant

A Home Assistant app that runs [Phonon](https://github.com/gradium-ai/xn-ptts),
a local text-to-speech model, and connects it to your voice assistants over the
Wyoming protocol. It speaks on the CPU of the machine Home Assistant runs on,
and starts speaking a reply while the assistant is still writing it.

## Install on Home Assistant OS

[![Add this repository to your Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fgradium-ai%2Fphonon-home-assistant)

Or add `https://github.com/gradium-ai/phonon-home-assistant` as a repository in
Home Assistant's app store.

Then install **Phonon**, set its model and language, and start it. The
[app's documentation](phonon/DOCS.md) walks through the rest.

## Other installs

On Home Assistant Container or Core, run the server with Docker yourself, as
the [server guide](https://github.com/gradium-ai/xn-ptts/blob/main/ptts-openai-server/README.md#home-assistant)
shows, then add the **Wyoming Protocol** integration with its address and port
`10200`.

## License

MIT or Apache-2.0, at your option.
