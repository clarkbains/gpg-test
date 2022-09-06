# GPG-Test

## What
Tested signing of my git commits. View the commit history to this repo and see the 'Verified' badge next to my recent commits. Previously I did this using a gpg keypair copied to all my devices and secured with a password. I recently got a yubikey though, and have moved a new key set (Using different keys for certify, auth, enc and sign this time) to my yubikey.

## Why
Realistically, I just like the verified badge, but don't want to use github web to make changes. It also lets me use vigilant mode, which helps guard against things like [this](https://github.com/Amog-OS/AmogOS/commit/0bb33e31e2a529bfd13c6013d1ad2dffa2485b61), by showing a big orange unverified badge.

I did not want to put my keys directly on my work laptop, and my own laptop's filesystem's security is not ideal (no LUKS, apparmour, or selinux configured.) The yubikey makes it so this is never stored on the computer I am using it with. 

## How
I created my new keyset, plugged in the yubikey, and used gpg's `keytocard`. On any new machine, all I have to do now, is plug in my yubikey, run `gpg --card-edit`, then `fetch` to get my public key from [pgp.mit.edu](https://pgp.mit.edu), and then I have a fully working pgp keyring. Then `git config --global user.signingkey 0F48BA00E928E05B2894078678CA2300ED571AEC` (Found using `gpg --list-keys`). Then I can `git commit`, using the `-S` switch, and the commit will be signed using the yubikey, which I've setup so I have to enter a pin, and then tap the physical device before it will sign. Afterwards I can git push, and the commit will show on github with the pretty 'verified' badge.

