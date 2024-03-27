# PASSING CKAD

This repository contains information about how I prepared and cleared the CKAD exam end of March 2024. Hopefully it also gives some insight into what it takes to pass the exam.

## About the exam

The exam is hands-on in an Ubuntu terminal. The exam environment is very locked down. You have access to a FireFox browser from within the exam environment and that's it.

From within FireFox you are allowed to use these two soucres:
https://kubernetes.io/docs
https://helm.sh

### Use Ubuntu Terminal as much as possible

It cannot be stressed enough. The exam is in Ubuntu terminal so that is where you need to excel. Practice using the terminal as much as possible.
If coming from Windows, consider using WSL2 as much as possible. Consider setting Ubuntu terminal as your default terminal in Windows terminal 

### Use short names for Kubernetes resources

Get used to using short names for Kubernetes resources. They are easier and faster to type. During the exam and in real life. 
If you use the amazing k9s CLI (https://k9scli.io/) you can also use the short names in that tool (k9s is not allowed during the exam).

The short names for various Kubernetes resources can be seen by running: 
kubectl api-resources

### Learn how to navigate kubernetes.io/docs quickly

Learn how to navigate kubernetes.io/docs and find whatever you need quickly. There is a search input field in the upper left part of the landing page.
If I searched for specific yaml snippets I'd often search for 'kind: <object-type>' and then put it on the paste board for re-use when I got to the relevant page, so
I didn't have to scroll through the page

### Use aliases

Use aliases for the kubectl commands you use the most. This will save time and keystrokes. I found simple aliases worked best for me. 

Strictly speaking not an alias. I also exported an environment variable 'do' so I could type $do instead of '--dry-run=client -o yaml':
export do="--dry-run=client -oyaml"

You can see defined aliases using the 'alias' command.

### Don't write yaml by hand

Don't write yaml by hand! It is too slow and too error-prone!

Either copy from kubernetes.io/docs or generate via imperative commands like:
kubectl run <pod-name> --image=<image-name> --oyaml --dry-run=client -n <namespace> (optionally configure env vars via --env=<var1>=<val1 and labels via -l=label1=value1)>p.yml
with the aliases I used, the above command would be:
kr <pod-name> --image=<image-name> $do -n <namespace> >p.yml (plus optionally parameters - significantly shorter and faster than writing the full commands)
The other command I used again and again was
kubectl create <object-type> <object-name> -n <namespace> >x.yml (plus optionally parameters passed in). This way you can quickly create yaml for configmaps, secrets, deployments, cronjobs, jobs, ingresses
with alias it would be
kc <object-type> <object-name> -n <namespace> > x.yml (where x represents a one to three letter trained short object form. For instance d for deployment cj for cronjob etc.
Check 'kubectl create -h' for supported object types that can be created this way 
Once you have the yaml, it can quickly be applied using kubectl create or kubectl apply commands. I used these aliases:
kc -f x.yml
ka -f x.yml

### Use kubectl explain

Become familiar with "kubectl explain <object-type>", "kubectl explain <object-type>.<field>", "kubectl explain <object-type> --recursive". 
The latter one can be super useful when piped to grep -i -C <context-lines>. 
In some cases it is faster checking yaml structure or supported values for specific fields than searching on kubernetes.io/docs. 

### Know how to navigate current line in the terminal

Know CTRL+a brings you to the start of a line in terminal
Know CTRL+e brings you to the end of a line in terminal
CTRL+ left/right arrow scrolls per word versus per character

It can save a bit of time and feels a bit more agile than using the left/right arrow keys

### Know how to put a running process in the background

Know CTRL+z puts a process in the background in terminal and that you can bring it back via 'fg' (I assume it stands for foreground)).
This is useful when running a command that takes more than a few seconds to process. 
By putting the process in the background you can start typing on the next command and then retrieve the background command using 'fg' a bit later.
Again, it saves a bit of time.

### Become decent at either vi or nano

Become decent at working with with vi or nano. You only have these two editors in the exam environment. It is also useful in real life. I went all-in and learnt to use vi decently.
If you consider using vi and are new to that editor I'll recommend using vimtutor. I think most Linux systems have vimtutor pre-installed. Just type vimtutor in the terminal and spend an hour learning the basics.

### Consider using tmux

Tmux is a terminal multiplexer. It enables you to split the terminal in multiple panes and windows. It is pre-installed and allowed at the exam. I like using it in real life, but did not use it during the exam. 
It complicates output, coloring and copy-paste behavor in the exam scenario, so I chose not to use it during training and exam.

### Know how to use grep

Become familiar with grep (-i,-R options especially)

### Become familiar with common short form arguments to kubectl

Become familiar with general short form arguments to kubectl. Use -h instead of --help. Use -A installd of --all.

### Become familiar with less and tree

Not a must. But I find less and tree to be useful in the terminal. Less is more flexible than cat. Tree is useful to quickly visualize a folder structure in the terminal.

### Consider using flashcards

Consider using flashcards to memorize various things. I made the ones below to ensure I trained and memorized things I bumped into I didn't know and found relevant to remember.
I used the free option from cram.com and made the flashcards public:

https://www.cram.com/flashcards/ckad-13709656
https://www.cram.com/flashcards/helm-13716537
https://www.cram.com/flashcards/kubectl-13168712



The majority of my preparation I spent watching videos and doing labs via:
https://kodekloud.com/courses/certified-kubernetes-application-developer-ckad/
I used a spreadsheet with date and subject rehearsed as well as how long it took to do the lab.
I made notes in the spreadsheet when something was challenging and kept revisiting until the topic was easy
I prioritized labs over videos. Not sure I saw all videos.

When I had a decent all-round proficiency I moved on to do mock exams from this site:
https://kodekloud.com/lessons/certified-kubernetes-application-developer-mock-exam-series/
These are  mock exams with 20 random questions. One mock exam is meant to take 2 hours. I wanted to rehearse smaller chunks often as that fitted my schedule best.
So I did 5 questions some days, 10 some days and some days an entire set. Many days I skipped due to work or private stuff..:-) 
I kept track of number of questions and how well I did in the beforementioned spreadsheet. One major difference between the kodekloud mock exams and the real exam and killer.sh sessions is the way passing percentage is calculated. Kodekloud mock exams have 20 questions typically devided into 2-5 parts. If you get just one of these wrong it will count the entire question as failed. In the real exam it is granular. You get points for each part. So in that way the real exam is a bit easier than getting the kodekloud mock exams right. 
When I started passing I started thinking about the last month of exam prep. When buying the exam slot, you get 2 sessions on https://killer.sh with access for 36 hours.
Killer.sh is a CKAD exam simulator that most accurately resembles the real exam environment. You want to practice in the environment, so you know how to copy/paste, switch between windows (terminal and FireFox browser primarily). Especially if you are coming from Windows.
For instance I didn't know how to maximize FireFox so first time I did a test exam I could only partially view the kubernetes.io/docs page. Subsequently I found ALT + F10 was the solution (maximize window) (or F11 for full-screen).
My exam plan and execution looked like this:
17 days before exam: booked exam slot
15 days before exam: did my first 36 hour killer.sh session. I did the exam set 4 times over two days and reviewed challenging topics. Status and percentage in my spreadsheet.
14 days to 3 days before exam: I practiced 7 times on topics that were still challenging. My first killer.sh session showed I needed to get faster. I optimized my alias usage for more speed.
2 days before exam: I did my second 36 hour killer.sh session. I did two two-hour exam sessions and they went well. I scored 90/113 and 101/113. 
1 day before exam: Relaxed. thought about other things. Spent time with family. At this point I believe you have to trust your preparation and so I tried. 
Exam day: I booked exam Sunday morning at 10. The room has to be meticously stripped from personal belongings. I was asked to show the proctor the back of my screen. The backside of my keyboard and laptop. Had to explain what the silver grey thing connected to my laptop was (it was my USB hub I needed because my laptop only has 2 USB ports and I need ports for keyboard, mouse and web cam). Remove label from my water bottle. Show what was under my desk (nothing).

Finally the exam started. It felt challenging and stressful despite my preparation, but I managed to do all questions fully except one regarding ingresses I couldn't get my head around. I think I did the ingress one partially and might have scored a few points on that as well. 

Realizations after my exam:
I think I would do better if I arrived earlier at the exam location earlier. 2 hours is probably ideal. I arrived half an hour before exam start and needed to setup equipment, get my ID approved etc. Not optimal.
Consider if you do best in the morning or later during the day. I think I work better in the afternoon, so I could maybe have done better if I had scheduled a slot in the afternoon. 

https://killercoda.com/ (CKAD section - free)
https://killer.sh/

Research when you bump into behavior that surprices you. For instance I couldn't understand why 'kg secret -oyaml' gave a different result than 'kd secret'. I asked ChatGPT about the differences and got a great explanation I could verify subsequently. Turns out, 'k describe secret' implicitly base64 decodes, which 'k get secret' does not. Good to know!


