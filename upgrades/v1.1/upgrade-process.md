## Manual update guide for ChronicNetwork v1.1 network upgrade:

This guide shows how to perform a manual update of the binaries after a governance proposal has been approved for a chain update.
Below is a overview to manually upgrade Chronic Network Binary v1.0.0 to v1.1.0.

## About the upgrade

Chronic Chain update for the following:
- CosmosSDK v0.45.4
- IBC v3.0
- Cosmwasm v1.0.0

These upgrades expands Chronic Networks primary features, including:
- Stable Cosmwam Integrations
- ICA [InterChain Accounts]
- IBC [InterBlockchain Communication]
functionnality.

This is required for all your node (validators, sentries and any other you may have)

## Prerequisites

- Install make: ```sudo apt install make```

## 1. Stop your validator
First, make sure your node have reached at least the `754525` block height we will use to export the network state and restart from. You can configure your node in advance to stop at this height by setting the `halt-height` parameter in the `app.toml` file and restarting your node.
In the logs, you will see : `ERR UPGRADE "intent-1" NEEDED at height: 754525`
Also ensure that **no process managers (such as `systemd`) will attempt to restart it.**

The exact procedure to stop your node depends on how you configured it so we can't really give a generic way here.

Also double check it's properly stopped to avoid file corruption in the next steps.

```
sudo service chtd stop
```

## 1. Backup all crucial validator files & state  

Before making any changes, it's prefered to create a backup copy of your current `CHT_HOME` directory.

The following command can be used, assuming your `CHT_HOME` is `~/.cht/`:

```bash
cp -R ~/.cht/ ~/.cht_backup/
```

This would allow to revert back to your starting state in case something goes wrong on the way.
 

## 2. Install new chtd version:

You may already have the cht repository on your machine from the previous installation. If not, you can:

```bash
git clone https://github.com/ChronicNetwork/cht
cd cht
```

If you already have an existing clone, place yourself in and:

```bash
git fetch
git checkout
```

Now you can install the new chtd version:

```bash
make build
make install

# and verify you now have the correct version:
chtd -h
# must print chtd help message

chtd version
# must print v1.1.0-1-g396f602
```

Make sure the version is correct before proceeding further!

You're now ready to restart your node


## Verify upgrade completed

Start the chtd service

```
chtd start --unsafe-skip-upgrades 754525
```

Ensure that everything is OK by checking the logs 

```
sudo journalctl -u chtd -f
```
