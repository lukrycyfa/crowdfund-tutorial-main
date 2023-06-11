# Developing Testing and Deploying A Crowdfund Smart Contract With Eth-Brownie On Celo Alfajores. 

- This tutorial put readers through developing, testing and deploying a crowdfund smart contract having extra Utilities and less abstraction that could be used in live cases. Included in the Smart Contract are not just utilities for funding’s but also utilities for a blog, where users and contributors on subjects, get informed and updates on fundings, tackling issues and could even grow a community. Another utility that will be created would be a utility for Handing out Awards in form of tokens to our donors since the contract will be based off an ERC721 Token standard Created for NFT's (Non fungible Tokens). [more on token standard here](https://ethereum.org/en/developers/docs/standards/tokens/). For the purpose of handing out tokens to our donors, This tutorial contains a reserved section that explains just enough for this projects, on Generative Art i.e. generating  unique images for our tokens using an art engine. A Dapp to this project is linked [here](https://crowdfund-dapp-seven.vercel.app/), a link to a boilerplate for the tutorial [here](https://github.com/lukrycyfa/crowdfund-tutorial-boilerplate) and a link to the [tutorial project here](https://github.com/lukrycyfa/crowdfund-tutorial-project).

- On completing this tutorial readers will be expected to understand and gain some expirience on how to develop deploy and test a smart contract on celo alfajores using Eth-brownie a Python Framework for developing and testing smart contracts, create scripts that could be used to interact with your contract on the chain using Python and gain some basic understanding on generative arts.

- ⏰ time for the tutorial

## 1.0 Required Tech-Stack's  🛠

- [Python](https://www.python.org/downloads/).

- [Node.js](https://nodejs.org/en/download). for ganache-cli.

- [Metamask-Browser-Extension](https://metamask.io). if you do not already have.

- [Eth-Brownie](https://pypi.org/project/eth-brownie/).

- [Ganache](https://www.npmjs.com/package/ganache).

- [nft-genrator-py](https://link/here).

## 2.0 Prerequisites... 🔑

- To get the most out of this tutorial the readers are belived to have some expirience in....
- Solidity Programming, and some expirience of writing smart contracts. link to a [tutorial on developing smart contracts](https://dacade.org/communities/celo/courses/celo-development-101/learning-modules/6c18d048-b3e0-47a0-bdc0-dae8076da410).
- Python Programming at an Intermidiate level. link to a [course on python](https://www.udemy.com/course/python-the-complete-python-developer-course/).

## 3.0 A Brief Overview On Smart Contracts, Celo, Eth-Brownie, Ganache And Generative Art

### 3.1 Smart Contracts

- Supposedly, smart contracts are contracts that are represented in code and executed by computers. These Contracts are not only created online but their very performance is enabled and guaranteed by a network of decentralized, co-operating computer nodes, known as blockchains. Originally, smart contracts were restricted within a limited range of transactions, predominantly financial instruments. Progressively, however, the surrounding narrative has become broader, implying that all contracts can be made smart or that many different obligations can be enforced by code. What started as a niche phenomenon in such areas as financial derivatives and prediction markets, is now poised to change the entire legal landscape and “revolutionize” commerce. Allegedly, smart contracts can streamline the contracting process, reduce transaction costs by eliminating intermediaries and, most importantly, simplify enforcement without the need to seek protection from traditional legal institutions, such as courts. The theories underpinning smart-contracts and blockchains combine multiple, interrelated threads all of which reflect an indiscriminate, if not irrational, fascination with certain technical characteristics of blockchains. They also reflect a surprising lack of trust in humans. As the latter are perceived as inherently biased and unreliable, things should be left to computers. Humans, especially bankers and judges, are fallible and not trustworthy.
- Computers, on the other hand, are objective, infallible and trustworthy.
- The very idea of smart contracts is thus inextricably tied to the elimination of human judgment, the reduction of dependence on financial intermediaries and, in many instances, a detachment from the legal system.
- In other, more commercially-oriented contexts, smart contracts can simply be seen as part of the broader trend to use technology to ensure a consistent application of legal rules and agreements.
(provide a screen shot depicting a smart contract)


### 3.2 Celo and Alfajores Testnet..

- Celo is a mobile-first blockchain that 

- Celo is the carbon-negative, mobile-first, EVM-compatible blockchain ecosystem leading a thriving new digital economy for all. Making decentralized financial (DeFi) tools and services accessible to anyone with a mobile phone. It aims to break down barriers by bringing the powerful benefits of DeFi to the users of the 6 billion smartphones in circulation today. The celo Afajores Testnet is a Celo test network for developers building on the Celo platform. It could be used to try out the Celo Wallet or Celo CLI. Other use cases specifically for this tutorial would be to test and deploy The Smart Contract we will be developing.. 

### 3.3 Eth-Brownie And Ganache

- what is Eth-brownie?

- Eth-brownie unlike other frameworks for developing and testing Smart Contract such as hardhat or truffle written in JavaScript, is Python based Targeting EVM's to achieve the same purpose and is built and depends much on web3.py. [need more on web3.py](https://web3py.readthedocs.io/en/stable/). Where you have developers that will be interested in developing and testing smart contracts in JavaScript this framework was built for developers who would prefer to do the same using python. To understand more on Eth-brownie and Usage [Read the Docs](https://eth-brownie.readthedocs.io/en/stable/).

- Having understood what Eth-brownie is let's have a look at its structure and some of its features.

    - Fully supports Solidity and Vyper programming languages for Developing Smart contracts.
    - Smart Contracts are tested via pytest library and include a trace-based coverage evaluation. 
    - Property-based and stateful testing via hypothesis for locating edge cases and discovering faulty assumptions within your code.
    - Utilize built-in powerful debugging tools, including python-style tracebacks and custom error strings.
    - Built-in python like console for quick project interaction (i.e. interacting with deployed contracts).
    - Support for ethPM packages.

#### 3.3.1 Creating A Project With Eth-Brownie..

- Projects in Eth-brownie could be created basically in two ways i.e. an initiated project or a template based project.

- Eth-brownie initiated projects could be created by creating a new directory, navigating to that directory with a terminal and issuing this command
```bash
$ brownie init
```
or

- A template based project from "Brownie mixes" as a starting point for your project. The command bellow gets you a template implementation of an ERC20 Token standard

```bash
$ brownie bake token
```

- For a template implementation of an ERC721 Token standard.
```bash
$ brownie bake nft
```
[more brownie mixies](https://github.com/brownie-mix/)

#### 3.3.2 Eth-Brownie Project Structure 📂

- Every brownie project is composed of these structure

- Contracts/: Contract sources
    - The contract directory holds the contract files in a project. Each time brownie is executed it looks up this directory for new files or an update in any existing file and makes updates to compiled sources. The default extensions for file in this directory are in the .sol for solidity files and .vy for vyper files.

- interfaces/: Interface sources
    - the interface directory holding interfaces sources that could be referenced in contract's, but  not really necessary except it has a source to be referenced in a contract in the project. The default extensions for file in this directory are in the .sol for solidity files and .vy for vyper files.

- Scripts/: Scripts for deployment and interactions
    - The script directory holds the scripts that will be utilized in deploying or interacting with our project via Brownie console. (Default extension for these files are in .py for python files)

- Tests/: 
    - This directory holds the scripts for testing our project via the console making use of pytest. (Default extension for these files are in .py for python files).

- These following directories are also created, and used internally by Brownie for managing the project. You should not edit or delete files within these folders.
    - build/: Project data such as compiler artifacts and unit test results
    - reports/: JSON report files for use in the GUI

<!-- - [An example tutorial on Eth-brownie usage on celo](https://celo.academy/t/building-a-smart-contract-lottery-application-on-celo-with-python/246) -->

#### 3.3.3 Accounts And Chains

- Having access to local accounts to interact with a local-chain and make transactions in Eth-brownie, is via Accounts a list-like object that contains Account objects. These accounts can be accessed on the console while making transactions or imported in a .py file to be used in the script.

(provide screenshots)

- Interacting with a Testnet is feasible with brownie, already having pre-configured testnets on it's list of networks or manually adding a network to brownie. You could access the list of networks configured on brownie using this command. 

```bash
$ brownie networks list
``` 
![network-list](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/network-list.png)

// am here
#### 3.3.4 Contracts

- Brownie provides a ContractContainer Object for each deployable contract in your project. They are list-like objects used to deploy new contracts. When a contract is deployed you are returned a Contract object that can be used to interact with it. This object is also added to the ContractContainer. Contract objects contain class methods for performing calls and transactions.

#### 3.3.5 Ganache...

- A local-Chain we will be using to test, deploy and interact with our smart contract 

- Interacting with our deployed contract, brownie console and other commands will be looked into when we get into creating our tutorial's project.

### 3.4 Generative Art...

- Generative art refers to Digital art Works that in a whole or in part has been created with the use of autonomous systems i.e. (creative code, artificial intelligence, or an algorithm). However, the term in a broader historical sense refers to any non-human entity that is capable of independently choosing aspects of a piece of art that would normally require a direct choice from an artist. [More resources on generative art](https://aiartists.org/generative-art-design).

## 4.0 The Project In Procedures And Steps

- This tutorial was created with readers in mind having to run into minimal or no issues while trying to work on the project in the tutorial. Most of the issues that might arise while working on the project had already been handled. Except for some core dependencies that may be missing on your machine or you do something that’s not plausible or not provided in the tutorial. For windows users while installing Dependencies  
- if you run into a .sh script not being executed, use a terminal that supports bash scripts(e.g. a git terminal)
- Or you run into issues that has to do with Visual Studio a link to the missing dependency will be provided on the terminal. 

### 4.1.0 Installing Depenencies and Packages. 🛠

- Get [Python](https://www.python.org/downloads/) v3.9 or >.

- Get [Node.js](https://nodejs.org/en/download). v16.16.0 or >.

- Install [Metamask-Browser-Extension](https://metamask.io/download/). If not already installed on your browser.
    - Install Metamask
    Go to metamask.io.
    Click on the download button, then click on install for your browser (e.g., Chrome) and add the extension to your browser.
    Create a wallet as described.

    - After setting up metamask you will need to create two additional accounts, export all three private keys and copy them somewhere safe we will be needing them later, alot in the project depends on that mostly our scripts for testing and interacting with alfajores testnet. (provide a video a gif or a link on doing that).
    ![additional_account](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/additional_account.gif)

    ![export_private_key](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/export_private_key.gif)

    - Connect Metamask to Alfajores
    - Click on "Ethereum Mainnet" in your MetaMask extension, then click on "Add Network".
    - You should see "Add a network manually" under the list of provided networks, click on it and.
    - Enter the data provided in this [Celo documentation](https://docs.celo.org/getting-started/wallets/using-metamask-with-celo/manual-setup). Make sure to choose the data for the Alfajores Testnet.

    - You would need to fund your newly created accounts with Celo Alfajores Faucets.
    Go to the Alfajores testnet faucet [here](https://faucet.celo.org/alfajores).
    Enter your wallet address and click on "Faucet".
    When you open your MetaMask extension, you should be able to see the Celo tokens you have received. To see the cUSD tokens, click on assets, then click on the "Import tokens" link, and enter "0x874069Fa1Eb16D44d622F2e0Ca25eeA172369bC1" as the "Token Contract Address".


#### 4.1.1 Installing Eth-Brownie..

- Eth-brownie Could be installed via "pipx", “pip" or cloning the repo and installing via the setup script. If you’re not familiar with pipx I suggest you use "pip" or clone the repo (🚨 i mean safety first 🚨).

- installing via pipx..

```bash
python -m pip install --user pipx
python -m pipx ensurepath
```

```bash
pipx install eth-brownie
```

- installing via pip..
```bash
pip install eth-brownie
```

- installing from a cloned repo..
```bash
git clone https://github.com/eth-brownie/brownie.git
cd brownie
python setup.py install
```

```bash
brownie
```

![brownie](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/brownie.png).

#### 4.1.2 Installing Ganche-cli

```bash
npm install ganache --global
```

#### 4.1.3 Installing The Generative Art Engine

```bash
git clone https://github.com/lukrycyfa/nft-generator-py.git
```
```bash
cd nft-generator-py
python -m pip install -r requirements.txt
```

#### 4.1.4 Installing The Contract Dependencies

- instaling OpenZeppelin-contracts library needed for writing our smart contract.
```bash
brownie pm install OpenZeppelin/openzeppelin-contracts@4.8.2
```

- verify the installed package
```bash
brownie pm list
```
![pm-list](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/pm-list.png)

#### 4.1.5 Adding Alfajores Testnet To Brownie

- Add Celo alfajores testnet to brownie for deploying our Contract on the testnet.
    - where:
        - name: Alfajores alfajores
        - host: 'https://alfajores-forno.celo-testnet.org'
        - chainId: 44787
        - explorer: 'https://alfajores-blockscout.celo-testnet.org'

```bash
brownie networks add Alfajores alfajores host=https://alfajores-forno.celo-testnet.org chainid=44787 explorer=https://alfajores-blockscout.celo-testnet.org
```
```bash
brownie networks list
```
![network-list](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/network-list.png)


### 4.2 Developing, Deploying And Testing Our CrowdFund Smart Contract.

- In this section we will be Developing, deploying and testing our smart contract on ganache and celo testnet(alfajores). This section may require much attention as it's the core of this tutorial. We will get to understand more on Eth-Brownie, its scripts, tests, interacting with our deployed contract from the console and more. We would also take the liberty of looking into specifiers, modifiers, variables and some data-types we will be using while creating the smart contract as a recap to your understanding in Solidity Programming.

#### 4.2.0 Developing The Smart Contract.

- I have created a boilerplate to this tutorial located [here](https://github.com/lukrycyfa/crowdfund-tutorial-boilerplate). If you would prefer using the boilerplate, do make sure you have all dependencies installed then update, create or rename file's that need to be as you go through the tutorial.

##### 4.2.0.1 Initializing The Project

- Lets Start by creating an initiated brownie project. In a terminal and an empty directory of your choice issue this command.

```bash
mkdir project_dir_name
cd project_dir_name
brownie init
```
![init](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/init.png)

- You should have this expected project structure.

![project-structure](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/project-structure.png)

##### 4.2.0.2 Creating The Smart Contract

- like any other programming language Solidity utilize data-type and variables to create functionalities and store data. It further utilize specifiers and modifiers to create restrictions and keep functionalities within confines. More details on features we will be utilizing are seen below. [Read The Docs](https://docs.soliditylang.org/en/v0.8.20/) if you need more on solidity programming.

- Data Types
    - uint: unsigned integer of 256 bits (could also come in bits of different sizes) 
    - strings: String literals e.g("foo" or 'bar') 
    - arrays: Arrays can ba of a fixed size, or they can be dynamically size.
    - mappings: Mappings are like dicts in python. but in solidity a hash-table virtually initialized where every possible value exists and is mapped to a value.
    - structs: Structs are custom defined types that can group several variables.
    - address: Holds a 20 byte value (size of an Ethereum address) e.g an wallet address or a contract address.
    - bool: basically a boolean.

- Variables
    - state variables: variables stored on the blockchain and will cost gas.
    - local variables: variables stored temporary in memory and not saved.
    - global variables: exist in the global namespace, example of a global variable we will be utilising is `msg` which includes `msg.sender` and `msg.value`.

- Visibility Specifiers
    - public: visible externally and internally (use while creating a getter function for storage/state variables)
    - private: only visible within the current contract. 

- Modifiers
    - view for functions: added to disallow modification of states. utilized in a getter function.
    - payable for functions: Applied to functions that invovles sending tokens allowing the token to be received together with a call.
    - onlyowner for functions: Applied to functions, to be called only by the owner of the contract.
    - virtual for functions and modifiers: Allows the function’s or modifier’s behaviour to be changed in derived contracts.
    - override: States that this function, modifier or public state variable changes the behaviour of a function or modifier in a base contract.

- Require: a function taking an expression like condition to return a bool, that needs to be met as its first argument and a string that is returned if the first argument is not met as its second argument. 
 
- Let's create our Crowdfund smart contract explaing its utilities and functionalities as we walk through. 
- Create a Crowdfund.sol file in the. /contracts directory. By default every contract to be created in an Eth-brownie project goes into this directory. 

- Now let's get into the Crowdfund Smart Contract by Code blocks.

- The first line should specify that the source code is licensed under the GPL version 3.0.
- The next line is a Pragma. Pragma’s are instructions to compilers on how to handle the code, here it specifies that the source code was written in Solidity version > 0.7 and < 0.9 and should be compiled with a similar versioned compiler.

```sol

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L2).

- This next block are the imported libraries and modules required by the contract from the OpenZeppelin-contracts library.
    - The first line imports ERC721.sol, to base our contract off this token standard. We will be needing some of the functions from its interface.
    - the second line imports ERC721Enumerable.sol, implying the tokens in this contract and token's owned by accounts on this contract could be enumerated.
    - the third line imports ERC721URIStorage.sol, Implying the contract supports the storage of tokens Uri's generated on it.
    - The fourth line imports Ownable.sol, giving some access control mechanism. Basically it gives you access to a mechanism like the onlyowner modifier.
    - The fifth line imports Counters.sol, a module that provide values that could be incremented and decremented with its methods mostly to keep tracks on ID’s.

```sol

import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/token/ERC721/ERC721.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/token/ERC721/extensions/ERC721Enumerable.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/access/Ownable.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/utils/Counters.sol";

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L8).

- On this line we define our contract as an ERC721, ERC721Enumerable, ERC721URIStorage and an Ownable Contract.

```sol

contract FundRaiser is ERC721, ERC721Enumerable, ERC721URIStorage, Ownable {
        //// lines ommited
        //// lines ommited
}

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L11).

- On the next four lines we would create four instances of the Counter method that will be used for these private variables on the next for line's i.e. `_DonorsCount`, `_PostsCount`, `_ActPstCount` and `_tokenIdCounter`. The Counter instances will be used to keep track of the values to the variables.

```sol

    using Counters for Counters.Counter;
    using Counters for Counters.Counter;
    using Counters for Counters.Counter;
    using Counters for Counters.Counter; 
    Counters.Counter private _DonorsCount;
    Counters.Counter private _PostsCount;
    Counters.Counter private _ActPstCount; 
    Counters.Counter private _tokenIdCounter;

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L24).


- Next we are creating our variable's for `_TotalDonations` and `_DonationBalance` and applying `public` and `private` specifiers to them.

```sol

    uint public _TotalDonations;
    uint private _DonationBalance;

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L30).

- Now we will need to identify a donor, a post and who is liking a post so...
    - Here we will be creating three structs the first struct for a `Donor` having variables `donorsIdx`, `adr`, `amount` and `donCount`.
    - the second struct for a `Post` having variables `postIdx`, `author`, `post`, `slug` and `likecount`.
    - And the third struct for a `likeAdrs`. With variables `user` and `liked`.

```sol

    struct Donor{ 
        uint donorsIdx;  
        address adr;  
        uint amount; 
        uint donCount;    
    }

    struct Post{ 
        uint postIdx;  
        address author;  
        string post;
        string slug;
        uint likecount;     
    }

    struct likeAdrs{
      address user;
      bool liked;
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L35).


- On these next lines we will create Mappings for instances of the above identifiyers. So when making calls to functions that create those instances they are saved as state variables.
    - On this block we will create three mappings the first map is for our `PostLikes` Mapping a postId to a mapping that maps an address to a `LikeAdrs` Struct
    - the second `AllPosts` maps a postId to a `Post` Struct,
    - the third `AllDonors` maps a address to a `Donor` Struct.
    - and the last line is an array for our donors addresses which we will be using for refrencing, and returning values from `Alldonors` later.

```sol

    mapping(uint => mapping(address => likeAdrs)) public PostLikes;

    mapping(uint => Post) public AllPosts;

    mapping(address  => Donor) public AllDonors;

    address[] public DonorsAdrLst;

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L70).

- This Block of the code will be where we initiate our constructor, which is executed when a Contract Deployed. Here you could assigne values to already defined state variables you need to at deployment. So we are incrementing our `_tokenIdCounter` to begin the token count at 1. Before subsequent updates to be made deploying the contract. 

```sol

    //Initiated At first Contract Deployment.
    constructor() ERC721("FundRaiserNFTs", "FRN") { 
          // Initialize the tokenIdCounter to start 1
         _tokenIdCounter.increment();
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L74).

- In the next block of code we will be creating our event emitters. Think of an event emitter as an Object added to the transaction Object created from some values you defined.
    - The first will be for events a Token was minted.
    - The second will be for events a Donation was made.
    - The third will be for events Donations were Transferred.
    - The fourth for events a post was added.
    - The fifth will be for events a Post was liked.
    - The sixth will be for events a Post Was Deleted.

```sol

    event TokenMinted( address sender, uint tokenId );
    event DonationMade( address sender, uint amount );
    event DonationTransfered( address sender, uint amount ); 
    event NewPostAdded( address sender, string slug );
    event LikedPost( address sender, uint postId, bool liked );
    event DeletedPost( address sender, uint postId );

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L83).

- In the next couple of code blocks we will be creating functions defined for the crowdfund utility in our contract.

- In this block of code we create our `safeMint()` function to mint awards to our donors, having some conditions to meet before the minting process is possible.
- The first line defines the function with an argument of a string `uri` then a `public` `specifier`. The second line makes use of require to assert that the amount of times the user has donated is > amount of token's on the users wallet to guarantees a mint.
- the third line assigns a new tokenId from the current `_tokenIdCounter` value, the fourth line increments the `_tokenIdCounter `for the next mint, the fifth and sixth `_safeMint` the token to the caller and assigns the `uri` to the token. While the last line is our event emitter emitting a token has been minted.

```sol

    function safeMint(string memory uri) public {
        require(AllDonors[msg.sender].donCount > balanceOf(msg.sender), "The Connected account is Not eligible to Mint token"); 
        uint256 tokenId = _tokenIdCounter.current(); 
        _tokenIdCounter.increment();    
        _safeMint(msg.sender, tokenId);
        _setTokenURI(tokenId, uri);
        emit TokenMinted(msg.sender, tokenId); 
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L95).

- This next block creates our `Donate()` function to accept donations made to the crowdfund.
    - the first line defines the function adding a `public` `specifier` and a `modifier` `payable`, the second and third lines makes use of require to assert first that the caller is not the `contract owner` and the next asserting the value sent for donation is not < the minimum donation value.
    - The fourth line transfers the donation to the `contract owner`, the next line makes update to `_TotalDonations` & `_DonationBalance` 
    - the next block checks if the caller had made a donation before and updates the necessary variables then emits a donation has been made,  
    - Else a new `Donor` struct should be created using the next block for the caller and a DonationMade Even is emitted. 

```sol

    function Donate() public payable {
        require(msg.sender != owner(), "Donations Can Not Be Made By The Contract Owner");
        require(msg.value >= (10**18)*2, "Sent Value Below Minimum Donation");
        payable(owner()).transfer(msg.value);
        _TotalDonations += msg.value;
        _DonationBalance += msg.value;
        if(AllDonors[msg.sender].adr == msg.sender ){
            AllDonors[msg.sender].amount += msg.value;
            AllDonors[msg.sender].donCount +=1;
            emit DonationMade(msg.sender, msg.value);  
            return;
        }        
        Donor storage D = AllDonors[msg.sender];
        D.donorsIdx = _DonorsCount.current();
        _DonorsCount.increment();
        D.adr = msg.sender;
        D.amount = msg.value;
        D.donCount +=1;
        DonorsAdrLst.push(msg.sender);
        emit DonationMade(msg.sender, msg.value); 
        return;
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L108).

- Next we create a function that makes transfers of donations to other accounts just in cases where a project will be needing funding.
    - Here we first define our `TransferDonations()` function  with the `payable` `modifier` assigned to the `adr` argument  we will be transfering the donation to. Then apply the `payable`, `onlyOwner` `modifiers` and a `public` `specifier` to the function. 
    - The next two lines makes use of the require function restricting transfers to the owners account and asserting the value to be transferred is < `_DonationBalance`. 
    - The last three lines makes the transfer, updates the donation balance and emits the DonationTransfered Event.

```sol

    function TransferDonations(address payable adr) public payable onlyOwner {
        require(msg.sender != adr, "Transfer To Own Account Is Not Valid");
        require(msg.value < _DonationBalance, "Withdrawal Limits Excceded");
        adr.transfer(msg.value);
        _DonationBalance -= msg.value;
        emit DonationTransfered(msg.sender, msg.value);
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L134).

- The next block is created to return an array or in Eth-brownies case a tuple containing addresses of donors.
    - We define the `DonorAdr()` function with the `public` `specifier`, the `onlyOwner` and `view` `modifiers` which returns an fixed array of addresses using a for loop and the `DonorsAdrLst` array.   

```sol

    function DonorAdr() public view onlyOwner returns (address[] memory)
    {
        address[] memory Adrs = new address[](DonorsAdrLst.length);
        for (uint256 i = 0; i < DonorsAdrLst.length; i++) {   
            Adrs[i] = DonorsAdrLst[i]; 
        }
        return Adrs;
    }    

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L146).

- This next function `_donationtBalance()` returns `_DonationBalance`. Defined with `public` `specifier`, the `onlyOwner` and `view` `modifiers`.

```sol

    function _donationtBalance() public onlyOwner view returns( uint ){
        return _DonationBalance;
    }  

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L159).

- On this last block of the Crowdfund utitlity we create a function `OwnWallet()` Defined with `public` `specifier` and `view` `modifiers`. Returning an enumerated array of token's owned by the connected account. By getting the balance of the connected account and iterating over it.

```sol

    function OwnWallet()public view returns (uint256[] memory)
    {
        uint256 ownerTokenCount = balanceOf(msg.sender);
        uint256[] memory tokenIds = new uint256[](ownerTokenCount);
        for (uint256 i = 0; i < ownerTokenCount; i++) {
            tokenIds[i] = tokenOfOwnerByIndex(msg.sender, i); 
        }
        return tokenIds;
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L163).

- In this section we will be creating functions that will be utilized to interact with the blog (again why i feel one might need of a blog on a crowdfund project is to actually keep a growing audience of donor and people interested in our goal and purpose however this isn’t a blog with complete features).
    - In the next block we are creating is the `NewPost()` function, taking two strings as arguments a `post` and a `slug` and applying the `public` `specifier`. 
    - the second line makes use of the require function, making assertions on the post, 
    - the third to fifth line creates an instance of a Post, 
    - the next two line's increments `_PostsCount`, `_ActPstCount` and the last emits the `NewPostAdded` Event. 

```sol

    function NewPost(string memory post, string memory slug) public {
      require(bytes(post).length > 0, "Invalid Post");
      Post storage P = AllPosts[_PostsCount.current()];
      P.postIdx = _PostsCount.current();
      P.author = msg.sender;
      P.post = post;
      P.slug = slug; 
      _PostsCount.increment();
      _ActPstCount.increment();
      emit NewPostAdded(msg.sender, slug);      
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L178).

- Next we create a function to like and unlike our posts, the function takes an argument of a `postId` and a `public` `specifier`. 
    - The next line asserts the post is a valid post, the third line looks up if there is a `likeAdrs` instance for the caller.
    - The next five lines updates the liked status to `false` the next four updates the liked status to `true `, 
    - The next six lines creates a new `likeAdrs` instance of the caller on that post if the caller's instance never existed and emits the `LikedPost` Event.

```sol

    function LikeandUnlikePost(uint postId) public {
        require(AllPosts[postId].postIdx == postId, "Invalid... Post Does Not Exist");
        if(PostLikes[postId][msg.sender].user == msg.sender){
            if(PostLikes[postId][msg.sender].liked == true){
                  PostLikes[postId][msg.sender].liked = false;
                  AllPosts[postId].likecount -= 1;
                  emit LikedPost(msg.sender, postId, false);
                  return;
            }
            PostLikes[postId][msg.sender].liked = true;
            AllPosts[postId].likecount += 1;
            emit LikedPost(msg.sender, postId, true);
            return;
        }
        AllPosts[postId].likecount += 1;
        likeAdrs storage l = PostLikes[postId][msg.sender];
        l.user = msg.sender;
        l.liked = true;
        emit LikedPost(msg.sender, postId, true);
        return;
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L194).

- The next block is a function we are creating  `ReturnLiked()` taking `postId` as an argument, and applying a `public` `specifier`, a `view` `modifier` and it returns a `bool` 
    - the second line asserts the post is a valid post the third line looks up if the caller has an instance on that post and 
    - the last two line returns the liked status of that user on that post.

```sol

    function ReturnLiked(uint postId) public view returns (bool)
    {
        require(AllPosts[postId].postIdx == postId, "invalid... Post Does Not Exist");
        if (PostLikes[postId][msg.sender].user != msg.sender){
            return false;
        }  
        bool Liked = PostLikes[postId][msg.sender].liked;
        return Liked;
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L220).

- This block defines the `DeletePost()` function, taking an argument of a `postId` and a `public` `specifier`. 
    - The second and third line's asserts the post is a valid one and the caller is the author of the post.
    - the last three line's delete's the post, decrement the `_ActPstCount` and emits The DeletePost Event.

```sol

    function DeletePost(uint postId) public{
        require(AllPosts[postId].postIdx == postId, "Invalid.. Post Does Not Exist");
        require(AllPosts[postId].author == msg.sender, "Account Unathorized To Delete Post");
        delete AllPosts[postId];
        _ActPstCount.decrement();
        emit DeletedPost(msg.sender, postId);
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L234).

- The last block for our Blog utility is a function `ReturnPosts()` with a a `public` `specifier`, a `view` `modifier` we create to return an array of active post. Utilizing a loop to iterate over active posts. 

```sol

    function ReturnPosts() public view returns (Post[] memory)
    { 
        uint idx = 0;
        Post[] memory Posts = new Post[](_ActPstCount.current());
        for (uint i = 0; i < _PostsCount.current(); i++) { 
              if(bytes(AllPosts[i].post).length > 0){
                  Posts[idx] = AllPosts[i];
                  idx++;
              }  
        }
        return Posts;
    }

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L246).

- This block of functions are overrides required by solidity. I.e. making a call to any of these functions initiates an override on the contract.

```sol 

    // The following functions are overrides required by Solidity.
    function _beforeTokenTransfer(address from, address to, uint256 tokenId, uint256 batchSize)
      internal
      override(ERC721, ERC721Enumerable)
    {
      super._beforeTokenTransfer(from, to, tokenId, batchSize);
    }

    function supportsInterface(bytes4 interfaceId)
      public
      view
      override(ERC721, ERC721Enumerable)
      returns (bool)
    {
      return super.supportsInterface(interfaceId);
    }

    function _burn(uint256 tokenId) internal override(ERC721, ERC721URIStorage) {
      super._burn(tokenId);    
    }

    // Returns The Token URI Of The Requested Token.
    function tokenURI(uint256 tokenId)
      public
      view
      virtual
      override(ERC721, ERC721URIStorage)
      returns (string memory)
    {
      require(
        _exists(tokenId),
        "ERC721Metadata: URI query for nonexistent token"
      );
    
        return super.tokenURI(tokenId);

    } 

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol#L260).


#### 4.2.1 The Crowd Fund Smart Contract.

- This is what your entire Crowdfund.sol contract should look like. 

```sol

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/token/ERC721/ERC721.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/token/ERC721/extensions/ERC721Enumerable.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/access/Ownable.sol";
import "OpenZeppelin/openzeppelin-contracts@4.8.2/contracts/utils/Counters.sol";


contract FundRaiser is ERC721, ERC721Enumerable, ERC721URIStorage, Ownable {
    
    using Counters for Counters.Counter;
    using Counters for Counters.Counter;
    using Counters for Counters.Counter;
    using Counters for Counters.Counter; 
    Counters.Counter private _DonorsCount;
    Counters.Counter private _PostsCount;
    Counters.Counter private _ActPstCount; 
    Counters.Counter private _tokenIdCounter;

    uint public _TotalDonations;
    uint private _DonationBalance;

    struct Donor{ 
        uint donorsIdx;  
        address adr;  
        uint amount; 
        uint donCount;    
    }

    struct Post{ 
        uint postIdx;  
        address author;  
        string post;
        string slug;
        uint likecount;     
    }

    struct likeAdrs{
      address user;
      bool liked;
    }

    mapping(uint => mapping(address => likeAdrs)) public PostLikes;

    mapping(uint => Post) public AllPosts;

    mapping(address  => Donor) public AllDonors;

    address[] public DonorsAdrLst;

    
    //Initiated At first Contract Deployment.
    constructor() ERC721("FundRaiserNFTs", "FRN") { 
          // Initialize the tokenIdCounter to start 1
         _tokenIdCounter.increment();
    }


    event TokenMinted( address sender, uint tokenId );
    event DonationMade( address sender, uint amount );
    event DonationTransfered( address sender, uint amount ); 
    event NewPostAdded( address sender, string slug );
    event LikedPost( address sender, uint postId, bool liked );
    event DeletedPost( address sender, uint postId );


    // CROWDFUND SECTION
    function safeMint(string memory uri) public {
        require(AllDonors[msg.sender].donCount > balanceOf(msg.sender), "The Connected account is Not eligible to Mint token"); 
        uint256 tokenId = _tokenIdCounter.current(); 
        _tokenIdCounter.increment();    
        _safeMint(msg.sender, tokenId);
        _setTokenURI(tokenId, uri);
        emit TokenMinted(msg.sender, tokenId); 
    }


    // checked updated this....
    function Donate() public payable {
        require(msg.sender != owner(), "Donations Can Not Be Made By The Contract Owner");
        require(msg.value >= (10**18)*2, "Sent Value Below Minimum Donation");
        payable(owner()).transfer(msg.value);
        _TotalDonations += msg.value;
        _DonationBalance += msg.value;
        if(AllDonors[msg.sender].adr == msg.sender ){
            AllDonors[msg.sender].amount += msg.value;
            AllDonors[msg.sender].donCount +=1;
            emit DonationMade(msg.sender, msg.value);  
            return;
        }        
        Donor storage D = AllDonors[msg.sender];
        D.donorsIdx = _DonorsCount.current();
        _DonorsCount.increment();
        D.adr = msg.sender;
        D.amount = msg.value;
        D.donCount +=1;
        DonorsAdrLst.push(msg.sender);
        emit DonationMade(msg.sender, msg.value); 
        return;
    }


    function TransferDonations(address payable adr) public payable onlyOwner {
        require(msg.sender != adr, "Transfer To Own Account Is Not Valid");
        require(msg.value < _DonationBalance, "Withdrawal Limits Excceded");
        adr.transfer(msg.value);
        _DonationBalance -= msg.value;
        emit DonationTransfered(msg.sender, msg.value);
    }


    function DonorAdr() public view onlyOwner returns (address[] memory)
    {
        address[] memory Adrs = new address[](DonorsAdrLst.length);
        for (uint256 i = 0; i < DonorsAdrLst.length; i++) {   
            Adrs[i] = DonorsAdrLst[i]; 
        }
        return Adrs;
    }    


    function _donationtBalance() public onlyOwner view returns( uint ){
        return _DonationBalance;
    }  

    function OwnWallet()public view returns (uint256[] memory)
    {
        uint256 ownerTokenCount = balanceOf(msg.sender);
        uint256[] memory tokenIds = new uint256[](ownerTokenCount);
        for (uint256 i = 0; i < ownerTokenCount; i++) {
            tokenIds[i] = tokenOfOwnerByIndex(msg.sender, i); 
        }
        return tokenIds;
    }


    // BLOG SECTION
    function NewPost(string memory post, string memory slug) public {
        require(bytes(post).length > 0, "Invalid Post");
        Post storage P = AllPosts[_PostsCount.current()];
        P.postIdx = _PostsCount.current();
        P.author = msg.sender;
        P.post = post;
        P.slug = slug; 
        _PostsCount.increment();
        _ActPstCount.increment();
        emit NewPostAdded(msg.sender, slug);      
    }


    function LikeandUnlikePost(uint postId) public {
        require(AllPosts[postId].postIdx == postId, "Invalid... Post Does Not Exist");
        if(PostLikes[postId][msg.sender].user == msg.sender){
            if(PostLikes[postId][msg.sender].liked ==  true){
                  PostLikes[postId][msg.sender].liked = false;
                  AllPosts[postId].likecount -= 1;
                  emit LikedPost(msg.sender, postId, false);
                  return;
            }
            PostLikes[postId][msg.sender].liked = true;
            AllPosts[postId].likecount += 1;
            emit LikedPost(msg.sender, postId, true);
            return;
        }
        AllPosts[postId].likecount += 1;
        likeAdrs storage l = PostLikes[postId][msg.sender];
        l.user = msg.sender;
        l.liked = true;
        emit LikedPost(msg.sender, postId, true);
        return;
    }

    function ReturnLiked(uint postId) public view returns (bool)
    {
        require(AllPosts[postId].postIdx == postId, "invalid... Post Does Not Exist");
        if (PostLikes[postId][msg.sender].user != msg.sender){
            return false;
        }  
        bool Liked = PostLikes[postId][msg.sender].liked;
        return Liked;
    }

    function DeletePost(uint postId) public{
        require(AllPosts[postId].postIdx == postId, "Invalid.. Post Does Not Exist");
        require(AllPosts[postId].author == msg.sender, "Account Unathorized To Delete Post");
        delete AllPosts[postId];
        _ActPstCount.decrement();
        emit DeletedPost(msg.sender, postId);
    }
   
    function ReturnPosts() public view returns (Post[] memory)
    { 
        uint idx = 0;
        Post[] memory Posts = new Post[](_ActPstCount.current());
        for (uint i = 0; i < _PostsCount.current(); i++) { 
              if(bytes(AllPosts[i].post).length > 0){
                  Posts[idx] = AllPosts[i];
                  idx++;
              }  
        }
        return Posts;
    }

    // The following functions are overrides required by Solidity.
    function _beforeTokenTransfer(address from, address to, uint256 tokenId, uint256 batchSize)
      internal
      override(ERC721, ERC721Enumerable)
    {
      super._beforeTokenTransfer(from, to, tokenId, batchSize);
    }

    function supportsInterface(bytes4 interfaceId)
      public
      view
      override(ERC721, ERC721Enumerable)
      returns (bool)
    {
      return super.supportsInterface(interfaceId);
    }

    function _burn(uint256 tokenId) internal override(ERC721, ERC721URIStorage) {
      super._burn(tokenId);
        
    }
    // Returns The Token URI Of The Requested Token.
    function tokenURI(uint256 tokenId)
      public
      view
      virtual
      override(ERC721, ERC721URIStorage)
      returns (string memory)
    {
      require(
        _exists(tokenId),
        "ERC721Metadata: URI query for nonexistent token"
      );
    
        return super.tokenURI(tokenId);

    }  

}

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/contracts/Crowdfund.sol).


#### 4.2.2 Deploying The Smart Contract

- To interact or make use of our contract either locally or on the testnet our contract needs to be compiled and then deployed for that purpose we will be creating a deploy script to deploy our contract, a config file for deployment configurations and a .env files for our keys. In the ./scripts the default directory for scripts create a deploy.py file to populate with our deploy script, create a brownie-config.yaml file in the root directory (brownie-config.yaml default naming convention for a brownie config file) for our deployment configuration and a .env file we will use to populate our key's.

- By default when creating an Eth-brownie script a `main()` function should be defined in it (e.g. in a deploy.py file), so when the script is called the function is executed e.g. `brownie run deploy.py` executes the `main()` in it. 
- Here is another way to creating and calling an Eth-brownie script having several functions. Create the script (e.g. running.py) define your functions e.g. `getBlogs()` or `getDonations()` and while calling the script just call the function alongside the script i.e. `brownie run running.py getBlogs` or `brownie run running.py getDonations`. For the deploy script we will be using the default approach and use the other method for the scripts we will be using to interact with our project on the chain.

- Create the .env file and populate these keys with the extracted keys from the previously created metamask accounts and do make sure you have funded accounts.

```.env
export PRIVATE_KEY_OWNER=
export PRIVATE_KEY_ACC1=
export PRIVATE_KEY_ACC2=

```


- Create the brownie-config.yaml file and populate it with this block of code.
    - Basically the config file holds configurations for deploying our contract.

```yaml

    project_structure:
        build: build/contracts
        
    autofetch_sources: True
    dotenv: .env

    networks:
        default: development
        alfajores:
            verify: False
            update_interval: 60
        
    wallets:
        from_key0: ${PRIVATE_KEY_OWNER}
        from_key1: ${PRIVATE_KEY_ACC1}
        from_key2: ${PRIVATE_KEY_ACC2}

    pinata_keys:
        api_key: ${API_KEY}
        secret_api_key: ${SECRET_API_KEY}    

    dev_deployment_artifacts: true

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/brownie-config.yaml).


- Creating the deploy.py file
- Let begin with our imports, we import our `FundRaiser` contract from the Contractcontainer that will be created when the contract is complied, our accounts for interacting with the local chain, the network and the config file from brownie.
- Then we import `LinearScalingStrategy` to set the gas price for our deploy transaction and then import json.


```py
from brownie import FundRaiser, accounts, network, config
from brownie.network.gas.strategies import LinearScalingStrategy
import json

```

- Next we set the gas price for the transaction by instanciating `LinearScalingStrategy` class.

```py
gas_strategy = LinearScalingStrategy("10 gwei", "50 gwei", 1.1)

```

- In the deploy script we Create our `main()` function.
- looking up first if the network to be deployed on is alfajores and deploy the contract using the first key from our config file (i.e. the first exported key should be the owners account). 
- The next if block validates if we are to deploy on the development network i.e. ganache and deploy the contract with brownies pre-defined accounts.
    - whats happning here is we are adding our private key to brownies account to create an account that coulde be used on the testnet
    - and then deploying the contract with the `deploy` method of the `FundRaiser` Object.

```py

def main():
    if network.show_active()=='alfajores':
        adr = {}
        dev = accounts.add(config["wallets"]["from_key0"])
        print(network.show_active())
        deployed = FundRaiser.deploy({'from':dev, "gas_price":gas_strategy})
        adr["address"] = deployed.address
        with open('./build/deployments/deployAlfajores.json', 'w') as outfile:
            json.dump(adr, outfile, indent=4)              
        return deployed


    if network.show_active()=='development':
        adr = {}       
        owner = accounts[0]
        deployed = FundRaiser.deploy({'from':owner, "gas_price":gas_strategy})
        adr["address"] = deployed.address
        with open('./build/deployments/deployLocal.json', 'w') as outfile: 
            json.dump(adr, outfile, indent=4)   
        return deployed
  
```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/scripts/deploy.py).

// am here
##### 4.2.2.1 Next we deploy and test the contract on ganache local network 
- Open a new terminal for the ganache network and issue this command

```bash
ganache-cli
```
![ganache-1](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/ganache-1.png)

![ganache-2](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/ganache-2.png)

- Open a separate terminal and issue the commands below

```bash
brownie compile
```
```bash
brownie run deploy.py
```
- do copy your deployed contract address somewhere safe we would need it to get our deployed contract on the chain.
![deploy-local](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/deploy-local.png)

- We could now make calls and interact with our deployed contract. Access the console (brownie console is a lot similar to the python console) by issuing this command 

```bash
brownie console 
```


- You could get access to an instance of your deployed contract on ganache by interacting with the console.

```bash
funds = FundRaiser.at('contract_address')
```
![console-local](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/console-local-1.png)



- make some transactions 

```bash
funds.Donate( {'from': accounts[1], 'value':4000000000000000000, 'gas_price':100000000} )
```

```bash
funds.safeMint('my/new/token/uri', {'from': accounts[1], 'gas_price':100000000} )
```

```bash
funds._TotalDonations()
```
![donate-mint-local](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/donate-mint-local.png)


```bash
funds.NewPost("just deployed a test contract", "just depl...", {'from': accounts[1], 'gas_price':100000000})
```

```bash
funds.NewPost("Updated the contract for a better prefrence", "updated the.....", {'from': accounts[2], 'gas_price':100000000})
```

```bash
funds.ReturnPosts()
```
![newpost-posts-local](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/newpost-posts-local.png)

- Eth-brownie utilizes pytest and hypothesis for unit and property-based testing providing a robust framework for testing your contracts. Every test scripts created should be placed in the `./tests` directory and for naming conventions, test files are to be prefixed with test_ or suffixed with _test while being named. One of the reasons one would want to automate testing a Smart Contract is, instead of making several calls from the console to manual test a contract it will be preferable to automate the process by writing a script that would make several calls to the contract and making assertions to those calls, saving a lot of time and going a long way by using just a script. Brownie provides pytest Fixtures for easy testing and interacting with our project.   

- Create a test_OnGanache.py file in the `./tests` directory and populate it with the code below or you could create your own test. For our tests we will be using a module scoped fixture for deploying the contract, so the same deployed instance will be used on all test functions and applying a `fn_isolation` fixture to the our tests. Where `fn_isolation` takes a snapshot of the chain before running the test and reverts back after the test.

- Note This Isolations will only be applied to the test files that would be executed on ganache where we have that level of control. 

[More on brownie tests](https://eth-brownie.readthedocs.io/en/stable/tests-pytest-intro.html?highlight=tests#writing-unit-tests)

- These tests are some series of calls, transactions and assertions to make sure our contract responds as it should. 
- The Created functions tests the Crowdfund and Blogs methods in our smart contract.

```py

import pytest
from brownie import accounts, network
from brownie.network.gas.strategies import LinearScalingStrategy


gas_strategy =  LinearScalingStrategy("10 gwei", "50 gwei", 1.1)

@pytest.fixture(scope="module", autouse=True)
def Funds(FundRaiser):
    yield FundRaiser.deploy({'from': accounts[0], "gas_price":gas_strategy})

@pytest.fixture(autouse=True) 
def isolation(fn_isolation):
    pass

def test_nftfunds_Donate_functions(Funds):
    """
    Test Contract's Minting And Donation Methods.
    """
    print(network.show_active())
    assert Funds.owner() == accounts[0]
    Funds.Donate({'from':accounts[1], 'value':2000000000000000000, 'gas_price':gas_strategy})
    Funds.safeMint("new/nft/acc1", {'from': accounts[1], 'gas_price':gas_strategy})
    Funds.Donate({'from':accounts[2], 'value':4000000000000000000, 'gas_price':gas_strategy})
    Funds.safeMint("new/nft/acc2", {'from': accounts[2], 'gas_price':gas_strategy})
    assert Funds._donationtBalance() == 6000000000000000000
    assert Funds._TotalDonations() == 6000000000000000000
    Funds.TransferDonations(accounts[3],{'from':Funds.owner(), 'value':2400000000000000000, 'gas_price':gas_strategy})
    assert Funds._donationtBalance() == 3600000000000000000
    assert Funds._TotalDonations() == 6000000000000000000
    assert Funds.ownerOf(1) == accounts[1]
    assert Funds.ownerOf(2) == accounts[2]


def test_nftfunds_Blog_functions(Funds, accounts):
    """
    Test Blogs Post And Like Functions.
    """
    print(network.show_active())
    Funds.NewPost("You have a new Post", "You have...", {'from': accounts[1], 'gas_price':gas_strategy})
    Funds.NewPost("Another post from another accouunt", "Another post...", {'from': accounts[2], 'gas_price':gas_strategy})
    Funds.LikeandUnlikePost(0, {'from': accounts[2], 'gas_price':gas_strategy})
    Funds.LikeandUnlikePost(1, {'from': accounts[1], 'gas_price':gas_strategy})
    Posts = Funds.ReturnPosts()
    assert Posts[0][2] == "You have a new Post"
    assert Posts[0][1] == accounts[1]
    assert Posts[0][4] == 1
    assert Posts[1][2] == "Another post from another accouunt"
    assert Posts[1][1] == accounts[2]
    assert Posts[1][4] == 1
    P1 = Funds.ReturnLiked(0, {'from': accounts[2]})
    P2 = Funds.ReturnLiked(1, {'from': accounts[1]})
    assert P1 == True
    assert P2 == True
    Funds.LikeandUnlikePost(0, {'from': accounts[2], 'gas_price':gas_strategy})
    Funds.LikeandUnlikePost(1, {'from': accounts[1], 'gas_price':gas_strategy})
    P1 = Funds.ReturnLiked(0, {'from': accounts[2]})
    P2 = Funds.ReturnLiked(1, {'from': accounts[1]})
    assert P1 == False
    assert P2 == False
    Funds.DeletePost(0,  {'from': accounts[1], 'gas_price':gas_strategy})
    Posts = Funds.ReturnPosts()
    assert len(Posts) == 1

```
[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/tests/test_OnGanache.py).


- Lets run the test on ganache You should expect two passes at the end of the test. 

```bash
brownie test tests/test_OnGanache.py
```
![test-local](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/test-local.png)



##### 4.2.2.2 Next Deploy and test the contract on The Alfajores testnet

```bash
brownie run deploy.py --network alfajores
```
- do copy your deployed contract address we would need it to get our deployed contract on the chain.
![deploy-alfajores](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/deploy-alfajores.png)

- access the console.

```bash
brownie console --network alfajores
```
![console-alfajores](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/console-alfajores.png)

- You could get access to an instance of your deployed contract on alfajores by interacting with the console....

```bash
funds = FundRaiser.at('contract_address')
```

```bash
from brownie import config
acc1 = accounts.add(config["wallets"]["from_key1"])
acc2 = accounts.add(config["wallets"]["from_key2"])
```

- make some transactions 

```bash
funds.Donate( {'from': acc1, 'value':4000000000000000000, 'gas_price':10000000000} )
```

```bash
funds.safeMint('my/new/token/uri', {'from': acc1, 'gas_price':10000000000} )
```

```bash
funds._TotalDonations()
```
![donate-mint-alfajores](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/donate-mint-alfajores.png)


```bash
funds.NewPost("just deployed and test contract", "just depl...", {'from': acc2, 'gas_price':10000000000})
```

```bash
funds.NewPost("Updated the contract for a better prefrence", "updated the.....", {'from': acc1, 'gas_price':10000000000})
```

```bash
funds.ReturnPosts()
```
![newpost-posts-alfajores](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/newpost-posts-alfajores.png)

- Now Create a test_OnAlfajores.py file in the `./tests` directory and populate it with the code below or you could create your own test.

- These tests are a series of calls, transactions and assertions to make sure our contract responds as it should. 
- The Created functions tests the Crowdfund and Blogs methods in our smart contract.
- Our extra accounts come in handy here.

```py

import pytest
from brownie import accounts, network, config
from brownie.network.gas.strategies import LinearScalingStrategy


gas_strategy =  LinearScalingStrategy("10 gwei", "50 gwei", 1.1)

metamaskAccounts = [accounts.add(config["wallets"]["from_key0"]), accounts.add(config["wallets"]["from_key1"]), accounts.add(config["wallets"]["from_key2"])] 

@pytest.fixture(scope="module", autouse=True)
def Funds(FundRaiser):
    yield FundRaiser.deploy({'from': metamaskAccounts[0], "gas_price":gas_strategy})


def test_nftfunds_Donate_functions(Funds):
    """
    Test Minting And Donation Functions.
    """
    print(network.show_active())
    assert Funds.owner() == metamaskAccounts[0]
    Funds.Donate({'from':metamaskAccounts[1], 'value':2000000000000000000, 'gas_price':gas_strategy})
    Funds.safeMint("new/nft/acc1", {'from': metamaskAccounts[1], 'gas_price':gas_strategy})
    Funds.Donate({'from':metamaskAccounts[2], 'value':2000000000000000000, 'gas_price':gas_strategy})
    Funds.safeMint("new/nft/acc2", {'from': metamaskAccounts[2], 'gas_price':gas_strategy})
    assert Funds._donationtBalance({'from': metamaskAccounts[0]}) == 4000000000000000000
    assert Funds._TotalDonations() == 4000000000000000000
    Funds.TransferDonations(metamaskAccounts[2],{'from':metamaskAccounts[0], 'value':2400000000000000000, 'gas_price':gas_strategy})
    assert Funds._donationtBalance({'from': metamaskAccounts[0]}) == 1600000000000000000
    assert Funds._TotalDonations() == 4000000000000000000
    assert Funds.ownerOf(1) == metamaskAccounts[1]
    assert Funds.ownerOf(2) == metamaskAccounts[2]


def test_nftfunds_Blog_functions(Funds):
    """
    Test Blogs Post And Like Functions.
    """
   
    print(network.show_active())
    Funds.NewPost("You have a new Post", "You have...", {'from': metamaskAccounts[1], 'gas_price':gas_strategy})
    Funds.NewPost("Another post from another accouunt", "Another post...", {'from': metamaskAccounts[2], 'gas_price':gas_strategy})
    Funds.LikeandUnlikePost(0, {'from': metamaskAccounts[2], 'gas_price':gas_strategy})
    Funds.LikeandUnlikePost(1, {'from': metamaskAccounts[1], 'gas_price':gas_strategy})
    Posts = Funds.ReturnPosts()
    assert Posts[0][2] == "You have a new Post"
    assert Posts[0][1] == metamaskAccounts[1]
    assert Posts[0][4] == 1
    assert Posts[1][2] == "Another post from another accouunt"
    assert Posts[1][1] == metamaskAccounts[2]
    assert Posts[1][4] == 1
    P1 = Funds.ReturnLiked(0, {'from': metamaskAccounts[2]})
    P2 = Funds.ReturnLiked(1, {'from': metamaskAccounts[1]})
    assert P1 == True
    assert P2 == True
    Funds.LikeandUnlikePost(0, {'from': metamaskAccounts[2], 'gas_price':gas_strategy})
    Funds.LikeandUnlikePost(1, {'from': metamaskAccounts[1], 'gas_price':gas_strategy})
    P1 = Funds.ReturnLiked(0, {'from': metamaskAccounts[2]})
    P2 = Funds.ReturnLiked(1, {'from': metamaskAccounts[1]})
    assert P1 == False
    assert P2 == False
    Funds.DeletePost(0,  {'from': metamaskAccounts[1], 'gas_price':gas_strategy})
    Posts = Funds.ReturnPosts()
    assert len(Posts) == 1

```

[Link to code block](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/tests/test_OnAlfajores.py).

- Lets run the test on the alfajores testnet You should expect two passes at the end of the test.

```bash
brownie test tests/test_OnAlfajores.py --network alfajores
```
![test-alfajores](https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/test-alfajores.png)


### 4.3 Generating Unique Images Using An Art Engine..

- This part of the tutorial involves generating unique images that will be assigned to awarded tokens for our donor. These images are to represent an identifyer or an appreciation for donations or a reference for participation in the crowdfund Project. The complete Dapp to this project built with react.Js could quickly express that idea.[link to Dapp here](https://crowdfund-dapp-seven.vercel.app/) to get a complete idea of the project.

- We explained earlier a little on generative art. I cloned from the original [nft-generator-py repo](https://github.com/Jon-Becker/nft-generator-py/blob/main/)(Art engine) and made a some modification to the generator script and some files, then created a repo for this tutorials purpose. 
- Here we will be getting into the config and directories to the art engine for better experience on what we will be doing. We installed our art engine earlier let’s get into how it works just in case you didn’t go through the README.md for the art engine.

- Having a look at the directories.  
- `./images` and `./metadata` will be were our images and metadata go into after the are generated. 
- `./trait-layers` with sub-directories `./backgrounds` for the background images  `./foreground` for the foreground images `./text` for our text images.

- The images used where rarely edited i didn’t get to do any Photo Shoping. Just examples for this tutorial. The idea is for you to understand how it works and get to come up with your own idea or you could just use and improve on mine. 

- Take Note.
- All images should have dimensions of `1000x1000` and must be in `.png` format.

- The config file is an Object with `layers` where unique images and metadata are generated from by selecting images from each layer in the config, each layer having key-pair values and the chances an image is selected in a layer is based on the `weights`. 
- The `incompatibilities` is where images in layers that are incompatible due to color or other reasons are defined.
- The `name` is the default prefix for each image or metadata name and `description` describes the whole batch generated.
- Use the README.md for more info because of time on this tutorial. 

- The config file.
```json
{
  "layers": [
    {
      "name": "Background",
      "values": ["Blue", "Green", "Purple Mix", "Fade Away", "Neon Mix", "Pattern", "Gradient", "Stacked Wall", "Mixture", "Leaves"],
      "trait_path": "./trait-layers/backgrounds",
      "filename": ["Blue", "Green", "Purple Mix", "Fade Away", "Neon Mix", "Pattern", "Gradient", "Stacked Wall", "Mixture", "Leaves"],
      "weights": [10,10,10,10,10,10,10,10,10,10]
    },
    {
      "name": "Foreground",
      "values": ["Award-One", "Award-Two", "Award-Three", "Award-Four", "Award-Five", "Award-Six", "Award-Seven", "Award-Eight", "Award-Nine", "Award-Ten"],
      "trait_path": "./trait-layers/foreground",
      "filename": ["Awd-one", "Awd-two", "Awd-three", "Awd-four", "Awd-five", "Awd-six", "Awd-seven", "Awd-eight", "Awd-nine", "Awd-ten"],
      "weights": [10,10,10,10,10,10,10,10,10,10]
    },
    {
      "name": "Fundtext",
      "values": ["Fund Raiser"],
      "trait_path": "./trait-layers/text",
      "filename": ["donation"],
      "weights": [100]
    }
  ],
  "incompatibilities": [
    {
      "layer": "Background",
      "value": "Leaves",
      "incompatible_with": ["Award-Five"],
      "default": {
        "value": "Default Incompatibility",
        "filename": "./trait-layers/foreground/Awd-five"
      }
    }
  ],
  "name": "NFT_",
  "description": "Project Fund Raiser."
}

```

- Having updated our images and config file to our preferences lets generate our images.
   Where:
   1. `AMOUNT` is the amount of images to generate
   2. `CONFIG` is the path pointing to a `.json` file containing valid program configuration.

```bash
cd nft-generator-py python3 generate.py --amount AMOUNT --config CONFIG
```

- Having generated your images create a `./nft` directory in your tutorial project directory, then also create these subdirectories in `./nft` directory. `./images`, `./metadata`, `./awardlocal` and `./awardalfajores`.
    where:
    - `./images`: will be where we copy our generated images to.
    - `./metadata`:  will be where we copy our generated metadata to.
    - `./awardlocal`: where a copy of our minted token metadata goes into when interacting with ganache.
    - `./awardalfajores`: where a copy of our minted token metadata goes into when interacting with alfajores.

- [more on generative art here](https://www.udemy.com/course/free-art-blockchain/).   

- Having done all that, there are three scripts Created to assist with interacting with your contract on the both alfajores and ganache and the third a utility script. Much won’t be explained on these script because i believe we understand python at an intermediate level and won’t want to exhaust our time. Our extra wallet accounts come in handy here too.

- These scripts requires api keys from piñata ipfs for storing images and metadata so before you run the scripts be sure to head over to [Pinata Ipfs](https://app.pinata.cloud/). Sign up with piñata, get a secret key and an api key instructions on that are found in the doc's [Authentication](https://docs.pinata.cloud/pinata-api/authentication), and update this two keys in your .env file with the generated key's.

```.env
export API_KEY= your api key
export SECRET_API_KEY= your api secret key
```
- Then visit the Tutorials project repo [here](https://github.com/lukrycyfa/crowdfund-tutorial-project) and download or copy these three files in the ./script directory `useFundsAlfajores.py`, `useFundsLocal.py` and `utility.py` and make copy's in the scripts directory of your project.

    - [Alfajores script](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/scripts/useFundsAlfajores.py).
    - [Ganache script](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/scripts/useFundsLocal.py).
    - [Utility script](https://github.com/lukrycyfa/crowdfund-tutorial-project/blob/main/scripts/utility.py).

- What’s happing in our scripts is there are three created functions to make calls to related functionalities in our crowdfund contract, in each script that interacts with their respective networks and the utility script carries functions that sends data to the IPFS and collect inputs from the terminal. All you have to do is to call the script alongside a function e.g.

- For donations and minting on alfajores
```bash
brownie run --network alfajores useFundsAlfajores.py donate_mint
```
- After making donations and minting you should be able to see your metadata and image on your ipfs dashboard.

- For Posting to the Blog...
```bash
brownie run --network alfajores useFundsAlfajores.py returnPosts_Pst
```
- For Likes...
```bash
brownie run --network alfajores useFundsAlfajores.py like_unlikePst
```
<iframe className="mx-auto" width="100%" height="515"  src="https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/alfajores-script-mp4.mp4" title="Testing Interactive Script On Alfajores" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


- For donations and minting on ganache
```bash
brownie run  useFundsLocal.py donate_mint
```
- For Posting to the Blog...
```bash
brownie run  useFundsLocal.py returnPosts_Pst
```
- For Likes...
```bash
brownie run  useFundsLocal.py like_unlikePst
```
<iframe className="mx-auto" width="100%" height="515"  src="https://github.com/lukrycyfa/crowdfund-tutorial-main/blob/main/Media/local-script-mp4.mp4" title="Testing Interactive Script On Ganache" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- !and here we have it you could now develop, test and deploy a smart contract on alfajores using eth-brownie. 

## 5.0 FAQ....
- Ipfs: The InterPlanetary File System (IPFS) is a protocol, hypermedia and file sharing peer-to-peer network for storing and sharing data in a distributed file system. IPFS uses content-addressing to uniquely identify each file in a global namespace connecting IPFS hosts. IPFS can among others replace the location based hypermedia server protocols http and https to distribute the World Wide Web. [wikipedia](https://en.wikipedia.org/wiki/InterPlanetary_File_System).

- Nft Erc721 token standard: A Non-Fungible Token (NFT) is used to identify something or someone in a unique way. This type of Token is perfect to be used on platforms that offer collectible items, access keys, lottery tickets, numbered seats for concerts and sports matches, etc. This special type of Token has amazing possibilities so it deserves a proper Standard, the ERC-721 came to solve that

## 6.0 Conclution
- From this tutorial we have gained some reasonable amount of experience using One of Celo Blockchain Technology's (alfajores testnet) and Eth-brownie to develop test and deploy a crowdfund smart contract with extra features and got to generate unique images to associate with token's using a generative art engine written in python and gained other valuable insight's about Smart contract's and other Technologies. After completing this tutorial you should be encouraged to create your own unique smart contract's or improve on the existing contract and explore more on Celo Blockchain Technologies and Eth-brownie. Congrats on completing this tutorial 🥳.