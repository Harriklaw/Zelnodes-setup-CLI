# Zelnodes-setup-CLI
## How to setup zelnodes on linux using cli
For clear ubuntu 16 (both Zelnode and Control)

We highly recommend to follow these instructions how to make ssh key pairs and create new sudo user.
Use the new sudo user for installation, managment and running the zelnodes.

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04

and how to make a firewall setup:

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-16-04

First build and run on Control (after the intallation follow the exact same instructions for your Zelnode steps 1-9):

1. *sudo apt-get update && apt-get upgrade -y*

2. *sudo apt-get install* \

*build-essential pkg-config libc6-dev m4 g++-multilib* \

*autoconf libtool ncurses-dev unzip git python python-zmq* \

*zlib1g-dev wget curl bsdmainutils automake*
 
3. *git clone https://github.com/zelcash/zelcash.git*

4. *cd zelcash*

5. *./zcutil/build.sh -j$(nproc)*

6. *mkdir ~/.zelcash*

*echo "rpcuser=username" >> ~/.zelcash/zelcash.conf*

*echo "rpcpassword=`head -c 32 /dev/urandom | base64`" >> ~/.zelcash/zelcash.conf*

*echo "rpcallowip=127.0.0.1" >> ~/.zelcash/zelcash.conf*

*echo "addnode=explorer.zel.cash" >> ~/.zelcash/zelcash.conf*

*echo "addnode=explorer.zel.zelcore.io" >> ~/.zelcash/zelcash.conf*

*echo "addnode=node.zel.cash" >> ~/.zelcash/zelcash.conf*

*echo "addnode=explorer.zel.cash" >> ~/.zelcash/zelcash.conf*

*echo "addnode=explorer2.zel.cash" >> ~/.zelcash/zelcash.conf*

*echo "addnode=explorer.zelcash.online" >> ~/.zelcash/zelcash.conf*

*echo "addnode=node-eu.zelcash.com" >> ~/.zelcash/zelcash.conf*

*echo "addnode=node-uk.zelcash.com" >> ~/.zelcash/zelcash.conf*

*echo "addnode=node-asia.zelcash.com" >> ~/.zelcash/zelcash.conf*

*echo "listen=1" >> ~/.zelcash/zelcash.conf*

*echo "server=1" >> ~/.zelcash/zelcash.conf*

*echo "daemon=1" >> ~/.zelcash/zelcash.conf*

*echo "logtimestamps=1" >> ~/.zelcash/zelcash.conf*

*echo "txindex=1" >> ~/.zelcash/zelcash.conf*

7. *cd zelcash*
*./zcutil/fetch-params.sh*

8. *./src/zelcashd*  Allow the daemon time to sync.
9. *./src/zelcash-cli stop*


On your control wallet run on a new terminal:

10. *cd zelcash*
11. *./src/zelcash-cli createzelnodekey*

make sure you store this key
12. *./src/zelcash-cli getnewaddress*

13. Transfer your collateral for your desired tier of ZelNode to the address generated in Step 2.Send the exact ammount of zel(eg 10k,25k or100k). Triple check the receiving address. We cannot help you if you transfer funds to the wrong address.
in that phase you should be able to use the swing wallet gui for making txs.
Once your transfer is confirmed (check the address at ZelCash Testnet Explorer, needs 2 confirmations minimum), use your control wallet to run the command -new terminal:


  *sudo nano ~/.zelcash/zelnode.conf*
 
14.using the arrow move below the last line and Now copy/paste this command to your last open terminal(using ctrl+shft+v to paste to terminal):

ZelNode1 168.104.100.190:16125 1234567890H9sA5ArE5Y9rrrrgAfRtKLYUp 13c385119f135c215a2bef7de37b534f1ac27f4d0f23c105d8ee431f9b797105 0

adding ZelNode details from Steps 1 and 4.
[ZelnodeName] [ZelNode IP address:port] [priv key from Step 1] [ZelNode output from Step 4] [Tx output digit from Step4]
There are spaces between the brackets. Call your [ZelnodeName] anything you want.

15. press [ctrl+x, y, enter ]to save and exit

16.(control wallet) 
sudo nano ~/.zelcash/zelcash.conf

17. same as 14 and 15 use the arrow to go down and copy/paste:
rpcuser=type an random long username
rpcpassword=type a long pass
rpcallowip=127.0.0.1
server=1
daemon=1
txindex=1
logtimestamps=1
maxconnections=256

18.press ctrl+x, y, enter to save and exit

19. on the vps server assuning that we built and run the zelcashd use the command
(if we are already in zelcash folder- starts with ~/zelcash#)
 cd
(Now starts with ~#)
(if we run the daemon)
./src/zelcash-cli stop 

20. sudo apt-get install nano
21. sudo nano ~/.zelcash/zelcash.conf
22. using the arrow move below the last line and copy/paste this:
rpcuser=type a random long username
rpcpassword=type a random long password
rpcallowip=127.0.0.1
zelnode=1
zelnodeprivkey=your key from step 1
listen=1
server=1
daemon=1
externalip=your server/vps ip
bind=your server/vps ip


Save and close the file, .
23. cd zelcash
24. ./src/zelcashd
25. On the control wallet, run the command 
zelcash-cli startzelnode alias false [ZelnodeName].

26.    I f everything was successful, you should see:

"overall": "Successfully started 1 zelnodes, failed to start 0, total 1",

"detail":[{

  "alias": [ZelNode Name],

  "result": "success",

  "error": ""

}]

27. On the ZelNode daemon, run the command ./src/zelcash-cli startzelnode local false local false. You should see a successful response.






