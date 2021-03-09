
## Problem Solving Mode - Jeopardy


The problem-solving type (Jeopardy) is a common format in online CTF competitions. In a Jeopardy CTF, the participating teams can participate through the Internet or the on-site network. Furthermore, teams can use the online environment to communicate and share files, solve technical challenges, and submit the answers to score points.


What’s different in Jeopardy is that the first three teams that solve a challenge get rewarded with extra points. Generally, the first three solves are referred to as first blood, second blood, and third blood. This scoring format not only rewards teams who can solve the challenge quickly, but also shows teamwork through collaboration.


Of course, there is another popular way of scoring, where the number of points a challenge worth is determined by the number of teams that successfully solve the challenge. Initially, A challenge is given reward points. As more teams successfully solve a challenge, that challenge’s total points reward decreases. Lastly, the reward points will stop decreasing once a hits a threshold.


In CTF, topics mainly include these six categories **Web – Web Application Exploits and Defenses**, **RE - Reverse Engineering**, **Pwn - Binary Exploitation**, **Crypto - Cipher Attacks**, **Mobile - Mobile Security** and **Misc - Miscellaneous **


## War Sharing Mode - Belluminar


In the 2016 World Hacking Masters Challenge (WCTF), China was first introduced to the Belluminar CTF. Since then, Belluminar type of CTFs has been slowly popping up. In 2016, this type of competition has been seen in the XMan Summer Camp by Zhuge Jianwei and the Baidu Cup CTF Competition in September of the same year.


Here is the official Belluminar website: <http://belluminar.org/>


### Introduction to the Belluminar System


> Belluminar, hacking contest of POC, started at POC2015 in KOREA for the first time. Belluminar is from 'Bellum'(war in Latin) and 'seminar'. It is not a just hacking contest but a kind of

> festival consisted of CTF & seminar for the solution about challenges. Only invited teams can join Belluminar. Each team can show its ability to attack what other teams want to protect and can

> defend what others want to attack.



### Stage of Making the Challenges


> Each team is required to submit 2 challenges to the challenge bank.


First, each invited team must submit a question before the official competition. The teams will have 12 weeks to prepare the questions for the challenges. The score of the challenges made accounted for 30% of the total team score.


> Challenge 1: must be on the Linux platform;

>

> Challenge 2: No platform restriction(except Linux) No challenge type restriction (Pwn, Reverse...)



Traditional Belluminar systems require each team to make two challenges. One of the challenges must be in Linux, while the other has no platform or challenge type restriction. Therefore, teams can show their skill and creativity.


In order to make the types of challenges more balanced, teams have to draw for their challenge type. This requires the team's skill level to be more comprehensive. In order to maintain balance, the two challenges might have different scores (For example, one might need to be the score of 200, while the other be the score of 100).


### Submitting Challenges


Before submitting the challenges, teams must submit a full document and a solve writeup for the challenges. The document must include the challenge name and score, challenge description, challenge creator, knowledge needed, and source code of the challenge. However, the solve write-up only needs to include the operating environment, full solving process, and solve script/code.


After the challenges are submitted, the organizers will test the challenges and code. If issues are found, the person responsible for the challenge must help to solve the problems. Then, the challenges can be put on the competition platform.


### During the Competition


After entering the competition, each team can request to solve the other team’s challenge. If they can’t solve the challenge, they will not get the First Blood reward. The ranking is based on the accumulated points earned by solving the challenges; points earned from challenges account for 60% of the overall points.


### Share Discussion After the Competition


After the game is over, the team rests and creates PowerPoints (can also be done in the challenge creation phase). During the sharing meeting, each team sends two members to share their intended solutions, learning process, knowledge points, etc. Once the presentative is over, open discussion begins. The two team representatives must answer questions from other players or judges. While they don’t have a time limit on answering questions, however, the time used is a variable in the scoring process.


### Scoring Rules


Scores from creating challenges (30% of overall score) – 50% of the points are based on the level of details, completion, submit time, and the other 50% of the points coms from solved challenges.
The formula is as follows: Score = MaxScore -- | N -- Expect＿N |
N is the number of teams that solved this challenge.
Expect＿N is the number of teams expected to solve this challenge.
Only when the challenge’s difficulty is balanced, the number of teams solved this challenge will be closer to the number of teams expected to solve this challenge, the challenge’s creator will earn more points.

Score from solving challenges (60% of overall score) – First Blood is not included in the calculation.

Score from sharing – (10% of overall score) – Scores based on the content during the sharing meeting voted by players and judges (account for the time taken and other restrictions), will be calculated as an average.


### Thoughts on the Belluminar System


The Belluminar system handed over the responsibility of creating challenges to the invited teams, where each team do their best to create challenges for each other. The difficulty and scope of the competition will not be restricted by the organizer, so the quality of the challenges will improve. The “Sharing” phase allows each team to explain their challenges. The open discussion process enables the sharing of creative ideas/methods. The “Sharing” phase after the competition is a great way for others players to learn.


## Attack and Defense Mode - Attack &amp; Defense


### Overview


The finals of Attack and Defense competitions are usually done offline. In Attack and Defense mode, teams will use the same system environment, often referred to as the “Gamebox”. On the attacking side, teams need to discover vulnerabilities on services running on the opponent’s machine, then exploit them to score by obtaining the flag. On the defending side, teams need to patch existing vulnerabilities to stop losing points (usually defending and patching are the only way to stop losing points, of course, in some competitions successful defending can be rewarded with points).


An Attack and Defend competition not only tests the team’s technical skills but also tests the players' body (since most competitions last about 48 hours). At the same time, team members need to split up the tasks and work together on solving different problems.


Usually, the competition organizer will disclose the details on the requirements 30 minutes or 1 day before the competition. During that time, you cannot attack. You need to get familiar with the given environment and prepare to defend based on the given requirements. You will need to discover the opponent Gamebox’s IP address using the given subnet.

If the two Attack and Defend sessions are between morning and afternoon, then the vulnerable services will get changed (in case players talk about them during the break). However, the IP address and what will not change.

Normally, the organizer will provide ethernet cables, but not ethernet adopters.


### Basic Rules


The general rules of attack and defense mode are as follows


- The teams will start with x points
- During each round, the organizer will update which service contains the released flag.
- During each round, if a team’s vulnerable service and the attacker obtained the flag via the vulnerable service, then the team will lose some points and the attacker will gain some points.
- During each round, if a team can keep the its services running normally, then that team won’t lose points. (if defended successful, the points will be rewarded)
- If a team’s service goes down, then the team will lose points, which distributed to teams that had their service running normally. Often, service downtime and errors will result in more deduction of points.
- If all teams’ service goes down during a round and it is determined to be unavoidable. Then, no points will be deducted.
- During each round, if a service goes down and a team gets the flag, the team responsible for the service may get deduct double the points.
- The uses of general defense methods are forbidden.
The participating teams should backup all services before the competition. If a service gets lost or damaged, the organizer will not restore it.
- It is forbidden to attack the competition platform, including but not limited obtaining root in Gameebox. The offender immediately banned from the competing.
- If the team finds violations of other teams, please report them immediately and we will strictly review and make corresponding judgments.


### Network Environment


The document will usually include a **network topology map** (as shown below), each team will maintain some Gamebox (one’s own server), there are vulnerable services deployed on the Gamebox.


![attach and defend mode network topology map] (../images/network.jpg)


The document will include the environment of the players, the offensive and defensive environment, and the organizers.


Players need to be configured on a PC or automatically acquired by DHCP


- IP address
- Gateway
- Mask DNS server address


Offensive and defensive environment


- The address of the Gamebox, including the address of the party and other teams.
- The game usually provides a mapping table of the team&#39;s id and corresponding ip so that the player can specify the appropriate attack and defense strategy.

Organizer environment


- Competition answer platform
- Submit flag interface
- Traffic access interface


### Visit Gamebox


The way the team logs in to the gamebox is given in the entry document, generally as follows


- Username is ctf
- The private key is usually given by ssh login, password or private key.


Naturally, all default passwords should be modified after logging in to the team machine, and weak passwords should not be set.
