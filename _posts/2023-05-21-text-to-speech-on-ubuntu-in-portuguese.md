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
spd-say -y "Portuguese (Brazil)+Linda" "Sejam todos bem vindo."

# Configure defaults values
spd-conf

# RHVoice
sudo apt install rhvoice
sudo apt install rhvoice-brazilian-portuguese
sudo apt install speech-dispatcher-rhvoice

# Remove local default values (need reboot)
rm -rf /home/$USER/.config/speech-dispatcher

# List all voices in RHVoice module (high quality) - Remove default values before
spd-say -o rhvoice -L

# Speak on terminal
echo "Sejam bem-vindos!" | RHVoice-test -p "Letícia-F123"
spd-say -o rhvoice -y "Letícia-F123" "Sejam todos bem vindos!"
spd-say -o rhvoice -l pt "Sejam todos bem vindos!"

# Set global confs
# yes -> system -> espeak-ng -> pt-BR -> pulse -> 0 -> 0 -> 0 -> yes -> yes -> yes
sudo spd-conf
```

Now it's need to open the file `/etc/speech-dispatcher/speechd.conf` or `~/.config/speech-dispatcher/speechd.conf` and replace this line `#DefaultModule espeak-ng` with `DefaultModule rhvoice`. After that we will restart service:

```bash
# Restart service
sudo systemctl restart speech-dispatcher.service
sudo reboot

# Speak on terminal
spd-say "Sejam todos bem vindos!"
```

Now we can install Okular and configure TTS to speak in portuguese.

## Watch my tutorial on Youtube

<iframe width="100%" height="480" src="https://www.youtube.com/embed/qiFCQsm-A7U" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

### References

[https://wiki.archlinux.org/title/RHVoice](https://wiki.archlinux.org/title/RHVoice)

[https://github.com/RHVoice/RHVoice](https://github.com/RHVoice/RHVoice)
