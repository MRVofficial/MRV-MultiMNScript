# Multiple MasterNode

A script which is easily create Multiple Masternodes of the same coin in the same VPS.

First of all you have to start one masternode using <a href="https://github.com/MRVofficial/MRV-MNScript/blob/master/mrv_16.04.sh">mrv_16.04.sh</a> script that is your MainNode.

# Guide for Install MultiMN:

Install the multimn script 

`curl -sL https://raw.githubusercontent.com/MRVofficial/MRV-MultiMNScript/master/multimn_install.sh | sudo -E bash -`

Add the coin profile.
```
wget -q https://raw.githubusercontent.com/MRVofficial/MRV-MultiMNScript/master/profiles/mrvcoin.mn
multimn profadd mrvcoin.mn mrvcoin
```
Now the MRVCoin profile is saved and the downloaded file can be removed if you want: `rm -rf mrvcoin.dmn`

Stop the mrvcoin Service:

`systemctl stop mrvcoin`

Now create 3 extra instances (Ex. You want to make 3 Masternode):
```
multimn install mrvcoin
multimn install mrvcoin
multimn install mrvcoin
```
You can check every MN like this:
```
mrv_coin-cli-1 getinfo
mrv_coin-cli-2 getinfo
mrv_coin-cli-3 getinfo
mrv_coin-cli-all getinfo
```
There's also a `mrv_coin-cli-0`, that is a reference to the 'main node', not a created one with multimn.

Now, if you want to uninstall any instances,then just uninstall it with:

`multimn uninstall mrvcoin 2` (Uninstall instance 2)

You can uninstall all of them with:

`multimn uninstall mrvcoin all`


You can get priv key of all MN with:

`multimn list mrvcoin --privkey`


Note this all priv key and make `masternode.conf` in your Coldwallet where you done MasternodeTx.
so `masternode.conf` look like this:
```
MN01 IP:9555 MN_PrivKey Tx_Hash Output_Index
MN02 IP:9555 MN_PrivKey Tx_Hash Output_Index
MN03 IP:9555 MN_PrivKey Tx_Hash Output_Index
MN04 IP:9555 MN_PrivKey Tx_Hash Output_Index
```

Here IP and port Same for all MN.

MN01 is your main_node MN which you create with <a href="https://github.com/MRVofficial/MRV-MNScript/blob/master/mrv_16.04.sh">mrv_16.04.sh</a> script.

MN02, MN03, MN04 is your masternode which you create with multimn.


Now StartMasternode from Coldwallet with:
```
startmasternode alias false MN01
startmasternode alias false MN02
startmasternode alias false MN03
startmasternode alias false MN04
```

Now StartMasternode in VPS with Service:

`systemctl start mrvcoin` (Start your MN which is create with main_node <a href="https://github.com/MRVofficial/MRV-MNScript/blob/master/mrv_16.04.sh">mrv_16.04.sh</a> script)

Below 3 MN which is create with `multimn` script.
```
systemctl start   mrvcoin-1.service
systemctl start   mrvcoin-2.service
systemctl start   mrvcoin-3.service
```

That's all now your MN start.





