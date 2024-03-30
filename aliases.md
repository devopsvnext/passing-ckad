alias ka="k apply"
alias kc="k create"
alias kd="k describe"
alias ke="k edit"
alias kg="k get"
alias kn="k config set-context --current --namespace"
alias kr="k run"
alias kt=kr tmp --image=nginx --rm -it --restart=Never -- curl

export do="--dry-run=client -oyaml"

Remember you have to memorize and define the aliases you want to use at the exam, so it has to be balanced. Most probably don't want too many and too advanced aliases since that will take time to type in during the exam. Only the ones that are used a lot and will save time are good candidates.

Strictly speaking not an alias. I also exported an environment variable 'do' so I could type $do instead of '--dry-run=client -o yaml':
export do="--dry-run=client -oyaml"

You can see defined aliases using the 'alias' command.



