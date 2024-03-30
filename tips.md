## Tips

This page contains tips on how to prepare for the CKAD exam.<br><br>

From within FireFox you are allowed to use these the few sources mentioned here: <br>
https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad

### Use Ubuntu Terminal as much as possible

It cannot be stressed enough. The exam is in Ubuntu terminal so that is where you need to excel. Practice using the terminal as much as possible.
If coming from Windows, consider using WSL2 as much as possible. Consider setting Ubuntu terminal as your default terminal in Windows terminal 

### Use short names for Kubernetes resources

Get used to using short names for Kubernetes resources. They are easier and faster to type. During the exam and in real life. 
If you use the amazing k9s CLI (https://k9scli.io/) you can also use the short names in that tool (k9s is not allowed during the exam).

The short names for various Kubernetes resources can be seen by running: <br><br>
```kubectl api-resources```

### Learn how to navigate kubernetes.io/docs quickly

Learn how to navigate kubernetes.io/docs and find whatever you need quickly. There is a search input field in the upper left part of the landing page.
If I searched for specific yaml snippets I'd often search for 'kind: <object-type>' and then put it on the paste board for re-use when I got to the relevant page, so
I didn't have to scroll through the page

### Use aliases

Use aliases for the kubectl commands you use the most. This will save a lot of time and keystrokes. I found simple aliases worked best for me. 

See more on [aliases](aliases.md) and which ones I used here.

### Don't write yaml by hand

Don't write yaml by hand! It is too slow and too error-prone!

Either copy from https://kubernetes.io/docs or generate via imperative commands like:<br><br>
```kubectl run <pod> --image=<image> --oyaml --dry-run=client -n <namespace> >p.yml```<br> <br>
or with labels and environment variables added:<br><br>
```kubectl run <pod> --image=<image> --oyaml --dry-run=client -n <namespace> --env=<var1>=<val1> -l=label1=value1)>p.yml``` <br><br>
with the aliases I used, the above command would become:<br><br>
```kr <pod> --image=<image> $do -n <namespace> --env=<var1>=<val1> -l=label1=value1)>p.yml``` <br>

significantly shorter and faster than typing the full commands.<br>

The other command I used again and again was <br><br>
```kubectl create <object-type> <object-name> -n <namespace> >x.yml```<br><br>
This way you can quickly create yaml for configmaps, secrets, deployments, cronjobs, jobs, ingresses
with alias it would be something like the below depending on <object-type><br><br>
```kc <object-type> <object-name> -n <namespace> > x.yml``` <br><br>
where x represents a one to three letter trained short object form. For instance d for deployment cj for cronjob etc.
Check 'kubectl create -h' for supported object types that can be created this way 
Once you have the yaml, it can quickly be applied using kubectl create or kubectl apply commands. I used these aliases to do that: <br><br>
```kc -f x.yml```<br><br>
```ka -f x.yml```<br>

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

https://www.cram.com/flashcards/ckad-13709656 <br>
https://www.cram.com/flashcards/helm-13716537 <br>
https://www.cram.com/flashcards/kubectl-13168712

### Research and experiment when something works unexpectedly

Research when you bump into behavior that surprices you. <br><br>
For instance I couldn't understand why 'kg secret -oyaml' gave a different result than 'kd secret'. More specifically why the token part in 'kubectl get secret <secret> -o jsonpath='{.data.token}' gave a different result than 'kubectl describe secret <secret>' I asked ChatGPT about the differences and got a great explanation I could verify subsequently. Turns out, 'k describe secret' implicitly base64 decodes, which 'k get secret' does not. Good to know!

### Do a lot of lab exercises

The majority of my preparation I spent watching videos and doing labs via:<br><br>
https://kodekloud.com/courses/certified-kubernetes-application-developer-ckad/<br>
I used a spreadsheet with date and subject rehearsed as well as how long it took to do the lab.
I made notes in the spreadsheet when something was challenging and kept revisiting until the topic was easy
I prioritized labs over videos. Not sure I saw all videos.

### Do mock exams

When I had a decent all-round proficiency I moved on to do mock exams from this site:<br><br>
https://kodekloud.com/lessons/certified-kubernetes-application-developer-mock-exam-series/ <br><br>
These are  mock exams with 20 random questions. One mock exam is meant to take 2 hours. I wanted to rehearse smaller chunks often as that fitted my schedule best.<br><br>
So I did 5 questions some days, 10 some days and some days an entire set. Many days I skipped due to work or private stuff..:-) <br><br>
I kept track of number of questions and how well I did in the beforementioned spreadsheet. <br><br>One major difference between the kodekloud mock exams and the real exam and killer.sh sessions is the way passing percentage is calculated. Kodekloud mock exams have 20 questions typically devided into 2-5 parts. If you get just one of these wrong it will count the entire question as failed. In the real exam it is granular. You get points for each part. So in that way the real exam is a bit easier than getting the kodekloud mock exams right. <br><br>
When I started passing I started thinking about the last month of exam prep. 

### Do killercoda.com exercises

Do the CKAD section on https://killercoda.com/. The challenges are short, so they don't take long to do. They get around various topics pretty well and they are free. 

### Do killer.sh sessions 

When buying the exam slot, you get 2 sessions on https://killer.sh with access for 36 hours.
Killer.sh is a CKAD exam simulator that most accurately resembles the real exam environment. You want to practice in the environment, so you know how to copy/paste, switch between windows (terminal and FireFox browser primarily). Especially if you are coming from Windows.

For instance I couldn't figure out how to maximize FireFox (as stupid as it sounds) so first time I did a test exam I could only partially view the kubernetes.io/docs page. Subsequently I found ALT + F10 was the solution (maximize window) (or F11 for full-screen).

It's the same mock exam set with 22 questions you get access to everytime you do a killer.sh session. 

The killer.sh questions are harder then the real exam and there are 22 questions. The real exam has between 15-20 questions.  

### Practice using your planned exam hardware setup

You are only allowed to use one monitor at the exam. If you are used to using more monitors consider practicing working with only the one you plan to use at the exam. A large screen is better than a small one. An external web cam is required unless using a laptop with built-in camera.

### Have an overall plan in place

Regardless of your level of relevant knowledge when taking on the CKAD It's a good idea to have at least a brief overall plan.

1/ Do some initial assesment of your skills. For instance a mock exam, some kodekloud labs or some killercoda.com exercises. 

2/ Study and practice everything that is not easy and all topics that you cannot quickly solve

3/ When you start to master all relevant topics do kodekloud mock exams

4/ If you can do kodekloud mock exams decently, start thinking about the exam phase. Specifically which exam date to choose and when to do your two killer.sh exam simulator mock exam sessions. I recommend killer.sh session 1 about 2 weeks before the exam date. The second killer.sh session I'd do 2-3 days before the exam date. Practice everything that is still challenging in between the two killer.sh sessions.

5/ On exam day. Allow plenty of time to setup, login, get your ID approved and get your exam room approved.


