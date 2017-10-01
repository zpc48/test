# Overview of Hybrid Consensus Scheme in Hcash

[![ISC License](http://img.shields.io/badge/license-ISC-blue.svg)](http://copyfree.org)
[![GoDoc](https://img.shields.io/badge/godoc-reference-blue.svg)](http://godoc.org/github.com/HcashOrg/hcashd)


When designing the consensus scheme for Hcash, we need to determine which technology for permissionless distributed ledger should be adopted, blockchain-based or DAG(Directed Acyclic Graph)-based? On the one hand, blockchain technique has been well studied in the aspects of consensus model, scalability, efficiency, security, robustness, privacy preserving, etc. Also, it has been widely applied and thoroughly testified in various decentralized cryptocurrencies or systems such as Bitcoin, Ethereum, and so on. Hence, blockchain is considered as a reliable technique for permissionless distributed ledger though there is still lots of room for the improvement of this promising technology. On the other hand, DAG technique has been leveraged recently in a few cryptocurrencies. These DAG-based cryptocurrencies are merited for their potential high throughput, especially in the case of massive transactions. However, DAG-based distributed systems lack sufficiently rigid and convincing investigation and evaluation, as well as sophisticated trial in practice. Furthermore, we find that there are some security issues in the existing DAG-based cryptocurrencies, for instance, IOTA's security heavily relies on the transaction frequency; Security flaw exists in the consensus model of Byteball (specifically, in the strategy algorithm for moving forward stable point of the distributed system); Byteball's security depends on a few “witness” nodes, which leads to potential centralization. Consequently, we adopt blockchain-based instead of DAG-based technology in Hcash.

After bitcoin was presented in 2008, various cryptocurrencies have been proposed and developed. Also, enhancements to the existing decentralized systems have been devised and put into practice. Among all, the most attractive innovations include Ethereum (supporting smart contracts), CryptoNotes, ZeroCash (enhancing privacy via ring signatures or non-interactive zero-knowledge proofs), DASH, Decred (implementing hybrid consensus and basic DAO), IOTA, Byteball (improving the throughput with DAG-based structure), Bitcoin-NG (introducing keyblock and microblock to enhance throughput), and sidechain techniques (supporting interchangeability between some given cryptocurrencies).


Proof-of-work (PoW), the consensus scheme implemented in bitcoin and many other well-known decentralized cryptocurrencies, has lots of merits including trustworthy sustainability, strong robustness against malicious participants, delicate incentive-compatibility, and openness to any participant (i.e., participants could join and leave  dynamically). 


Meanwhile, PoW has been criticized due to its waste of resources and a potential centralization of hash power. Thus alternative consensus models have been introduced to replace (fully or partially) PoW, like proof-of-stake (PoS). However, PoS is controversial for its sustainability and security, due to lack of practical trials and the risk of data forgery.


Another drawback of PoW is its relatively poor efficiency. Bitcoin, equipped with PoW, can only support very limited transaction throughput (say, at most 7 transactions per second (TPS)), which greatly constrains the scalability of Bitcoin system. So far five approaches have been proposed to solve or relieve this issue as shown below:

1. Shorten the block interval;
2. Extend the block size;
3. Adopt two-layer chain structure (i.e., keyblock/microblock);
4. Introduce the lightning network;
5. Apply DAG-based framework/structure.

Among them, 1) compromises certain stability/security of decentralized system, which has been shown by the practice of ETH. More specifically, the short block interval (20-30s) adopted in ETH did cause instability of the system, and to face this issue, the “GHOST” protocol (somewhat controversial) was implemented in ETH. For 2), it seems simple but causes communication burden to the network. While for 3), it was presented in Bitcoin-NG and its main idea is as follows: the block created by a miner after solving hash puzzle is called a keyblock. After the creation of a keyblock (say, block A), the corresponding miner can release several microblocks before a keyblock succeeding block A is generated. The security and robustness of the decentralized system rely on the PoW mechanism for keyblock, and the system throughput can be improved greatly due to frequent release of microblocks. However, Bitcoin-NG is problematic for its vulnerability to selfish mining and a potential attack by keyblock proposer's spawning massive microblocks which undermines the convergence property of the system and causes network overburdening because of massive forks. Regarding 4), it provides an efficient off-chain transaction mechanism, targeting on transactions with small value and high frequency. As for 5), it draws much interest for its potential high throughput, however, this novel technique still needs to be sufficiently investigated and evaluated theoretically and practically.


To date, existing decentralized cryptocurrencies adopt either PoW consensus scheme or hybrid consensus model of PoW and PoS. However, these systems still encounter the issue of very limited efficiency/throughput. 

Hcash project aims to build secure, efficient, robust and reliable decentralized system. Highlighted features such as newly-proposed hybrid consensus scheme, post-quantum digital signature, linkability among various blockchain-based and DAG-based decentralized cryptocurrencies, smart contract mechanism and post-quantum privacy-preserving scheme will be proposed and implemented in Hcash eventually. First of all, we present a novel hybrid consensus scheme with strong robustness, high throughput as well as sufficient flexibility in Hcash. On the one hand, with a newly-proposed two-layer framework of block chain, significant improvement of the efficiency is offered without compromising the security. On the other hand, with a hybrid consensus model, both PoW and PoS miners are incentivized to take part in the consensus process, thereby enhancing the security and flexibility of the consensus scheme, and providing a mechanism that supports basic DAO for future protocol updating and project investments.

Our brand-new consensus mechanism inherits the merits of Decred and Bitcoin-NG, based on which we propose key innovations to make our scheme more secure, efficient and flexible. Firstly, with the methodology from Bitcoin-NG's keyblock/microblock structure, we offer a two-layer chain structure. To tackle the aforementioned security issue existed in Bitcoin-NG, we present two-level mining mechanism and incorporate this mechanism into the two-layer chain structure. More specifically, two level of difficulties of PoW hash puzzle are set and these difficulties can be adjusted dynamically. When solving a hash puzzle, PoW miner can create a keyblock once the hard-level difficulty is met, and publish a microblock in the case that the low-level difficulty is satisfied. In this way, the system throughput could be enhanced significantly, and the security of the system is not compromised since malicious miners can not spawn massive microblocks freely. Furthermore, to tackle the selfish mining issue, strengthen the robustness against “the 51% attack” of PoW miners, and offer the sufficient flexibility (supporting both PoW and PoS mining), we borrow the idea of Decred's ticket-voting mechanism (a practical and flexible PoS scheme) and combine it with our newly-proposed two-layer chain structure delicately to devise a secure, efficient and flexible hybrid consensus scheme. In Hcash, keyblocks should be confirmed by certain voting tickets, and both PoW and PoS miners play important roles on the consensus of the system. With this novel hybrid scheme, we further implement basic DAO to provide PoW and PoS miners an effective mechanism for future protocol updating and project investments. Meanwhile, our scheme supports the segregated witness scheme, which facilitates the implementation of the lightning network and post-quantum signature schemes in the future. The schematic framework of our consensus scheme is shown in Figure I.

<p align="center">
	<img src ="pic/Figure1.png" />
	<br/>
	Figure I: The schematic framework of our consensus scheme
	<br/>
	<br/>
</p>
     


In Table I, comparisons are made between Hcash and a few well-known decentralized cryptocurrencies. Table I also includes throughputs of Hcash with different parameters for keyblock/microblock generations. The current release of Hcash corresponds to the row marked with bold font.

|             |Keyblock Average Interval|Block Size|Microblock Average Interval|Transaction Size|Throughput      |
|:----------- |:-----------------------:|:--------:|:-------------------------:|:--------------:|:--------------:|
|BTC          | 10min                   | 1MB      |                           | 250B           | 6.99TPS        |
|BTC(extended)| 10min                   | 2MB      |                           | 250B           | 13.98TPS       |
|BCC          | 10min                   | 8MB      |                           | 250B           | 55.92TPS       |
|Decred       | 5min                    |1.25MB    |                           | 250B           | 17.48TPS       |
|<span style="color:rgb(192, 0, 0)">__Hcash__</span>   | __5min__                | __2MB__  |    __18.75 sec__          | __250B__       | __447.39TPS__  |
|Hcash        | 5min                    | 8MB      |      18.75 sec            | 250B           | 1789.57TPS     |
<p align="center">
	Table I: Comparisons between Hcash and a few well-known decentralized cryptocurrencies 
	<br/>
	<br/>
</p>



Table II offers the relation between adversary’s PoW power and PoS capabilities (measured in proportion over all PoW power or PoS capabilities) and the success possibility of adversary undermining the system (α denotes the proportion of adversary's PoW power, β denotes the proportion of adversary's PoS capabilities).

<p align="center">
	<img src ="pic/Table2.png" />
	<br/>
	Table 2:  Probability of adversary's succeeding in an attack with α fraction of total hash power and β fraction of total stake
	<br/>
	<br/>
</p>



The detailed description and analysis (including security and efficiency analysis) of the novel hybrid consensus scheme implemented in Hcash will be given in our research paper which will appear in the near future.

## Starting Hcashd
Hcashd is a Hypercash full node implementation written in Go (golang).

This acts as a chain daemon for the [Hypercash](https://h.cash) cryptocurrency. Hcashd maintains the entire past transactional ledger of Hypercash and allows relaying of transactions to other Hypercash nodes across the world.
The installation of hcashd requires Go 1.7 or newer.
* Glide 

	Glide is used to manage project dependencies and provide reproducible builds. To install:
	```
	go get -u github.com/Masterminds/glide
	```
* Build and Installation
	
	For a first time installation, the project and dependency sources can be obtained manually with git and glide (create directories as needed):
	```
	git clone https://github.com/HcashOrg/hcashd $GOPATH/src/github.com/HcashOrg/hcashd
	cd $GOPATH/src/github.com/HcashOrg/hcashd
	glide install
	go install $(glide nv)
	```
    To update an existing source tree, pull the latest changes and install the matching dependencies:
    ```
	cd $GOPATH/src/github.com/HcashOrg/hcashd
	git pull
	glide update
	glide install
	go install $(glide nv)
    ```


## License

hcashd is licensed under the [copyfree](http://copyfree.org) ISC License.







# hcashwallet

## Overview

Hcashwallet is a daemon handling hcash wallet functionality for a single user.  

It acts as both an RPC client to hcashd and an RPC server for wallet clients and legacy RPC applications. It manages all of your accounts, addresses, and transactions and allows users to participate in Proof-of-Stake voting.

Hcashwallet is not an SPV client and requires connecting to a local or remote hcashd instance for asynchronous blockchain queries and notifications over websockets. Full hcashd installation instructions can be found [here](https://github.com/HcashOrg/hcashd).

## Build and Installation

The installation of hcashwallet requires Go 1.7 or newer.
* Glide
	
	Glide is used to manage project dependencies and provide reproducible builds. To install:
	```
	go get -u github.com/Masterminds/glide
	```
* Build and Installation
	
	For a first time installation, the project and dependency sources can be obtained manually with git and glide (create directories as needed):
	```
	git clone https://github.com/HcashOrg/hcashwallet $GOPATH/src/github.com/HcashOrg/hcashwallet
	cd $GOPATH/src/github.com/HcashOrg/hcashwallet
	glide install
	go install $(glide nv)
	```
    To update an existing source tree, pull the latest changes and install the matching dependencies:
    ```
	cd $GOPATH/src/github.com/HcashOrg/hcashwallet
	git pull
	glide install
	go install $(glide nv)
    ```

## Getting started

The following instructions detail how to get started with hcashwallet connecting to a localhost hcashd. The command should be run in the console.

* Creating

The folloing instruction detail how to create a new wallet when first starting the wallet. (PS: This instruction is only for initailize your new wallet, thus it's not recommanded when you already had wallet)

```
hcashwallet --create
```

During this process, you’ll set a private passphrase, optionally set a public passphrase, and record your seed. 

* Configuring

After creating the wallet for the first time, it's necessary to configure your wallet before launching. It's recommanded to copy the sample hcashd and hcashwallet configurations and update with your RPC username and password.

```
$ cp $GOPATH/src/github.com/HcashOrg/hcashd/sample-hcashd.conf ~/.hcashd/hcashd.conf
$ cp $GOPATH/src/github.com/HcashOrg/hcashwallet/sample-hcashwallet.conf ~/.hcashwallet/hcashwallet.conf
```
After copy the sample configuration file to working directory, you need to update your RPC username and password. In addtion, if you want to participate the PoS consensus process, you need to purchase ticket and set the following parameter in your hcashwallet.conf.
```
enablevoting=1
```  
The detailed information of configuration will be released soon.

* Lauching

```
hcashwallet
```
If already set enable voting before , you need to type in your private phrase later.

You can run hcashctl.exe and type in the following common instructions to gain detailed inforamtion of your current state. 

PS: Hcashctl will be installed with the installation of hcashd.
```
hcashctl getinfo  		           //Displays the basic info about the network including current block number and network difficulty.
hcashctl --wallet getnewaddress   //Get a new address in the given account.
hcashctl --wallet getbalance      //Get the spendable balance in the given account. 
hcashctl --wallet getstakeinfo    //Get info about the current status of the PoS pool. 
hcashctl --wallet sendtoaddress "[address]" [amount]  //Send hcash from your account to the wanted address
hcashctl --wallet purchaseticket "[fromaccount]" spendlimit minconf "ticketaddress" "[numtickets]")   
//Purchase tickets to participate in PoS process. Spendlimit denotes the limit on the amount to spend on ticket, minconf denotes the minimal required confirmation of the transaction(e.g. 1)
```

## License

hcashwallet is licensed under the [copyfree](http://copyfree.org) ISC License.