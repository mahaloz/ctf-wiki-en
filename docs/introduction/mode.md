
## Problem Solving Mode - Jeopardy


The problem-solving type (Jeopardy) is a common format in online CTF competitions. In a Jeopardy CTF, the participating teams can participate through the Internet or the on-site network. The participating teams can participate through the Internet or the on-site network. Furthermore, teams can use the online environment to communicate and share files, solve technical challenges, and submit the answers to score points. Examples such as The International Collegiate Programming Contest, International Olympiad in Informatics, etc. The ranking is calculated by time of solve and total points.


What’s different in Jeopardy is that the first three teams that solve a challenge get rewarded with extra points. Generally, the first three solves are referred to as first blood, second blood, and third blood. This scoring format not only rewards teams who can solve the challenge quickly, but also shows teamwork through collaboration.


Of course, there is another popular way of scoring, where the number of points a challenge worth is determined by the number of teams that successfully solve the challenge. Initially, A challenge is given reward points. As more teams successfully solve a challenge, that challenge’s total points reward decreases. Lastly, the reward points will stop decreasing once a hits a threshold.


In CTF, topics mainly include these six categories **Web – Web Application Exploits and Defenses**, **RE - Reverse Engineering**, **Pwn - Binary Exploitation**, **Crypto - Cipher Attacks**, **Mobile - Mobile Security** and **Misc - Miscellaneous **


## War Sharing Mode - Belluminar


In the 2016 World Hacking Masters Challenge (WCTF), China was first introduced to the Belluminar CTF. Since then, Belluminar type of CTFs has been slowly popping up. In 2016, this type of competition has been seen in the XMan Summer Camp collected by Zhuge Jianwei and the Baidu Cup CTF Competition in September of the same year.


Here is the official Belluminar website: <http://belluminar.org/>


### Introduction to the Belluminar System


> Belluminar, hacking contest of POC, started at POC2015 in KOREA for the first time. Belluminar is from 'Bellum'(war in Latin) and 'seminar'. It is not a just hacking contest but a kind of

> festival consisted of CTF & seminar for the solution about challenges. Only invited teams can join Belluminar. Each team can show its ability to attack what other teams want to protect and can

> defend what others want to attack.



### Stage of Making the Challenges


> Each team is required to submit 2 challenges to the challenge bank.


First of all, each invited team must submit a question before the official competition. The teams will have 12 weeks to prepare the questions for the challenges. The score of the challenges made accounted for 30% of the total team score.


> Challenge 1: must be on the Linux platform;

>

> Challenge 2: No platform restriction(except Linux) No challenge type restriction (Pwn, Reverse...)



Traditional Belluminar systems require each team to make two challenges. One of the challenges must be in Linux, while the other has no  platform or challenge type restriction. Therefore, the team can show their skill and creativity.


In order to make the types of challenges more balanced, teams have to draw for their challenge type. This requires the team's skill level to be more comprehensive. In order to maintain balance, the two challenges might have different scores (For example, one might need to be the score of 200, while the other be the score of 100).


### Submitting a deployment


Before submitting the challenges, teams must submit a full document and a solve writeup for the challenges. The document must include the challenge name and score, challenge description, challenge creator, knowledge needed, and the source code of the challenge. However, the solve write-up only needs to include the operating environment, the full solving process, and the solve script/code.


After the topic is submitted, the organizer will test the title and the problem solving code. If there is a problem during the period, the responsible person of the question needs to cooperate to solve the problem. Finally deployed to the competition platform.


### During the Completion


After entering the competition, each team can request to solve the other team’s challenge. If they can’t solve the challenge, they will not get the First Blood reward. The ranking is based on the accumulated points earned on solved challenges; points earned from challenges account for 60% of the overall points.


### Share Discussion


After the game is over, the team rests and is ready to make a shared PPT (also ready for the problem stage). When sharing the meeting, each team sends 2
The team members took the stage to carry out the problem-solving ideas, the learning process and the sharing of knowledge points. After the presentation, enter the interactive discussion session, and the explanation representative needs to answer the questions raised by the judges and other players. There is not much time limit for commentary, but time usage is a criterion for scoring.


### Scoring rules


50% of the points (30% of the total score) are scored by the judges according to the level of detail submitted by the judges, the complete quality, the submission time, and the other 50% are scored according to the final problem after the game. Example of scoring formula: Score = MaxScore -- | N -- Expect_N |. Here N
It refers to the number of teams that solved the problem, and Expect_N is the number of questions that the problem is expected to solve. Only when the difficulty of the topic is moderate and the number of problem solving teams is closer to the expected number Expect_N, the higher the problem scores obtained by the problem team.


Problem solving points (60% of total points) are not considered for the First Blood award.


Sharing points (10%) are scored by judges and other teams based on their technical sharing (considering sharing time and other restrictions), and the average is calculated.


### General review of the system


In the system, Challenge&#39;s questions are handed over to the invited team, so that the team can do their best to each other. The difficulty and scope of the game will not be restricted by the organizer level, and the Challenge can also be improved.
The quality of each team can have different experiences and upgrades. In the &quot;sharing&quot; session, the team&#39;s topic is explained at the same time as it is deepening its ability level. The process of discussing the answer is a kind of thinking interaction. Can get a better understanding in the learning summary after the game.


## Attack and Defense Mode - Attack &amp; Defense


### Overview


Attack and defense mode is common in the offline finals. In the offensive and defensive mode, at the initial moment, all participating teams have the same system environment (including several services, which may be located on different machines), often called gamebox. The participating teams mine network service vulnerabilities and attack the opponent service to get the flag to score and repair. Defend your own service vulnerabilities to prevent deductions (of course, some games will set a score on the defense, and the general defense can only avoid losing points).


The offensive and defensive mode can reflect the game situation in real time through the score, and finally scores the winner directly. It is a fiercely competitive, highly ornamental and highly transparent network security system. In this system, it is not only more than the intelligence and skills of the players, but also more physical (because the game will generally last
48 hours), and also cooperate and cooperate with the division of labor between the teams.


The specific environment of the general competition will be given by the competition organizer one day before the start of the competition or half an hour before the start of the competition (a small page of several pages). During this time, you need to be familiar with the environment and defend against the documentation provided by the organizer.


Half an hour before the start of the game, it is impossible to attack within half an hour, and each team will step up to become familiar with the game network environment and prepare for defense. As for the IP address of the enemy Gamebox, you need to find it on your own given network segment.


If it is divided into two offensive and defensive games in the morning and afternoon, then the Gamebox vulnerability service will be replaced in the morning and afternoon (avoid the player exchange during the break), but the IP address to be used for management will not change. That is, ** will change the new question in the afternoon**.


Under normal circumstances, the organizer will provide the network cable, but the network cable interface will not be provided, so you need to bring your own. **


### basic rules


The general rules of attack and defense mode are as follows


- The team&#39;s initial score is x points
- The match takes 5/10 minutes as a round, and each round of the organizer will update the flag of the released service.
- Within each round, a service of a team is successfully attacked by a penetration (taken and submitted by Flag), and after deducting a certain score, the team that successfully attacked divides the points equally.
- Within each round, if the team is able to maintain their own services, the score will not decrease (if the defense is successful, the points will be added);
- If a service is down or an exception cannot pass the test, it may be deducted, and the normal team will split the points. Often service exceptions will deduct more points.
- If the services of all the teams in the round are abnormal, it is considered to be an irresistible factor and the scores are not reduced.
- Within each round, the service exception and the taken Flag can occur simultaneously, ie the team may deduct the superimposed scores for a single service within one round.
- Forbid the team to use the general defense method
- Please enter the team to back up all services at the beginning of the game. If the service is permanently damaged or lost due to its own reasons, it cannot be restored. The organizer does not provide reset service.
- It is forbidden to attack the competition platform other than the competition, including but not limited to the root of the gamebox, the use of the host platform vulnerability, etc., the offender immediately cancels the qualification
- If the team finds violations of other teams, please report them immediately and we will strictly review and make corresponding judgments.


### Web environment


The document will generally have a network topology map of the game environment** (as shown below), each team will maintain a number of **Gamebox (self-server)**, there are vulnerable services deployed on the Gamebox.


![Offensive and defensive mode network topology] (./images/network.jpg)


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
