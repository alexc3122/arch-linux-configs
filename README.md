# linux-configs
This is a collection of my user and system configuration files while using Arch Linux. Most of these files reflect things I've learned over time when using Arch.

Some examples where this is evident:

* By default, the TRIM command isn't configured to run on Arch Linux. 
Depending on your use case, you may want to turn this on to help improve the performance of your SSD/NVMe drive. If you do enable TRIM, make sure you enable the appropriate system service. Be warned that this does have security implications if your drive is using LUKS. You can read about this on the Arch Linux wiki.

* To enable resuming from hibernate, make sure the `resume` hook is in the list of `HOOKS` in your mkinitcpio configuration.

* Tweaks to your `.bashrc` and `.vimrc`
