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
  - We established a serial connection with the network switch at the top of the rack. However, the switch prompts for a username and password. None of the obvious combinations work. We can either do a hard reset or consult engineering IT (maybe they manage it anyway).

# 2023-01-16

- I filed a support ticket with Engineering IT on 2023-01-16. Here are the responses:
- > (2023-01-17) I can either make the changes on the switch for you, or escalate your request to tech services networking.
- > (2023-01-19) I just learned that there were ACM members that had access to the switch granted to them, are there anyone still there that has that access?
- > (2023-01-20) I will get in touch with my contact at networking and we can work on getting these privileges transitioned to members who are here.
- > (2023-01-26) You need to get in touch with Matt Greimer and the ACM infrastructure lead Aydan Pirani. The ACM groups are strictly controlled and even I do not have access to them. so following up with Matt and Aydan will be your best option to move forward.
- https://help.uillinois.edu/TDClient/30/uofi/Requests/TicketRequests/TicketDet?TicketID=t6-gllpA6CU_

# 2023-02-01

- Present: whole general membership (yay good turnout!)
- Moved servers down to the ACM back room. We had trouble separating the server from the rack, so we just took both together.
- Tried to update firmware on several units. The BIOS was already latest. I don't know how to verify the firmware of the other devices in the blade (e.g., BMC).
- Installed OSes on silicon and lithium.

# 2023-02-07

- Nathan and Sam confirmed that Matt has access to the switch in question and the related ACM networks. We would like to disable MAC filtering on the ports, since the ports are behind a swipe-access door with few people allowed access. However, we don't know how to do that in IRIS.

- https://answers.uillinois.edu/illinois/48169
