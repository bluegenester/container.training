# Orchestration at Scale with Docker

This is the material for the "Docker orchestration workshop"
written and delivered by Jérôme Petazzoni (and possibly others)
at multiple conferences and events like:

- QCON, New York City (2015, June)
- KCDC, Kansas City (2015, June)
- JDEV, Bordeaux (2015, July)
- OSCON, Portland (2015, July)
- StrangeLoop, Saint Louis (2015, September)
- LISA, Washington D.C. (2015, November)
- SCALE, Pasadena (2016, January)
- Zenika, Paris (2016, February)
- Container Solutions, Amsterdam (2016, February)

## Content

- Chapter 1: Getting Started: running apps with docker-compose
- Chapter 2: Scaling out with Swarm Mode
- Chapter 3: Operating the Swarm (networks, updates, logging)
- Chapter 4: Deeper in Swarm (stateful services, scripting, DAB's)

## How This Repo is Organized

- **dockercoins**
  - Sample App: compose files and source code for the dockercoins sample apps
  used throughout the workshop
- **docs**
  - Slide Deck: presentation slide deck, works out-of-box with GitHub Pages,
  uses https://remarkjs.com
- **prepare-local**
  - untested scripts for automating the creation of local virtualbox VM's
  (could use your help validating)
- **prepare-vms**
  - scripts for automating the creation of AWS instances for students

## Slide Deck

- The slides are in the `docs` directory.
- To view them locally open `docs/index.html` in your browser. It works
  offline too.
- To view them online open https://jpetazzo.github.io/orchestration-workshop/
  in your browser.
- When you fork this repo, be sure GitHub Pages is enabled in repo Settings
  for "master branch /docs folder" and you'll have your own website for them.
- They use https://remarkjs.com to allow simple markdown in a html file that
  remark will transform into a presentation in the browser.

## Sample App: Dockercoins!

The sample app is in the `dockercoins` directory. It's used during all chapters
for explaining different concepts of orchestration.

To see it in action:

- `cd dockercoins && docker-compose up -d`
- this will build and start all the services
- the web UI will be available on port 8000

## Running the Workshop

### General timeline of planning a workshop

- Fork repo and run through slides, doing the hands-on to be sure you
  understand the different `dockercoins` repo's and the steps we go through to
  get to a full Swarm Mode cluster of many containers. You'll update the first
  few slides and last slide at a minimum, with your info.
- Your docs directory can use GitHub Pages.
- This workshop expects 5 servers per student. You can get away with as little
  as 2 servers per student, but you'll need to change the slide deck to
  accommodate. More servers = more fun.
- If you have more then ~20 students, try to get an assistant (TA) to help
  people with issues, so you don't have to stop the workshop to help someone
  with ssh etc.
- AWS is our most tested process for generating student machines. In
  `prepare-vms` you'll find scripts to create EC2 instances, install docker,
  pre-pull images, and even print "cards" to place at each students seat with
  IP's and username/password.
- Test AWS Scripts: Be sure to test creating *all* your needed servers a week
  before workshop (just for a few minutes). You'll likely hit AWS limits in the
  region closest to your class, and it sometimes takes days to get AWS to raise
  those limits with a support ticket.
- Create a https://gitter.im chat room for your workshop and update slides
  with url. Also useful for TA to monitor this during workshop. You can use it
  before/after to answer questions, and generally works as a better answer then
  "email me that question".
- If you can send an email to students ahead of time, mention how they should
  get SSH, and test that SSH works. If they can `ssh github.com` and get
  `permission denied (publickey)` then they know it worked, and SSH is properly
  installed and they don't have anything blocking it. SSH and a browser are all
  they need for class.
- Typically you create the servers the day before or morning of workshop, and
  leave them up the rest of day after workshop. If creating hundreds of servers,
  you'll likely want to run all these `trainer` commands from a dedicated
  instance you have in same region as instances you want to create. Much faster
  this way if you're on poor internet. Also, create 2 sets of servers for
  yourself, and use one during workshop and the 2nd is a backup.
- Remember you'll need to print the "cards" for students, so you'll need to
  create instances while you have a way to print them.

### Things That Could Go Wrong

- Creating AWS instances ahead of time, and you hit its limits in region and
  didn't plan enough time to wait on support to increase your limits. :(
- Students have technical issues during workshop. Can't get ssh working,
  locked-down computer, host firewall, etc.
- Horrible wifi, or ssh port TCP/22 not open on network! If wifi sucks you
  can try using MOSH https://mosh.org which handles SSH over UDP. TMUX can also
  prevent you from loosing your place if you get disconnected from servers.
  https://tmux.github.io
- Forget to print "cards" and cut them up for handing out IP's.
- Forget to have fun and focus on your students!

### Creating the VMs

`prepare-vms/trainer` is the script that gets you most of what you need for
setting up instances. See
[prepare-vms/README.md](prepare-vms)
for all the info on tools and scripts.

### Content for Different Workshop Durations

With all the slides, this workshop is a full day long. If you need to deliver
it in shorter timelines, here's some recommendations on what to cut out. You
can replace `---` with `???` which will hide slides. Or leave them there and
add something like `(EXTRA CREDIT)` to title so students can still view the
content but you also know to skip during presentation.

#### 3 Hour Version

- Limit time on debug tools, maybe skip a few. *"Chapter 1:
  Identifying bottlenecks"*
- Limit time on Compose, try to have them building the Swarm Mode by 30
  minutes in
- Skip most of Chapter 3, Centralized Logging and ELK
- Skip most of Chapter 4, but keep stateful services and DAB's if possible
- Mention what DAB's are, but make this part optional in case you run out
  of time

#### 2 Hour Version

- Skip all the above, and:
- Skip the story arc of debugging dockercoins all together, skipping the
  troubleshooting tools. Just focus on getting them from single-host to
  multi-host and multi-container.
- Goal is first 30min on intro and Docker Compose and what dockercoins is,
  and getting it up on one node in docker-compose.
- Next 60-75 minutes is getting dockercoins in Swarm Mode services across
  servers. Big Win.
- Last 15-30 minutes is for stateful services, DAB files, and questions.


# Problems? Bugs? Questions?

If there is a bug and you can fix it: submit a PR.
Make sure that I know who you are so that I can thank you
(because you're the real MVP!)

If there is a bug and you can't fix it, but you can
reproduce it: submit an issue explaining how to reproduce.

If there is a bug and you can't even reproduce it:
sorry. It is probably an Heisenbug. I can't act on it
until it's reproducible.

if you have attended this workshop and have feedback,
or if you want us to deliver that workshop at your
conference or for your company: contact me (jerome
at docker dot com).

Thank you!
