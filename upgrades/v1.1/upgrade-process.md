## ChronicNetwork v1.1 network upgrade:

Below is a overview to manually upgrade Chronic Network Binary v1.0.0 to v1.1.0. We will test this 

 

## 1. Backup all crucial validator files & state  
ex: `$HOME/.cht , previous binary version ]`
linux command example:` cp --backup $HOME/.cht $HOME/backups/ `
 

## 2. Once conensus has halted, fetch new upgrade files, we will be using make commands:

a- Install make: `apt install make`
b- Remove old source repo: commonly `$HOME/chtd`
c- Download new source repo: `cd $HOME && git clone https://github.com/ChronicNetwork/cht`
d- Build new binary: 
`cd cht `
`make build`
e- Install new binary: `make install`
f- Check binary version: `chtd version --long`

## 5. Upload new genesis file:
 A link will be available in the network governance discord channel.





