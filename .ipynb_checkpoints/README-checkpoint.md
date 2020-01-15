2
# Proof of Authority Development Chain

For this assignment, you will take on the role of a new developer at a small bank.

Your mission, should you choose to accept it, will be to set up a testnet blockchain for your organization.

To do this, you will create and submit four deliverables:

* Set up your custom testnet blockchain.

* Send a test transaction.

* Create a repository.

* Write instructions on how to use the chain for the rest of your team.

## Background

You have just landed a new job at ZBank, a small, innovative bank that is interested in exploring what
blockchain technology can do for them and their customers.

Your first project at the company is to set up a private testnet that you and your team of developers
can use to explore potentials for blockchain at ZBank.

You have decided on setting up a testnet because:

There is no real money involved, which will give your team of developers the freedom to experiment.

Testnets allows for offline development.

In order to set up a testnet, you will need to use the following skills/tools we learned in class:

* Puppeth, to generate your genesis block.

* Geth, a command-line tool, to create keys, initialize nodes, and connect the nodes together.

* The Clique Proof of Authority algorithm.

Tokens inherently have no value here, so we will provide pre-configured accounts and nodes for easy setup.

After creating the custom development chain, create documentation for others on how to start it using the pre-configured
nodes and accounts. You can name the network anything you want, have fun with it!

Be sure to include any preliminary setup information, such as installing dependencies and environment configuration.

## Instructions

1. Open a terminal window (GitBash in Windows) navigate to your `Blockchain-Tools` folder and type the following command:
​
  ```bash
  ./puppeth
  ```
​
2. `>finblock` <- name of network
​
3. Type `2` to pick the `Configure new genesis` option, then `1` to `Create new genesis from scratch`:
​
4. Type `1` to choose `Proof of Work` and continue.
​
5. Addresses: Uses those assocated with cloud mneumonic
Use MyCrypto like from the previous class, and explain to the students that in this step is where we are going to pre-fund any accounts.
​
6. Once you paste an address and hit enter, hit enter again on the blank 0x address to continue the prompt.
​
7. Continue with the default option for the prompt that asks, Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? by hitting enter again until you reach the Chain ID prompt.
​
8. come up with a number to use as a "chain ID" or make one up yourself, like 333, for example.
​
9. In the `puppeth` prompt, navigate to the `Manage existing genesis` by typing `2` and hit enter.
​
10. Next, type `2` again to choose the `Export genesis configurations` option, then continue with the default (current) directory:
​
11. Show files in Blockchain-Tools folder. Show json file.
​
12. Exit the puppeth prompt by using the Ctrl+C keys combination.
​
​
### 8. Create Nodes
13.
```bash
./geth account new --datadir node1
```
​
14. password "node1" (repeat)
​
15. repeat above for node2
​
16. Initialize nodes
```bash
./geth init puppernet.json --datadir node1
./geth init puppernet.json --datadir node2
```
17. Explain to students that the chain is ready to be started. Now it's time to have the students initialize their nodes.
​
​
### 12. Starting the Blockchain (10 min)
​
18. launch the first node into mining mode with the following command:
```bash
./geth --datadir node1 --mine --minerthreads 1
```
​
19. copy the entire `enode://` address (including the last `@address:port` segment) of the first node located in the `Started P2P Networking` line:
​
20.
  * Running in OS X:
​
  ```bash
  ./geth --datadir node2 --port 30304 --rpc --bootnodes "enode://69994ca26f775569b5cdb4970299c2265f7dcb7714a4ffaf66400f50e5128e79e2ff465731ddf597030f931375aa90f40d6cff7ace0f4afb84ae8de19da047bf@127.0.0.1:30303"
  ```
​
  * Running in Windows:
​
  ```bash
  ./geth --datadir node2 --port 30304 --rpc --bootnodes "enode://69994ca26f775569b5cdb4970299c2265f7dcb7714a4ffaf66400f50e5128e79e2ff465731ddf597030f931375aa90f40d6cff7ace0f4afb84ae8de19da047bf@127.0.0.1:30303" --ipcdisable
  ```
​
  **Note**: If you ever encounter strange errors, or need to start over without destroying the accounts, run the following command to clear the chain data (this will reset the `enode` addresses as well):
​
  ```bash
  rm -Rf node1/geth node2/geth
  ```
​
​
​
### Transacting on the chain (10 min)
​
### Getting address key
21. Open up MyCrypto and be sure the `Kovan` network is selected.
​
22. Unlock your wallet using your mnemonic phrase and choose the address you want to inspect.
​
23. Select the ETH address you use to pre-fund your chain, and in the "Select" dropdown list, choose "Wallet Info.
​
​
24. Click on the eye icon next to the "Private Key" field, and copy and paste the private key of the wallet.
​
Explain to students that now you are going to connect MyCrypto with the blockchain you created. Follow the next steps.
​
25. In the left pane on MyCrypto, click "Change Network" at the bottom left:
​
### seting network info
26. Click on "Add Custom Node", then add the custom network information that was set in the genesis.
​
27. Ensure that you scroll down to choose `Custom` in the "Network" setting to reveal more options like `Chain ID`:
​
28. The chain ID must match what you came up with earlier.
​
29. The URL is pointing to the default RPC port on your local machine. Everyone should use this same URL: `http://127.0.0.1:8545`.
​
Click on the "Save & Use Custom Node" button, to use the network; double-check that it is selected and is connected.
​
#### Sending money
​
30. On the left pane menu, click on "View & Send".
​
31. Next, click on the "Private Key" option to continue.
​
* A new window will pop-up, paste the private key of the pre-fund wallet and click on the "Unlock" button to continue.
​
* Looks like we're filthy rich! This is the balance that was pre-funded for this account in the genesis configuration; however, these millions of ETH tokens are just for testing purposes.
​
We're going to send a transaction to ourselves to test it out. Follow the next steps.
​
* Copy the pre-fund address into the "To Address" field, then fill in an arbitrary amount of ETH:
​
* Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.
​
* Click the `Check TX Status` when the green message pops up, confirm the logout:
​
* You should see the transaction go from `Pending` to `Successful` in around the same blocktime you set in the genesis.
​
* You can click the `Check TX Status` button to update the status.
​
Congratulations, that was the first transaction send on this blockchain network! Now it's time for the students to do the same

### Setup the custom out-of-the-box blockchain

* Create a new project directory for your new network. Call it whatever you want!

* Create a "Screenshots" folder inside of the project directory.

* Create accounts for two (or more) nodes for the network with a separate `datadir` for each using `geth`.

* Run `puppeth`, name your network, and select the option to configure a new genesis block.

* Choose the `Clique (Proof of Authority)` consensus algorithm.

* Paste both account addresses from the first step one at a time into the list of accounts to seal.

* Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

* You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

* Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

* Export genesis configurations. This will fail to create two of the files, but you only need `networkname.json`.

* You can delete the `networkname-harmony.json` file.

* Screenshot the `puppeth` configuration once complete and save it to the Screenshots folder.

* Initialize each node with the new `networkname.json` with `geth`.

* Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.

* Set a different peer port for the second node and use the first node's `enode` address as the `bootnode` flag.

* Be sure to unlock the account and enable mining on the second node!

* You should now see both nodes producing new blocks, congratulations!

### Send a test transaction

* Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port.

* You will need to use a custom network, and include the chain ID, and use ETH as the currency.

![custom-node](Images/custom-node.png)

* Import the keystore file from the `node1/keystore` directory into MyCrypto. This will import the private key.

* Send a transaction from the `node1` account to the `node2` account.

* Copy the transaction hash and paste it into the "TX Status" section of the app, or click "TX Status" in the popup.

* Screenshot the transaction metadata (status, tx hash, block number, etc) and save it to your Screenshots folder.

* Celebrate, you just created a blockchain and sent a transaction!

![transaction-success](Images/transaction-success.png)

### Create a repository, and instructions for launching the chain

* Create a `README.md` in your project directory and create documentation that explains how to start the network.

* Remember to include any environment setup instructions and dependencies.

* Be sure to include all of the `geth` flags required to get both nodes to mine and explain what they mean.

* Explain the configuration of the network, such as it's blocktime, chain ID, account passwords, ports, etc.

* Explain how to connect MyCrypto to your network and demonstrate (via screenshots and steps) and send a transaction.

* Upload the code, including the `networkname.json` and node folders.

### Remember, *never* share your mainnet private keys! This is a testnet, so coins have no value here!

### Challenge mode

* Create a separate `bootnode` dedicated to connecting peers together

* There will be a new DevOps engineer joining the team, add an additional sealer address to the network on the fly!
