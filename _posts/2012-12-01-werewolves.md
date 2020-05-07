---
layout: post
title: Side Channels Werewolves Project
---
Virtual Werewolves is a commandline multiplayer game designed to teach cybersecurity, adapted from the popular party game.

Virtual Werewolves is a program I wrote as a teaching assistant for Jed Crandall at UNM. He and his PhD student, Roya Ensafi, had a Cyber Security class, in which they wanted to teach their students about information flow and inference channels (via information leaks due to timing and storage attacks). So, as their teaching assistant, I was tasked with developing a Linux/Python game to demonstrate these concepts.

The game I came up with was based off the dinner party game, Werewolves (which itself is based off of a game called Mafia). In Werewolves, a moderator assigns each player a random role, either a werewolf or a townsperson. The game alternates between rounds of night and day. At night, werewolves silently decide and inform the moderator of who to eat, eliminating that player from the game. During the day, the entire town, including the werewolves, must discuss and vote on a player to hang. The
werewolves must eat the townspeople before the townspeople hang all the werewolves. The game is over if one of the team succeeds. Further, there is a special role, the witch, who plays for the townspeople. The witch acts at night, after the werewolves, and may heal an eaten victim or poison any player of his/her choosing one time each throughout the game.

So, the game I developed is a virtual version of this game. The game is played on Linux, such that players remotely log into the a game server. The game server acts as an automated moderator to initialize games and cycle through rounds, allowing players to discuss and vote as needed. Communication within the game is implemented on top of a series of named pipes with restrictive permissions such that players can talk to the moderator and vice versa. The server also handles things such group
communication and eliminating players from the game.

The educational component comes in with the game client. Since game state is somewhat predictable (the round that the game is currently in), information about game state can be inferred by analyzing /proc. In the Cyber Security class, students are encouraged to develop their own clients that automatically analyze /proc. For example, since communication uses named pipes, which inherently requires system calls to use, one analysis can be to count the number of context switches each process is
making at which point in the game. Werewolves must, at a minimum, vote at night to decide upon whom to eat, and a careful context switch analysis can identify a wolf as it votes.

For a couple months, we had our class play this game every Monday to test out their new clients. On Wednesdays, Jed or Roya would teach the class some new inference channel to potentially exploit, and on Fridays, the class would develop their clients to make use of the new information. In the end, the project was largely successful. It gave students a hands on opportunity to put the side channel concepts into practice, in a competitive way.

The slides below were for the final presentation that I delivered after finishing a version one of the project.

<center>
  <iframe src="https://www.slideshare.net/slideshow/embed_code/18368385" width="100%" height="300px" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" allowfullscreen=""></iframe>
</center>
