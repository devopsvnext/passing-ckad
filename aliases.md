alias ka="k apply"<br>
alias kc="k create"<br>
alias kd="k describe"<br>
alias ke="k edit"<br>
alias kg="k get"<br>
alias kn="k config set-context --current --namespace"<br>
alias kr="k run"<br>
alias kt=kr tmp --image=nginx --rm -it --restart=Never -- curl<br>


Remember you have to memorize and define the aliases you want to use at the exam, so it has to be balanced. <br>Most probably you don't want too many and too advanced aliases since that will take time to type in during the exam. <br>Only the ones that are used a lot and will save time are good candidates.<br>

Strictly speaking not an alias. I also exported an environment variable 'do' so I could type $do instead of '--dry-run=client -o yaml':<br><br>
export do="--dry-run=client -oyaml"<br><br>

You can see defined aliases using the 'alias' command.



