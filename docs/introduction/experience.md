First, the competition will provide a portal to submit flags. The URL of the portal is like this: `http://172.16.4.1/Common/submitAnswer`. We need to use the information in the document to connect to the portal and submit flags. To submit flags, you need to use HTTP Post method with two parameters. One parameter `answer` is value of the flag, the other parameter `token` is value of the team's token.


During the competition, the organizer will also provide each participating team with a **virtual machine for analyzing network traffic**, and players need to download the network traffic file and analyze it.


## Pay attention to the Gamebox's status


In the competition, you can check your own and your opponent's Gamebox status during a match. Paying attention to the status so you can pick up information early and adjust based on that information.


There are several reasons why your GameBox is down:


1. There was an error in the organizer's system that incorrectly displayed the Gamebox’s status. In this case, problems can normally be discovered before the competition. If you found issues in organizer's system, inform staff as early as possible to minimize damage.
2. The patch program can accidentally cause the service to be unavailable. Check the Gamebox’s status after the patch, if the service is unavailable, fix it immediately. You don't worry about replacing it with an unpatched service/program since when the service is down, teams won't lose too many points. However, the unpatched service/program will be exploited by top teams to obtain more points. You need to deal with this type of situation on a case-by-case basis.
3. Teams might use illegitimate attack methods that will bring down the Gamebox, if discovered, fix it immediately.
4. The organizer modifies the check program. In that case, the organizer will notify all the teams. You will a majority of the Gamebox are unavailable.


You can get the following information about the opponent’s Gamebox:


1. Determine which teams failed to defend their GameBox based on network traffic. So, more attacks can be made against these teams.
2. When a team gets First Blood, you can tell if the First Blood team used an exploit based on each teams’ Gamebox status.   
Furthermore, you can see which team's defense didn't work.

## Knowing the network segment and ports


During the competition, the organizer will assigned a network segment.


In maintenance, your team must be on the assigned network segment to connect to the Gamebox. Then login based on the CTF username and password provided. This network segment will allow you interact with another team’s Gamebox and vulnerable programs.


!!! warning

Here you must pay close attention to the port. If a port is mistyped or mistaken, then it might bring unnecessary problems, like unable to submit flags. Mistyping the port is hard to detect. So, you should double-check and make sure the port is correct.

## Service patch and defense


1. The patch program needs to meet the judge’s system check requirements. Even though what the system check actually checks are not disclosed, it’s not too difficult to pass.
2. Program patch is modified using IDA. IDA provides three ways.
Patch: byte, word, assemble. The bytecode modification is easier to use. Because the byte-by-byte modification does not need to consider the assembly instructions, generally such modification changes are also very small, and are very easy to use in certain occasions. Although the modification of the assembly instruction level does not require modification of the bytecode, it also causes some inconvenience. For example, it is necessary to additionally consider the length of the assembly instruction, whether the structure is reasonable and complete, whether the logic is the same as the original, whether the modified assembly instruction is legal or not.
3. Remember to back up the original vulnerability program for patch analysis when using the patch program. When uploading a patch, you should delete the original vulnerability program, and then copy the patched program into it. After copying it, you need to give the program the appropriate permissions.
4. In the general game, the vulnerability program will have more than a dozen places to patch. Patches must not only be effective and reasonable, but also satisfy the analysis that can prevent or confuse opponents to a certain extent.


## Constructing a Script Framework to Quickly Launch an Attack


In the course of the offensive and defensive competition, a blood is particularly important. So having an attack script framework is very beneficial. Quickly develop attack scripts, you can maintain a dominant position in the early stage, and you can save time and take time to defend.


## Some strategies of the game


1. In the course of the game, it is not advisable to die on a single question. Due to the superiority of a blood, it is necessary to fully understand the difficulty of the game during the competition. First, analyze the ** simple question **, step by step.
2. During the competition, the two poles will be seriously differentiated. Efforts should be made to strike teams that are comparable to their own strengths and stronger than their own teams, especially if the scores are almost the same, and they must be strictly guarded against them.
3. NPC will send attack traffic from time to time during the game. The payload can be obtained from the attack traffic.
4. Be sure to fight the NPC to death.
5. At the beginning of the game, all the management passwords can be set to the same password, which is convenient for the player to log in and manage. Back up all the files in the initial stage for sharing within the team.
