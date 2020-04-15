---
layout: post
title: The Story of the Nyan Cat hack
---
I was hacked. It happened at the Capture the Flag (hacking) competition, Tracerfire. The structure of this competition was such that we played with a team and attempted to solve a series of increasingly difficult puzzles. Puzzles were organized into categories and the idea was that each team was supposed to divvy up their players to work on some category, asking for help from the rest of the team when needed. One of the puzzles I worked on involved downloading
a binary called CowCli from the competition server, which let you play a little game with CowServ. The goal of this game was to communicate with the server by sending binary sequences and analyzing the output to ultimately find the correct binary sequence that gave you a code to submit for points.

CowCli was malicious. By default, it wouldn’t run with user permissions, and my gut reaction was to sudo run it (instead of chmod, ugh…). As an aside, though this was a “hacking” competition, the main goal was to solve puzzles, not infiltrate other team’s machines. So I guess I was lulled into a false sense of security. None the less, I ran CowCli as root and later found out it did more than play this little binary game.

Apparently, it ran a netcat command that listened for connections on some obscure port and returned a shell (root, in my case ) to users who knocked on that port. Further, it beaconed a simple message to the local network (which we all were using for the competition) saying something equivalent to, “this machine has been had!” One further point, our ip addresses were assigned based on the table we were sitting at, so one knew the physical location of an ip address at
        Tracerfire.

        So, the guy who had inserted this bit of hack into CowCli took my machine and executed the Nyan Cat Hack. Luckily, it wasn’t meant to do any real damage, but it served as a message for what he could have done. This Nyan Cat Hack overwrote my bootloader with code that ran a looping video of Nyan Cat. The guy then set my machine to restart in 30 seconds, walked over to me, and stood directly behind me while my computer rebooted into Nyan Cat. He silently watched me go from
        confused to angry to helpless. It was actually very creepy, to be honest… Moral of the story, don’t execute binaries you don’t trust, especially as root.

See how my post on <a href="/2012/10/01/nyan_how_to.html">how the hack works</a>!
