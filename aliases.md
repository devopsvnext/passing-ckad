# Aliases

I found the below aliases to be easy to remember and save quite a lot of time.<br> 

```alias ka="k apply"```<br>
```alias kc="k create"```<br>
```alias kd="k describe"```<br>
```alias ke="k edit"```<br>
```alias kg="k get"```<br>
```alias kn="k config set-context --current --namespace"```<br>
```alias kr="k run"```<br>
```alias kt=kr tmp --image=nginx --rm -it --restart=Never -- curl```<br>


Remember you have to memorize and define the aliases you want to use at the exam, so it has to be balanced. <br>Most probably you don't want too many and too advanced aliases since that will take time to type in during the exam. <br>Only the ones that are used a lot and will save time are good candidates.<br>

Strictly speaking not an alias. I also exported an environment variable 'do' so I could type $do instead of '--dry-run=client -o yaml':<br><br>
```export do="--dry-run=client -oyaml"```<br>

So for instance to create yaml for an nginx deployment called webapp with 2 replicas using the above aliases would be

```kc deploy webapp --image=nginx --replicas=2 $do>d.yml```

which would create this d.yml:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: webapp
  name: webapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: webapp
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: webapp
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

You can see defined aliases using the 'alias' command.

Whenever you do labs setup the aliases you want to use so you get used to setting them up quickly.



