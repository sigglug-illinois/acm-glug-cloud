# 2022-11-27

- Present: Nathan, Quan, Sun, Sam, Evan. I am writing names, so if future readers have a question about this, they can ask one of the people present.
- We found the second rack labelled ACM. Almsot all of the equipment on it is also labelled ACM.
- We removed harddrives from their original machines, noting their original configuration.
- We wrote a physical label on them.
- The harddrives appear empty or difficult to recover. They came from dead machines, so it is unlikely they have currently useful data.
- We tested the harddrives with [SMARTMon](https://wiki.archlinux.org/title/Smart).
- See our drive inventory and testing results [here](https://docs.google.com/spreadsheets/d/1Mex7f6qN9uSypg3oOCucHvvdE0HO6KnUJdlAhtJ2QbY).
- We tried to boot helium (see above document), but we got stuck on "waiting for iPXE" or something like that.

# 2022-12-30

- Present: Sam, Evan (treasurer)
- We tried the keys in ACM's posession, but none of them turn the locked server cover.

# 2022-12-06

- Present: Sam, Chase
- We were able to remove the locked server cover. The lock was not really engaged, so we could remove the cover nondestructively.

# 2022-12-07

- Present: Sam, Russel, Nathan, Benjamin, Liam, Quan, Sun, Orbital
- We added more harddrive details and serial numbers to the [inventory doc](https://docs.google.com/spreadsheets/d/1Mex7f6qN9uSypg3oOCucHvvdE0HO6KnUJdlAhtJ2QbY).
- We successfully booted hydroegn (see the inventory doc) to a live image, but there is no network.
- We think that the previous "waiting for iPXE" was due to using a PXE image, but the network was not up.