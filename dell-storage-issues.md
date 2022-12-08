Dell servers usually have their drive controllers run in Integrated RAID mode, so they need to be flashed to Initiator Target (IT) mode so that Ceph or ZFS can access the drive directly.

This *should* be possible to do given an updated iDRAC and an updated PERC H710 card. However, it is important to note that **the system cannot boot from any drives attached to a card in IT mode.** So, we will need to purchase a CD/DVD to SATA III convertor piece so that we can install a boot drive in the CD/DVD slot and boot from there.

Resources on the topic:
* https://dan.langille.org/2020/10/07/dell-r720-flashing-dell-perc-h710-mini-into-it-mode/
* https://www.reddit.com/r/homelab/comments/llag3u/help_putting_dell_r720_with_perc_h710_in_hba_mode/
