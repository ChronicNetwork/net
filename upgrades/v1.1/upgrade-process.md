## chtd v1.1 network upgrade:

Below is a overview to manually upgrade Chronic Network Binary v1.0.0 to v1.1.0. We will test this 

 

## 1. Backup all crucial validator files & state  [$HOME/.cht , previous binary version ]:
### linux command example:     ` cp --backup $HOME/.cht $HOME/backups/ `
 

## 2. Once conensus has halted, fetch new upgrade files, we will be using make commands:

a- install make: `apt install make`
b- remove old source repo: commonly $HOME/chtd
c- download new source repo: `cd $HOME && git clone https://github.com/ChronicNetwork/cht`
d- build new binary: 
`cd cht `
`make build`
e- install new binary: `make install`
f- check binary version: `chtd version --long`

## 5. upload new genesis file:
 a link will be available in the network governance discord channel.





