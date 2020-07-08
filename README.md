# DevOps

## Four pillars of DevOps
- Ease of use: everyone on the team will use this, which is why documentation is important.
- Flexibility: things change at incredible rate, you don't want to change that fast but adapt accordingly.
- Robustness: we need 100% uptime, fast and robust deployment
- Cost: cost of downtime, cost of slow innovation, cost of time to market, cost of infrastructure

## Bare Metal Mainframes
- your computer = your problem
- from planning, to serving, maintaining, securing, resourcing, setting up - everything except producing 

## IaaS
Infrastructure As A Service

- rent out the computing and storage power you need
- shared responsibility model: service provider has the responsibility of securing and maintaining the cloud - you have to do the security in the cloud. 
- rent out by the second, increase as you grow, consume only what you need
- technical knowledge of how to build systems needed
- only mental renter per second 
- i.e. AWS, Alibaba Cloud, Microsoft Azure

## PaaS
Platform As A Service

- built on top of IaaS
- you still need some technical know-how
- has a better graphical interface
- relatively more expensive per second
- depends on the cost of maintenance
- less control more vendor lock-in
- i.e. Heroku


## SaaS
Software As A Service

- highest level of abstraction
- the pure version means: no donwloads, no CDs or physical install
- all happens in the cloud
- access via browser or API
- if we need to download this means we will need to update and expose our sw to a different environment

The way we develop has changed, it is no longer as hierarchical with Agile and the ability of having software integrated which means that the sprint is shorter, it can be pushed/go live quicker, and the feedback loops are stronger.

## Environments
An environments is a location where code runs and data lives.

Github is not an environment really, maybe Github pages.

Your machine is an environment because code runs and you develop software and web apps and other apps.

What environments are there?
- Developments:
    - where you write your code, Py, Sql, Html - i.e. computer
- Testing:
  - external, has its own tools and infrastructure that runs the code
- Production:

Code pipelines: move between the environments.
Testing: ensures functionality and quality of the website.
Objective: increase speed of learning and developing -> increase feedback loops -> increase innovation.

"It's working on my computer" - this is the main issue in DevOps, to avoid this you must standardise the environment.


## pbm in development - standardise virtual environment
Develop a culture of DevOps: giving them ownership of their pipelines and that everyone in the organisation understands why we are doing things.

Tests - make sure that whatever you are creating is itself a standardised environment.

## pbm in operations - don't always receive code, power, electricity - has its own operational issues, you have to buy them and maintain them


## Node
- can mean an instance, a machine but in this case it means JS

Reidrect streams
3 streams in Linux

standard input keyboard
standard output what the application has
standard error - error application has

Use stre-redirection to redirect a stream and create a file from scratch
 i.e.: echo 'hello world' through command line into directory - when the command line returns it it is a standard output
To redirect:
i.e. echo 'hello world' > testfile.txt (file doesn't exist but it will be created)
There is no output in command line because it had been redirected.
You can use cat, i.e. cat testfile.txt to see the output.

To append content:
i.e. echo 'hello world' >> testfile.txt

## Links

These are shortcuts :

## Soft Links (symbolic links)
- syntax : ln -s
You can make links to files and directories, and you can create links (shortcuts) on different partitions and with a different inode number than the original.

If the real copy is deleted, the link will not work.

## Hard Links
- syntax: ln /scripts/firefox /scripts/on-fire
       ( Source )    ( Destination )
Hard links are for files only; you cannot link to a file on a different partition with a different inode number.

If the real copy is deleted, the link will work, because it accesses the underlying data which the real copy was accessing.

## Permissions

- syntax: ls -l

This will show the current permissions for files and folders.
The output will resemble:
-rwxr--rw- 1 user user 0 Jan 19 12:59 file1.txt
