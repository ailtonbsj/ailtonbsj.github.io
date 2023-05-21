---
layout: post
title: "Text to Speech on Ubuntu in Portuguese"
date: 2023-05-21 00:00:00 -0300
categories: tutorial linux tts
---
We can read PDF files using Text to Speech on Linux with Okular. For this we need to install Speech Dispatcher and RHVoice. Let's start installing some packages:

```bash
# Speech Dispatcher
sudo apt install speech-dispatcher
sudo apt install speech-dispatcher-espeak-ng
sudo apt install python3-speechd

# List voices in portuguese (low quality)
spd-say -L | grep pt-BR | less

# Speak on terminal
spd-say -l "pt-BR" "Sejam todos bem vindo."

# Configure defaults values
spd-conf

# RHVoice
sudo apt install rhvoice
sudo apt install rhvoice-brazilian-portuguese
sudo apt install speech-dispatcher-rhvoice

# List all voices in RHVoice module (high quality)
spd-say -o rhvoice -L

# Speak on terminal
echo "Sejam bem-vindos!" | RHVoice-test -p "Letícia-F123"
spd-say -o rhvoice -y "Letícia-F123" "Sejam todos bem vindos!"
spd-say -o rhvoice -l pt "Sejam todos bem vindos!"

# Remove defaults confs
rm -rf ~/.config/speech-dispatcher

# Set all confs as default
spd-conf
```

Now it's need to open the file `~/.config/speech-dispatcher/speechd.conf` and replace this line `#DefaultModule espeak-ng` with `DefaultModule rhvoice`. After that we will restart service:

```bash
# Restart service
sudo systemctl restart speech-dispatcher.service

# Speak on terminal
spd-say "Sejam todos bem vindos!"
```

Now we can install Okular and configure TTS to speak in portuguese.

### References

[https://wiki.archlinux.org/title/RHVoice](https://wiki.archlinux.org/title/RHVoice)

[https://github.com/RHVoice/RHVoice](https://github.com/RHVoice/RHVoice)
