# Arch Linux Config

This repository is a small collection of my user and system configuration files on Arch Linux. Most of these files reflect things I've learned over time and tweaks that I've found useful, important, or necessary. Some stuff isn't Arch Linux specific, such as `pip`, `tmux`, or `vim` configuration. Nonetheless, there are included here, mostly because I don't feel like they warrant an entirely new repo themselves.

Some notable configuration tidbits here:

* By default, the TRIM command isn't configured to run on Arch Linux for SSDs/NVMe drives. 
Additionally, if you leverage LUKS to encrypt your root file system, you may need to add the appropriate kernel flags on boot to enable TRIM. Depending on your use case, you may want to turn this on to help improve the performance of your SSD/NVMe drive. To enable TRIM on a system using LUKS and where the the `encrypt` hook is used, you'll need to add the `:allow-discards` to the UUID specifier.

  This page on the Arch Linux wiki describes which flags and where precisely:
  https://wiki.archlinux.org/title/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD)

  Note that once the flag is present, you'll still need to enable the systemd service which will trigger TRIM to run periodically (if you choose to have TRIM not run continuously). This page on the Arch Linux wiki gives more details:
  https://wiki.archlinux.org/title/Solid_state_drive#Periodic_TRIM

  Be warned that this does have security implications it could be a side-channel and reveal patterns in files activity.

* To enable resuming from hibernate, make sure the `resume` hook is in the list of `HOOKS` in your mkinitcpio configuration. Additionally, on laptops you may find that Linux doesn't really support hybrid sleep + hibernation very well. You just pick either hybrid-sleep or suspend-then-hibernate. For suspend-then-hibernate, Linux will keep the system in a suspended state until the battery reaches a certain threshold, then hibernate. This could be considered suboptimal behavior. However, you can change it by telling systemd how long to sleep for before it should hibernate.

* `NetworkManager` sometimes exhibits inconsistent behavior when renewing a DHCP lease. The `/etc/NetworkManager/conf.d/dhcp-client.conf` file tells NetworkManager to use a different DHCP client instead of the native, built-in one.

* For systems with NVIDIA cards, you'll need to enable the Direct Rendering Manager (DRM -- I know... great acronym) for Wayland to function properly. This can be done using `modprobe` and setting `modeset=1` for the `nvidia_drm` module.


Some other special things to note:

* As is evident, rEFInd was previously used on some of my systems. I've since migrated to using Unified Kernel Images with Secure Boot. I've left the rEFInd configuration largely for posterity.


