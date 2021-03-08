Welcome to the **CTF Wiki**.

**CTF** (Capture The Flag) is originated in the 1996 **DEFCON** Global Hacking Conference, a competitive game among cybersecurity enthusiasts.


The **CTF** competition covers a wide range of fields and has a complex content. At the same time, the development of security technology is getting faster and faster, and the difficulty of **CTF** is getting higher and higher, the threshold for beginners is getting higher and higher. Most of the online information is scattered and trivial. Beginners often don&#39;t know how to systematically learn the knowledge of **CTF** related fields, often taking a lot of time and suffering.


In order to make the **CTF** players life of entering this field easier, in October 2016, **CTF Wiki** had the first commit on Github. As content continues to improve, the **CTF Wiki** has been loved by more and more security enthusiasts, and there are also a lot of friends who have never met participating in this project.


As a free site, with the recent years' **CTF** challenges, **CTF Wiki** introduces the knowledge and techniques in all directions of **CTF** to make it easier for beginners to learn how to getting started at playing **CTF**.


At present, **CTF Wiki** mainly contains the basic knowledge of **CTF** in all major directions, and is working hard to improve the following contents.


- Advanced knowledge in the CTF competition
- Quality topics in the CTF competition


For more information on the above, see the [Projects] (https://github.com/ctf-wiki/ctf-wiki/projects) of the CTF Wiki for a detailed list of what is being done and what to do.


Of course, the **CTF Wiki** is based on **CTF**, but it is not limited to **CTF**. In the future, **CTF Wiki** will


- Introducing tools in security research area
- More integration with security area


In addition, given the following two points


- Technology should be shared in an open manner.
- Security offensive and defensive technologies are always up to date, and old technologies may fail at any time in the face of new technologies.


**CTF Wiki** will never publish books.


Finally, the **CTF Wiki** originates from the community, as an independent organization**, advocates **freedom of knowledge**, will never be commercialized in the future, and will always remain **independent and freedom**.


## How to build？



This document is currently deployed at [https://ctf-wiki.github.io/ctf-wiki/] (https://ctf-wiki.github) using [mkdocs](https://github.com/mkdocs/mkdocs) .io/ctf-wiki/). Of course, it can also be deployed locally, as follows:


```shell

# 1. clone

git clone git@github.com: ctf-wiki / ctf-wiki.git
# 2. requirements

pip install -r requirements.txt

# generate static file in site/

mkdocs build

# deploy at http://127.0.0.1:8000

mkdocs serve

```



**mkdocs Locally deployed websites are dynamically updated, i.e. when you modify and save the md file, refreshing the page and the contents will be dynamically updated. **




Just want to browse locally, don&#39;t want to modify the document? Try Docker!
```

docker run -d --name=ctf-wiki -p 4100:80 ctfwiki/ctf-wiki

```

You can then access the CTF Wiki by visiting [http://localhost:4100/] (http://localhost:4100/) in your browser.


## How to practice？



First, you can learn some basic security knowledge by reading online.


Second, the CTF Wiki has two accompany projects.


- The challenges mentioned in the CTF Wiki are in the [ctf-challenges] (https://github.com/ctf-wiki/ctf-challenges) repository, so look for them according to the corresponding category.
- Note: There are still some challenges that are currently being migrated. . . (misc, web)
- The tools involved in the CTF Wiki are constantly being added to the [ctf-tools](https://github.com/ctf-wiki/ctf-tools) repository.
