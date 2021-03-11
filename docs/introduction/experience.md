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
2. Use IDA to modify the patch program. IDA provides 3 ways to patch: byte, word, assemble. The byte method is easy to use since you don’t need assembly instructions. Generally, such modification is also very small and efficient. Assembly instruction-level modifications, while convenient without the need to modify the bytecode, can also cause some inconvenience. For example, having to worry about the length of the assembly instruction, if the structure is complete, and whether the logic and modified instruction are correct, etc.
3. Remember to back up the vulnerable program before the patch for team analysis. Before updating the patch, remove the vulnerable program. Then, copy the patch and give it proper permissions.
4. In general, there are around ten locations that need to patch in the vulnerable program.
The patch should not only be effective but also add protection or confusion to your opponent's analysis


## Use a Script to Attack Quickly


Fast attack scripts can maintain the advantage position in the early stage. At the same time getting points and saving time for defending.


## Some Tricks Used in the Competition


1. During the competition, don’t spend too long on a single question. Because of the advantage you get for obtaining First Blood, you should understand the overall difficulty of challenges. **Start from the easier question** and work your way up.
2. During the competition, you should try to attack teams that are similar or above your skill level. especially if they have around the same score as your team. Remember to buff up your defense.
3. During the competition, NPC (non-player characters) will randomly send your attack traffic. In the attack traffic, the payload can be obtained.
4. Be sure to attack the NPC.
5. At the beginning of the competition, you can change all the passwords to one password. That way, it’s easier to share and use. Also, back up all the files given and share them with the team.
