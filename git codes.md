## ssh into github

### creating ssh private-public key pair in a machine
1. open terminal
2. search for ```.ssh``` in home. If not found create the folder and cd into it
3. to generate key: ```ssh-keygen``` and click enter for all confirmations until key is generated.

## view the generated key
1. open terminal
2. go to home: ```cd ~``` -> ```cd .ssh``` -> ```ls```
3. 2 keys can be seen
 - private key : id_rsa
 - public key: id_rsa.pub
  1. will be shared to github
4. print public key: %cat id_rsa.pub%

## setting ssh to github\
1. open browser -> github -> login
2. settings -> ssh and gpg keys -> new ssh key
3. setting it up: 
 - key type: authentication key
 - key: copied public ssh key

## setting other team members
1. adithya must give access of the private project to other team members
2. go to project in github
3. settings -> access -> add people


## pushing the code

### commit
1. to add untracked files to the commit:  % git add . %
2. to see the changes to be committed: % git status %
3. % git commit -m “commit message” %

### initial push
>initial push will be a force push
1. % git push -u -f origin main % . enter yes if prompted to create trust.
>everything in the github repo will be overwritten when force pushed.

### push
1. % git push origin main %