---
layout: post
title:  "Using GNU Privacy Guard Tools"
date:   2020-05-28 20:06:00 -0300
categories: tutorial linux debian
---
You can manage your PGP keys on linux using the commands below.

```bash
# List keys
gpg --list-keys
gpg --list-secret-keys

# Delete keys
gpg --delete-key email.address
gpg --delete-secret-key email.address

# Create key
gpg --full-generate-key
gpg --gen-key

# Get keys
gpg --output public.key --armor --export email.address
gpg --output private.key --armor --export-secret-key email.address

# Store key
gpg --import public.key
gpg --import private.key
```
