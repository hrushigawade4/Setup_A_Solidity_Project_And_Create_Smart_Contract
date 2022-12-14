# Setup_A_Solidity_Project_And_Create_Smart_Contract
SImple solidity project setup and crate smart contract

# Set Up
Let's begin by setting you up to make you ready to begin creating your first project!


# Prerequisites

Visual Studio Code
NodeJS 14.x LTS

# Creating The Project

Now you are ready to initialize the project and install the necessary dependencies.

# Initializing An NPM Project

The most prominent Solidity tooling is based on JavaScript. It runs on Node and requires an npm project. It is basically like any other web development project you might have done in the past.

The first thing you thus have to do is to create a folder for your new project. So, go ahead and create a new folder. I will call mine solidity-project.

When you have that folder, jump into it and initialize a new npm project with:

```bash
npm init -y
```

This creates a basic package.json for you that should look like below.

```javascript
{
  "name": "solidity-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Oliver Jumpertz",
  "license": "ISC"
}
```

You can remove "main" if you want to, you won't need it.

# Installing Hardhat

Hardhat is a local Solidity development environment. It is available as an npm package and comes with a lot of tooling that enables you to develop with Solidity frictionlessly. It has a task runner, manages the Solidity compiler version for you, and comes with a test environment that allows you to test your contracts locally.

Hardhat has an initializer command you can execute with npx. So go ahead and execute the following command:


```bash
npx hardhat
```


You should be presented with a prompt like this (if npm asks you to install hardhat like shown below, confirm):

```javascript
Need to install the following packages:
  hardhat
Ok to proceed? (y) y
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

???? Welcome to Hardhat v2.4.0 ???????

? What do you want to do? ??? 
??? Create a sample project
  Create an empty hardhat.config.js
  Quit

```

You could now choose to create a sample project but go with the empty hardhat config for now because you will build your project from scratch.

When you executed the command, you should have a new file in your project called hardhat.config.js. You probably know such files already. Nearly all JavaScript tools have config files, and hardhat is no different.

It should look like this:


```javascript

/**
 * @type import('hardhat/config').HardhatUserConfig
 */
module.exports = {
  solidity: "0.7.3",
};


```

0.7.3 is sadly a little outdated, so update this to 0.8.5 (this is the latest version of Solidity at the time of writing this article).

# Installing Hardhat Locally

Hardhat's init command has only created a config file for you, but it has not altered your package.json. This is why you manually need to install hardhat as a development dependency now.

Execute the following command:


```bash
npm install --save-dev hardhat

```

Now you have hardhat installed in your project. You can execute Hardhat through npx anytime, but having a project-local version is usually a good idea. This prevents clashes through updates and unexpected changes in new versions.

# Creating The Folder Structure


Next, you need to create the three essential base folders of your Solidity project:

1.contracts is where your Solidity files go to.
2.scripts is where you store hardhat scripts (remember that I said it comes with a task runner? Scripts are basically hardhat tasks).
3.test is where your contract tests land.
When you created them, you are ready to install some more dependencies.

# Installing Hardhat Plugins


```bash
npm install --save-dev @nomiclabs/hardhat-waffle @nomiclabs/hardhat-ethers ethereum-waffle chai  ethers solidity-coverage


```

These are quite a few dependencies, so let's go over what each of them is or does right now:

@nomiclabs/hardhat-waffle: This is a Hardhat plugin that enables waffle support.
@nomiclabs/hardhat-ethers: This is a Hardhat plugin that enables ethers support.
ethereum-waffle: Waffle is a Solidity testing library. It allows you to write tests for your contracts with JavaScript.
chai: Chai is an assertion library and provides functions like expect.
ethers: This is a popular Ethereum client library. It allows you to interface with blockchains that implement the Ethereum API.
solidity-coverage: This library gives you coverage reports on unit tests with the help of Istanbul.

# Activating The Plugins

For plugins to become active, you need to tell Hardhat to use them actively. This task is relatively simple, though. You only need to require the plugins in your hardhat.config.js like this:

```javascript

require("@nomiclabs/hardhat-waffle");
require('solidity-coverage');

/**
 * @type import('hardhat/config').HardhatUserConfig
 */
module.exports = {
  solidity: "0.8.5",
};



```

Hardhat does now know which plugins are activated and can use them on demand. But to actually make use of them, you first need to create some commands.


# Adding Commands

Your project does currently only know one command: test, and this one isn't even really implemented. Time to change this. Let's add commands to build and test your smart contracts:

```javascript

"build": "hardhat compile",
"test:light": "hardhat test",
"test": "hardhat coverage",



```

These commands will do the following:

build: This command tells hardhat to take your Solidity files from the contracts folder and run them through the Solidity compiler.
test:light: This one invokes Waffle to test your contracts.
test: This one invokes Waffle and additionally generates a coverage report for you. The coverage command was added to Hardhat by the solidity-coverage plugin.
Your package.json should look something like this after your modifications:

```javascript

{
  "name": "solidity-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "hardhat compile",
    "test:light": "hardhat test",
    "test": "hardhat coverage"
  },
  "keywords": [],
  "author": "Oliver Jumpertz",
  "license": "ISC",
  "devDependencies": {
    "@nomiclabs/hardhat-ethers": "^2.0.2",
    "@nomiclabs/hardhat-waffle": "^2.0.1",
    "chai": "^4.3.4",
    "ethereum-waffle": "^3.4.0",
    "ethers": "^5.3.1",
    "hardhat": "^2.4.0",
    "solidity-coverage": "^0.7.16"
  }
}



```


Now you have a basic project that you could already work with. This means it is time to implement your first smart contract in Solidity, so you can make use of all the work you put into your project up until now.

# Implementing Your First Smart Contract

Time to write some Solidity! But please, don't expect too much. You will implement a very basic contract so you get a general idea of Solidity. Future articles will definitely cover more complex contracts.

# Time For Some Solidity Code

You can see the full code of the smart contract below. So go ahead, copy the code, and put it into contracts/MyContract.sol.

```solidity

// SPDX-License-Identifier: MIT

pragma solidity >=0.7.0 <0.9.0;

contract MyContract {
    string private name;

    constructor(string memory _name) {
        name = _name;
    }

    function changeName(string memory _name) public {
        name = _name;
    }

    function getName() public view returns (string memory) {
        return name;
    }
}


```


# Compiling Your Contract


```bash
npm run build



```

You should now see output that looks like the following:

```bash

> solidity-retry@1.0.0 build
> hardhat compile

Compiling 1 file with 0.8.5
Compilation finished successfully




```
If you watch your project closely, you will probably notice that a new folder, artifacts, has been created. This is the dist/out folder or whatever you call it in your usual projects. Within this folder, you find two more folders: contracts and MyContract.sol. Within the latter, you find two files, called MyContract.dbg.json and MyContract.json. Especially the last one is interesting because it contains the ABI and byte code of your smart contract. This is the output of the Solidity compiler.

You can take a further look if you are interested or follow along to learn how to test your contracts next.


# Testing Your Contract
Software without tests is always at risk of failing unexpectedly. Smart contracts are no different. But this is exactly what we included Waffle and chai for, to write tests that verify your contract works the way it should. And especially as it is not straightforward to write smart contracts that can actually be updated (everything on the blockchain is immutable, even your code), tests are even more important.

Waffle enables you to test your smart contracts not with Solidity itself but with JavaScript, all in an environment you are probably already comfortable with. Under the hood, Waffle uses mocha as a test runner and provides the well-known structure of describe and it for JavaScript tests.

Take a look at the following code and then copy it into a new file test/MyContract.test.js:


```javascript

const { expect } = require("chai");

describe("MyContract", () => {
  it("should return its name", async () => {
    const MyContract = await ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy("My Contract");

    await myContract.deployed();
    expect(await myContract.getName()).to.equal("My Contract");
  });
  it("should change its name when requested", async () => {
    const MyContract = await ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy("My Contract");

    await myContract.changeName("Another Contract");
    expect(await myContract.getName()).to.equal("Another Contract");
  });
});





```

# Executing Your Tests

```bash
npm run test


```

You should see output similar to this in your terminal:

```bash
> solidity-project@1.0.0 test
> hardhat coverage


Version
=======
> solidity-coverage: v0.7.16

Instrumenting for coverage...
=============================

> MyContract.sol

Compilation:
============

Compiling 1 file with 0.8.5
Compilation finished successfully

Network Info
============
> HardhatEVM: v2.3.3
> network:    hardhat



  MyContract
    ??? should return its name (174ms)
    ??? should change its name when requested (106ms)


  2 passing (283ms)

-----------------|----------|----------|----------|----------|----------------|
File             |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
-----------------|----------|----------|----------|----------|----------------|
 contracts/      |      100 |      100 |      100 |      100 |                |
  MyContract.sol |      100 |      100 |      100 |      100 |                |
-----------------|----------|----------|----------|----------|----------------|
All files        |      100 |      100 |      100 |      100 |                |
-----------------|----------|----------|----------|----------|----------------|

> Istanbul reports written to ./coverage/ and ./coverage.json



```

Congratulations! Your tests pass - time to think about how to deploy your contract.

# Deploying Your Contract

Solidity is no language that runs on every machine. It runs within the Ethereum VM that is a part of Ethereum nodes. Your code needs to be deployed to the blockchain to be usable.

Hardhat comes with a task runner that is a great help in automating this task. Those tasks are nothing else than JavaScript files that are executed on demand.

Copy this code and put it into a new file scripts/deployMyContract.js:

```javascript

async function main() {
  const MyContract = await ethers.getContractFactory("MyContract");
  const myContract = await MyContract.deploy("My Contract");

  console.log("My Contract deployed to:", myContract.address);
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
});


```

You might find some lines you've already seen before in your tests. Yes, you can use the same instantiation logic you used within your tests here.

It is good practice to never directly deploy your contracts out to the world. Gladly, Hardhat comes with a local testnet where you can test your contracts and play around with them locally.

Add the following script to your package.json:


```javascript
"deploy:local": "hardhat run --network localhost scripts/deployMyContract.js"


```

The command uses Hardhat to execute your script and defines the target network as localhost.

Next, you need a local testnet so that you have somewhere to deploy your contract.

Add another script to your package.json:






```javascript
"local-testnet": "hardhat node"



```

Your package.json should look similar to this now:

```javascript
{
  "name": "solidity-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "hardhat compile",
    "test:light": "hardhat test",
    "test": "hardhat coverage",
    "deploy:local": "hardhat run --network localhost scripts/deployMyContract.js",
    "local-testnet": "hardhat node"
  },
  "keywords": [],
  "author": "Oliver Jumpertz",
  "license": "ISC",
  "devDependencies": {
    "@nomiclabs/hardhat-ethers": "^2.0.2",
    "@nomiclabs/hardhat-waffle": "^2.0.1",
    "chai": "^4.3.4",
    "ethereum-waffle": "^3.4.0",
    "ethers": "^5.3.1",
    "hardhat": "^2.4.0",
    "solidity-coverage": "^0.7.16"
  }
}




```

You have everything you need to deploy your contract locally ready. Now open a new terminal (tab) and execute the following command:


```bash
npm run local-testnet


```

The output should look something like this:


```bash
> solidity-project@1.0.0 local-testnet
> hardhat node

Started HTTP and WebSocket JSON-RPC server at http://127.0.0.1:8545/

Accounts
========
Account #0: 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 (10000 ETH)
Private Key: 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80

Account #1: 0x70997970c51812dc3a010c7d01b50e0d17dc79c8 (10000 ETH)
Private Key: 0x59c6995e998f97a5a0044966f0945389dc9e86dae88c7a8412f4603b6b78690d

Account #2: 0x3c44cdddb6a900fa2b585dd299e03d12fa4293bc (10000 ETH)
Private Key: 0x5de4111afa1a4b94908f83103eb1f1706367c2e68ca870fc3fb9a804cdab365a

Account #3: 0x90f79bf6eb2c4f870365e785982e1f101e93b906 (10000 ETH)
Private Key: 0x7c852118294e51e653712a81e05800f419141751be58f605c371e15141b007a6

Account #4: 0x15d34aaf54267db7d7c367839aaf71a00a2c6a65 (10000 ETH)
Private Key: 0x47e179ec197488593b187f80a00eb0da91f1b9d0b13f8733639f19c30a34926a

Account #5: 0x9965507d1a55bcc2695c58ba16fb37d819b0a4dc (10000 ETH)
Private Key: 0x8b3a350cf5c34c9194ca85829a2df0ec3153be0318b5e2d3348e872092edffba

Account #6: 0x976ea74026e726554db657fa54763abd0c3a0aa9 (10000 ETH)
Private Key: 0x92db14e403b83dfe3df233f83dfa3a0d7096f21ca9b0d6d6b8d88b2b4ec1564e

Account #7: 0x14dc79964da2c08b23698b3d3cc7ca32193d9955 (10000 ETH)
Private Key: 0x4bbbf85ce3377467afe5d46f804f221813b2bb87f24d81f60f1fcdbf7cbf4356

Account #8: 0x23618e81e3f5cdf7f54c3d65f7fbc0abf5b21e8f (10000 ETH)
Private Key: 0xdbda1821b80551c9d65939329250298aa3472ba22feea921c0cf5d620ea67b97

Account #9: 0xa0ee7a142d267c1f36714e4a8f75612f20a79720 (10000 ETH)
Private Key: 0x2a871d0798f97d79848a013d4936a73bf4cc922c825d33c1cf7073dff6d409c6

Account #10: 0xbcd4042de499d14e55001ccbb24a551f3b954096 (10000 ETH)
Private Key: 0xf214f2b2cd398c806f84e317254e0f0b801d0643303237d97a22a48e01628897

Account #11: 0x71be63f3384f5fb98995898a86b02fb2426c5788 (10000 ETH)
Private Key: 0x701b615bbdfb9de65240bc28bd21bbc0d996645a3dd57e7b12bc2bdf6f192c82

Account #12: 0xfabb0ac9d68b0b445fb7357272ff202c5651694a (10000 ETH)
Private Key: 0xa267530f49f8280200edf313ee7af6b827f2a8bce2897751d06a843f644967b1

Account #13: 0x1cbd3b2770909d4e10f157cabc84c7264073c9ec (10000 ETH)
Private Key: 0x47c99abed3324a2707c28affff1267e45918ec8c3f20b8aa892e8b065d2942dd

Account #14: 0xdf3e18d64bc6a983f673ab319ccae4f1a57c7097 (10000 ETH)
Private Key: 0xc526ee95bf44d8fc405a158bb884d9d1238d99f0612e9f33d006bb0789009aaa

Account #15: 0xcd3b766ccdd6ae721141f452c550ca635964ce71 (10000 ETH)
Private Key: 0x8166f546bab6da521a8369cab06c5d2b9e46670292d85c875ee9ec20e84ffb61

Account #16: 0x2546bcd3c84621e976d8185a91a922ae77ecec30 (10000 ETH)
Private Key: 0xea6c44ac03bff858b476bba40716402b03e41b8e97e276d1baec7c37d42484a0

Account #17: 0xbda5747bfd65f08deb54cb465eb87d40e51b197e (10000 ETH)
Private Key: 0x689af8efa8c651a91ad287602527f3af2fe9f6501a7ac4b061667b5a93e037fd

Account #18: 0xdd2fd4581271e230360230f9337d5c0430bf44c0 (10000 ETH)
Private Key: 0xde9be858da4a475276426320d5e9262ecfc3ba460bfac56360bfa6c4c28b4ee0

Account #19: 0x8626f6940e2eb28930efb4cef49b2d1f2c9c1199 (10000 ETH)
Private Key: 0xdf57089febbacf7ba0bc227dafbffa9fc08a93fdc68e1e42411a14efcf23656e


```


Hardhat started a local Ethereum network for you and printed out all existing accounts, including their private keys. Before you ask: No, you can't move all the Ether to the main net. Sorry, this is only fake Ether to play and test with.

Now switch back to your original terminal (tab) and run:


```bash

npm run deploy:local

```

This should create output like this:

```bash

> solidity-project@1.0.0 deploy:local
> hardhat run --network localhost scripts/deployMyContract.js

Compiling 1 file with 0.8.5
Compilation finished successfully
My Contract deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
`


```


Congratulations, you successfully deployed your first smart contract to a local testnet!


# Conclusion


That's it. You have set up a local development environment, implemented your first smart contract, tested it, and then deployed it locally.

This setup is a pretty solid one, as it comes with well-maintained libraries and tools. It is also straightforward to use and scales pretty well. You can also extend it pretty easily, thanks to Hardhat tasks and npm's flexibility to simply add more scripts when you need them.

You can go on from here and play around. See what else you can create. It should be relatively straightforward to add more contracts to this project.











































