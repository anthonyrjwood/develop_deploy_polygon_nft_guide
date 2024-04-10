![Image of Kadonks Logo](https://soulagain.crypto-elites.club/yg/1.png)

# NFT - on Polygon - Development Guide 
A complete guide to deploying an NFT collection on Polygon and hosting a minting engine. This guide will walk through the necessary steps of how to develop an NFT collection structure, compiling the images and smart contract deployment, through to hosting a minting engine. 

# Art Structure
Step 1
-----
Utilize fixed guide lines within the artboard - fixed proportionality will allow attributes to be changed later on, but retain perfect alignment to former attributes.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/2.jpg"></p>
Create a guide layer for each individual attribute, so that each attribute's guide layer can be toggled on and off; the more complex the art, the more attribute divisions - too many guide layers viewed at once can be confusing!<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/3.jpg"></p>
Ensure that background layers are stacked at the bottom layers, so they, too, can be toggled on and off to ensure future attribute's compatibility.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/4.jpg"></p>
Each iteration of the NFT character should contain (vertically stacked) subdivisions of attributes. <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/5.jpg"></p>
Each subsequent iteration of the character can be initialized from duplicating the layer. That way, the underlying frame and positioning can be carried forward. The characters will stack vertically for toggling against former attributes. <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/6.jpg"></p>
How the scructure appears at completion:<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/7.jpg"></p>

# Compiling NFTs
Step 2
-----
`Download Visual Studio Code`<br>
`Download and Install node.js https://nodejs.org/en/download/`<br>
`Download the Hash Lips art engine https://github.com/anthonyrjwood/hashlips_art_engine.git`<br>
`Within VSC, install "npm script runner" and restart application [ctrl + p + npm script runner]`<br>
`Open Hash Lips repo inside VSC`<br>
`Open a new VSC terminal`<br>
`In the terminal, type: npm i canvas`<br><br>
At this point, the NFT art needs to now be added to the Hash Lips repo directory (/layers). The attribute file name at export needs to include both a unique title and how often this particular attribute will occur within the NFT collection. For example:
`Dark Blue#50`
The total number of NFTs for this example collection is 100, so the "Dark Blue#50" attribute will occur 50/100 times.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/8.jpg"></p>
Ensure to organize the attributes into their constituent categories.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/9.jpg"></p>
Within hashlips/config.js, organize the layersOrder property attribute stack in the same way it was stacked when created; the image compiler stacks in this order, so it's important that this stacking reflects the original art stacking. Furthermore, the growEditionSizeTo property represents the size of the NFT collection. For the purposes of demonstration, this will be a 100 NFT collection. <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/10.jpg"></p>
Next, populate the remainder of the config.js to your own requirements. When the document is configured, type `node index.js` in the terminal console and the images will begin compiling.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/11.jpg"></p>

# Host NFTs on IPFS
Step 3
-----
In order to upload the NFT collection to IPFS, we need to use Pinata interface.<br>
`Open an account on Pinata https://app.pinata.cloud/ `<br>
Once opened, go ahead and upload your NFT collection from `hashlips/build/images`<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/12.jpg"></p>

Updating Metadata
-----
We need to now return to VSC and populate the config.js with the correct URI CID. After uploading the NFTs via Pinata, the folder itself will now have a CID code, which is the unique ID of the content stored on IPFS. Using this code, you can now update the `baseUri` variable in the config.js: `ipfs://<yourCID>`<br><br><p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/13.jpg"></p>
Next, we will run `node utils/update_info.js` in the terminal to update the metadata of the NFTs.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/14.jpg"></p>
Once completed, we'll upload the meta data to Pinata. Simply upload the `hashlips/build/json` folder to Pinata as we did with the NFT folder.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/15.jpg"></p>

# Deploying Polygon Smart contract
Step 4
-----
Firstly, we will download and populate an existing smart contract.<br>
`git clone https://github.com/anthonyrjwood/nft-contract`<br><br>
Once downloaded, head over to `https://remix.ethereum.org/` and upload the smart contract. Make sure that the directory format is the same and also update the name of the Solidity file and populate areas with the new name. Also, remove some files from the directory; please see screenshot and emulate the directory setup.<br><br> 
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/19.jpg"></p>
Once everything has been populated, compile the contract.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/20.jpg"></p>
Once compiled, head to deploy. Switch environment to `injected web3` and connect your Metamask account.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/21.jpg"></p>
A Polygon (MATIC) faucet can be claimed from `https://faucet.polygon.technology/` to fund the deployment.<br>

Add MATIC to Metamask
-----

`Network Name: Matic Mainnet`<br>
`New RPC URL: https://rpc-mainnet.maticvigil.com/`<br>
`ChainID: 137`<br>
`Symbol: MATIC`<br>
`Block Explorer URL: https://explorer.matic.network/`<br><br>

**Note** Ensure that Polygon (MATIC) is sent to the Polygon network and not ETH. If that is the case, use the Polygon bridge to swap it over. 

Deployment
-----
Prior to deployment, decide whether or not you'd like to pre-mint some of the NFTs (great for testing out marketplaces like opensea, etc). If yes, then this can be configured in the primary `.sol` file. <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/28.jpg"></p>
Populate the form as such, including the .json CID from Pinata within `_INITBASEURI:` field. Be sure to add a `/` at the URI ending. <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/22.jpg"></p>
Once populated, make sure Metamask is on Polygon (MATIC) mainnet and then click `transact`.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/23.jpg"></p>
Additionally, switch the network fee to `Gwei`.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/24.jpg"></p>
When the smart contract has been deployed, the interface will produce the address.<br><br> 
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/25.jpg"></p>
Verify that the smart contract has been successfully deployed by viewing the chain at `https://polygonscan.com`.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/26.jpg"></p>
Next, you can mint 1 single NFT from within the Remix interface. Click the deployed contract's drop down menu. Within the mint section, populate the field with your own address and quantity. And then `transact`.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/27.jpg"></p>
Once minted to your address, you can then login to `https://opensea.io` and be able to view the NFT on your account! i.e. `https://opensea.io/collection/yellow-guy-dummy-pack`. If you decide to pre-mint a whole bunch, make sure to turn these into a collection on the opensea marketplace.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/29.jpg"></p>

# Hosting Mint Engine for NFT collection
Step 5
-----
Now it's time to setup the minting engine, so that users can mint an NFT (selected at random!) from the collection. Make sure to fork the GitHub repo first, so that you can push back to the repo when it's modified. <br><br>
When forked, clone a copy locally:<br>
`git clone https://github.com/anthonyrjwood/nft-minting-app`<br>
Firstly, within `public > config >abi.json` we need to paste over the ABI from the `remix.ethereum.org` interface we previously used to deploy the smart contract.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/30.jpg"></p>
Simply click the `ABI` copy symbol. Then in the minting-app repo `public > config > abi.json`, select all and delete. And then paste in what was copied and save.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/31.jpg"></p>
Next, populate the `public > config > config.json` file<br>
In order to calculate the correct Wei cost, you can use `https://eth-converter.com/` to achieve the correct value. I.e. 0.05 ETH into Wei formatting.<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/32.jpg"></p>
Once that's completed, then work through the files and update all the images and labeling according to your own needs.<br>
Next, installing the dependencies required for the code to run. Open a new terminal in VSC:<br>
`npm install` <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/33.jpg"></p>
To run the site locally, then type: <br>
`npm run start`<br>


Hosting Minting App via Netlify
-----
Create an account with: `https://app.netlify.com/`, a platform that will broadcast your website directly from the GitHub repo, run the necessary dependencies. This means that the minting app can be modified directly through the repo, and updating data on the website host won't be needed.<br>
Make sure to create the account via their GitHub option.<br>
Give Netlfy consent to control the fork of the minting app.<br>
Configure the site settings as such:<br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/34.jpg"></p>
Once completed, simple link your web host with Netlify! https://nft.bit-flowers.com <br><br>
<p align="center" width="100%"><img src="https://soulagain.crypto-elites.club/yg/35.jpg"></p>




























