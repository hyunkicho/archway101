# archway101
archway101

Hello everyone, following the last video, this time we will practice issuing, sending, and checking NFTs through archway. For archway, we provide separate CLI commands so that you can easily deploy NFTs on Cosmos Chain, and I think it will be very helpful for those who are learning for the first time. This lecture is not financial advice, it's just a lecture to help you start developing on archway chain technically.


This lecture is based on Archway's main documentation, so if you want to do more hands-on exercises, we recommend that you go to the official Archway documentation in the comments.


So let's get started with the lesson.


# Setup

## Prerequisite
https://docs.archway.io/developers/getting-started/install

First, you'll need to visit the sites below to download the necessary programs.


- Installation
To get started developing on the Archway Network, you will need to have the the following dependencies installed.

- Dependencies
  - Required
  - Rustc
  - Cargo
  - Cargo Generate
  - Node.js and NPM
  - Archway Developer CLI
  - Docker
- Optional
  - Archwayd

https://www.rust-lang.org/tools/install


Rustc
rustc, provided by the Rust project maintainers, is the compiler for the Rust programming language. rustc takes your Rust source code and produces binary code as a library or an executable.
To install Rust, follow the instructions for your operating system here.
https://www.rust-lang.org/tools/install

- install rust with rustup
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Cargo is the Rust package manager, like go get is for Golang or npm is for JavaScript. Cargo comes with Rust if you installed rustc using rustup.
If you did not already install rustc with rustup, or don't have cargo in your command line path, see the instructions for installing Cargo here.
https://doc.rust-lang.org/cargo/getting-started/installation.html

- install rust with cargo
```
curl https://sh.rustup.rs -sSf | sh
```
- cargo generate
```
cargo install cargo-generate --features vendored-openssl
cargo install cargo-run-script
```

## Setting up IDE for cosmwasm

I will recomment you 2 visual code extenstion for developing in cosmwasm.

- Rust-analyzer
The rust-analyzer extension is a language server for the Rust programming language, which provides features such as code completion, error checking, and documentation while writing Rust code in VS Code.
Follow these steps to install the extension:
Go to the Extension panel
In the Search field enter rust-analyzer
Click the install button to the bottom right of rust-analyzer

- CodeLLDB
The CodeLLDB extension is a native debugger used for debugging Rust and other compiled languages.
Follow these steps to install the extension:
Go to the Extension panel
In the Search field enter CodeLLDB
Click the install button to the bottom right of CodeLLDB

https://docs.archway.io/developers/getting-started/ide-setup


## install archway developer CLI
https://docs.archway.io/developers/getting-started/install
```
npm install -g @archwayhq/cli
```

## install Docker

Docker
Docker is required for the Archway Developer CLI to use the rust optimizer. You can use Docker Desktop or Docker Engine.
I will use Docker Desktop in this video
https://docs.docker.com/get-docker/


## wallet cli
from now on we will start developing in archway with archway cli 
there are plenty of functions in arcway Developer CLI wich we had installed.

you can also check cli commands in this link
https://www.npmjs.com/package/@archwayhq/cli/v/2.0.2

If you want to use existing account you could use this command
- use existing account
```
archway accounts new deployer --recover
```

but we will make new account in this video

- make new account
```
archway accounts -h
archway accounts new
//struggle alert sunny joke during side reopen silly soul collect yard crouch rookie version know casual divorce jewel onion found proud write foot pioneer
```

now you have made an accounts.
Let's checkout account list.
```
archway accounts list

Name: arch
Address: archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz
```

## getting testnet token

In order to make transactions in archway you need testnet token.
there are archway test token faucet in below link.
what you need is just discord id.
if you don't have one you could make it with your email.
lot of crpyto projects use discrod so I reccomend you to make one if u don't have it.

https://docs.archway.io/developers/guides/faucet


join discord server and type like below.
you should get testnet token to test in the accounts you typed in this command.

```
!faucet archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p
```

## checking cli commands with help
So now we are ready. lets checkout what we could do with archway developer CLI.

If you need guide you could see this with --help

```
archway --help
@archwayhq/cli/2.1.0 darwin-arm64 node-v18.18.1

Description:
  Develop WASM smart contracts with the Archway Network's Developer CLI

Usage:
  $ archway [COMMAND]

Available commands:
  new                      Initializes a new project repository
  autocomplete             display autocomplete installation instructions
  help                     Display help for archway.
accounts
  accounts new             Adds a new wallet to the keyring
  accounts get             Displays details about an account
  accounts list            Lists all accounts in the keyring
  accounts remove          Removes an account from the keyring
  accounts balances get    Query the balance of an address or account
  accounts balances send   Send tokens from one address or account to another
  accounts export          Exports an account's private key from the keyring
config
  config init              Initializes a config file for the current project
  config show              Displays the config values for the current project
  config deployments       Displays the list of deployments, allows filtering by chain, action and contract
  config chains use        Switches the current chain in use and updates the config file appropriately
  config chains import     Import a chain registry file and save it to the global configuration
  config chains list       Lists all available chains to use
  config get               Query config settings in the local or global config files
  config set               Update config settings in the local or global config files
contracts
  contracts new            Scaffolds a new Wasm smart contract from a template
  contracts build          Builds the smart contracts optimized Wasm file along with its schemas
  contracts store          Stores a Wasm file on-chain
  contracts instantiate    Instantiates code stored on-chain with the given arguments
  contracts metadata       Sets a smart contracts rewards metadata
  contracts premium        Sets the smart contract's premium flat fee. The contract must have the rewards metadata already configured
  contracts execute        Executes a transaction in a smart contract
  contracts migrate        Runs a smart contract migration
  contracts query balance  Access the bank module to query the balance of smart contracts
  contracts query smart    Queries a single smart contract
rewards
  rewards query            Queries the outstanding rewards for a specific account or address
  rewards withdraw         Withdraws rewards for a specific account
```

# Nft project guide
So what we will do today is make our own nft in archway testnet
You could also see the guide below. cause we are following this guide.
I reccomend you to look around officail guide line cause there are plenty of good education resources and examples.

https://docs.archway.io/developers/guides/nft-project/start

## STEP01. Build and optimize contracts
step 1 is to build and opitmize contracts.
you should select a chain and project name here.
In this video I will make project name as basic-nft.
Also you could use your own projcet name in here.

```
$ archway new basic-nft✔ Select a chain to use › Archway Testnet
✔ Choose a name for your contract … basic-nft✔ Choose a starter template 
› CW721 with on-chain metadataCreating Archway project basic-nft...🔧   
Destination: /Users/testuser/basic-nft ...🔧   
project-name: basic-nft ...🔧   
Generating template ...[ 1/19]   
Done: .cargo/                                                                                                           🔧   Moving generated files into: `/Users/testuser/basic-nft`...💡   
Initializing a fresh Git repository✨   
Done! New project created /Users/testuser/basic-nft
```

## STEP02. Designing tokens
Step 2 is desinging tokens.
The asset metadata is a critical element for any NFT. It defines information like the name, image URL, and other properties that can be pulled by NFT marketplaces to show relevant information to the users. Information like rarity, custom traits, etc., are all stored here.
In this example, we will keep our metadata on-chain. In other words, the contract will store the metadata in its internal state.
In the cw721-base code, NFT metadata is contained in the extension property of the TokenInfo struct:
https://github.com/public-awesome/cw-nfts/blob/v0.9.3/contracts/cw721-base/src/state.rs#L91-L105

```
#[derive(Serialize, Deserialize, Clone, Debug, PartialEq, JsonSchema)]
pub struct TokenInfo<T> {
    /// The owner of the newly minted NFT
    pub owner: Addr,
    /// Approvals are stored here, as we clear them all upon transfer and cannot accumulate much
    pub approvals: Vec<Approval>,

    /// Universal resource identifier for this NFT
    /// Should point to a JSON file that conforms to the ERC721
    /// Metadata JSON Schema
    pub token_uri: Option<String>,

    /// You can add any custom metadata here when you extend cw721-base
    pub extension: T,
}
```

To use this extension property, here's how we define our metadata in the CW721 with on-chain metadata template we cloned into our project.

```
#[derive(Serialize, Deserialize, Clone, PartialEq, JsonSchema, Debug, Default)]
pub struct Trait {
    pub display_type: Option<String>,
    pub trait_type: String,
    pub value: String,
}
#[derive(Serialize, Deserialize, Clone, PartialEq, JsonSchema, Debug, Default)]
pub struct Metadata {
    pub image: Option<String>,
    pub image_data: Option<String>,
    pub external_url: Option<String>,
    pub description: Option<String>,
    pub name: Option<String>,
    pub attributes: Option<Vec<Trait>>,
    pub background_color: Option<String>,
    pub animation_url: Option<String>,
    pub youtube_url: Option<String>,
}
```
https://github.com/archway-network/archway-templates/blob/main/cw721/on-chain-metadata/src/lib.rs#L9-L30

## STEP03. Designing tokens
 run docker desktop

you need to install docker to build contracts
https://docs.docker.com/desktop/install/mac-install/

## STEP04. Deploy the token Contract
- Generate an optimized build

First we will need to produce an optimized wasm build and upload it to the blockchain.
Optimized builds are produced by executing the archway contracts build command:

```
archway contracts build
```
you should make basic settings here. make sure you turn on the docker before using this
if you passed this process Schemas generated will appear in your cli

```
Building optimized wasm file for all contracts in the workspace using Docker...
✔ Pulling docker image cosmwasm/workspace-optimizer:0.14.0...
1.71.0-x86_64-unknown-linux-musl (default)
cargo 1.71.0 (cfd3bbd8f 2023-06-08)
Building artifacts in workspace...
Found workspace member entries: ["contracts/*"]
Package directories: ["contracts/testnft"]
Contracts to be built: ["contracts/testnft"]
Building "contracts/testnft" ...
.
.
.
✅ Schemas generated
```

- Store the optimized build on chain

To store the optimized build on Archway using the Archway CLI, you would use the following command:

```
✔ Enter the name or address of the account that will send the transaction … arch
Uploading optimized wasm for contract testnft
  Chain: constantine-3
  Signer: arch

✅ Contract testnft.wasm uploaded
  Code Id: 3186
  Transaction: 504433E1F8CD80000D5C9A39E3A4949EAF4A30141136014659A822F2AB084821
```

- Instantiate the NFT collection

Now we are ready to instantiate the contract. The contract instantiation requires three parameters:
name (the NFT collection name)
symbol (a token symbol to represent the collection)
minter (the wallet address allowed to mint a new NFT using this contract)
When we run the archway instantiate command, we add our values for name, symbol and minter as arguments.

basic scripts
```
archway contracts instantiate basic-nft --args '{ "name": "Test Collection", "symbol": "NFTEST", "minter": "archway1f395p0gg67mmfd5zcqvpnp9cxnu0hg6r9hfczq" }'
```

make your own scripts

1. find yout address from command below
```
archway accounts list

Name: arch
Address: archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz

Name: test
Address: archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p
```

2. set name, symbol, minter as an aurguments
```
archway contracts instantiate testnft --args '{ "name": "All about Archway", "symbol": "AAA", "minter": "archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz" }'
```

3. enter the name of the address at following command and give password of your os
```
✔ Enter the name or address of the account that will send the transaction … arch
Instantiating contract testnft
  Chain: constantine-3
  Code: 3186
  Label: testnft-0.1.0
  Admin: archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz
  Signer: arch

✅ Contract testnft-0.1.0 instantiated
  Address: archway1tf629qemlglefs2g8c2hurds8xrwt3wp728ehmts3cv6jaz4xjdqdvn2lg
  Transaction: 6970F74960835F192D964102A51DF125914083D3415F67AD9C7683AA914539DF
```

4. Configure the deployed contract
Now that the NFT contract is deployed it's recommended to set its metadata. This will configure the smart contract to collect developer premiums, rewards and can be used to enable gas rebates with a pooling account.

- Reward distribution : After the rewards are calculated, they are stored as reward records. These records establish claims that contracts can convert into ARCH tokens. To claim these rewards, a withdrawal operation must be executed. When a withdrawal is initiated, the tokens are transferred to the reward_address designated by the contract's owner.

So you should set rewards-address when you try to deploy contracts

basic example
```
archway contracts metadata basic-nft --owner-address "archway12qj4v8jg5pxk6gsqct09sf9szhwql69xmf9fh4"  --rewards-address="archway12qj4v8jg5pxk6gsqct09sf9szhwql69xmf9fh4"
```

your own exmaple
```
archway contracts metadata testnft --owner-address "archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz"  --rewards-address="archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p"
```

result
```
✔ Enter the name or address of the account that will send the transaction … arch
Setting metadata for contract testnft
  Chain: constantine-3
  Contract: archway1tf629qemlglefs2g8c2hurds8xrwt3wp728ehmts3cv6jaz4xjdqdvn2lg
  Rewards: archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p
  Owner: archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz
  Signer: arch

✅ Metadata for the contract testnft-0.1.0 updated
  Transaction: EB33F4C89ECE0F73EC3A1C06B689FF052A5B7800CA6EB3D78FED1691744EAC24
```

5. set contract premiums
To set a contract premium the contract must have the rewards metadata already configured. 
You can see Rewards information here : https://docs.archway.io/overview/rewards

There are 3 types of rewards
Gas rebates, Dev inflation tokens, Contract Premiums

- Gas rebates : 50% of this transaction fee is distributed to the dapp on which the gas was spent, while the other 50% is permanently removed from circulation ("burnt").

- Dev inflation tokens : Upon Mainnet launch, 25% of the DIT rewards will be allocated to developers, with the remaining 75% designated for validators and delegators. Thus, if the network experiences a total inflation of 8%, then 2% will be distributed to developers, and 6% will be awarded to validators and delegators.

- Contract Premiums : Archway enables dapp developers to define a custom flat fee for interacting with their smart contracts. These fees grant developers a versatile alternative to monetize their contracts. For the user’s experience, the Contract Premium will be paid alongside the gas fee.


basic example
```
archway contracts premium increment2 --premium-fee "1000000000000000000aconst" --from "mywallet" 
```

your own exmample
```
archway contracts premium testnft --premium-fee "1000000000000000000aconst" --from "arch" 
```

result

```
Setting premium for contract testnft
  Chain: constantine-3
  Contract: archway1tf629qemlglefs2g8c2hurds8xrwt3wp728ehmts3cv6jaz4xjdqdvn2lg
  Premium: 1 CONST (1000000000000000000aconst)
  Signer: arch

✅ Premium for the contract testnft-0.1.0 updated
  Transaction: 269372B5F02E8561B37C2AB99E748A9CCF4DA744F9DF773DF68CD262525BA0D8
```

## STEP05. Minting and sending tokens

Now that we've got our smart contract deployed we can mint tokens that can be sent to other Archway addresses.

1. minting tokens

MintMsg is a message type from the cw721_base package imported by our project's Cargo.toml. It's used by our contract's execution handler to set state for an NFT with metadata corresponding to the TokenInfo model we looked at previously.
To mint an NFT, we need to send a transaction to the smart contract with our MintMsg parameters in JSON format. For adding custom traits, we can use the on-chain metadata NFT template and include arbitrary metadata values using the extensions attribute of MintMsg.

This is the JSON string we will use to mint our test NFT:
```
{
  "mint": {
    "token_id": "1",
    "owner": "archway1f395p0gg67mmfd5zcqvpnp9cxnu0hg6r9hfczq",
    "extension": {
      "name": "Archway NFT #1",
      "description": "Building With NFTs",
      "image": "ipfs://QmZdPdZzZum2jQ7jg1ekfeE3LSz1avAaa42G6mfimw9TEn",
      "attributes": [
        {
          "trait_type": "tutorial",
          "value": "https://docs.archway.io/developers/guides/nft-project/start"
        }
      ]
    }
  }
}
```
To execute our mint transaction we add the JSON arguments using the --args flag of tx command of the Archway Developer CLI.

```
archway contracts execute basic-nft --args '{"mint":
{
    "token_id":"1",
    "owner":"archway1f395p0gg67mmfd5zcqvpnp9cxnu0hg6r9hfczq",
    "extension":{"name":"Archway NFT #1",
    "description":"Building With NFTs",
    "image":"ipfs://QmZdPdZzZum2jQ7jg1ekfeE3LSz1avAaa42G6mfimw9TEn",
    "attributes":
    [
        {
            "trait_type":"tutorial",
            "value":"https://docs.archway.io/developers/guides/nft-project/start"
        }
    ]
}}}'
```

making yout own metadata
```
archway contracts execute testnft --args '{"mint":
{
    "token_id":"1",
    "owner":"archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz",
    "extension":{"name":"All about Archway NFT #1",
    "description":"All about Arcway making NFT guide",
    "image":"ipfs://QmZdPdZzZum2jQ7jg1ekfeE3LSz1avAaa42G6mfimw9TEn",
    "attributes":
    [
        {
            "trait_type":"tutorial",
            "value":"https://docs.archway.io/developers/guides/nft-project/start"
        }
    ]
}}}'
```
result
```
✔ Enter the name or address of the account that will send the transaction … arch
Executing contract testnft
  Chain: constantine-3
  Signer: arch

✅ Executed contract  testnft-0.1.0
  Transaction: 6975A259529D9A3077BB3425F6FE4B5CBAAAAD0D8180010F7F1B2CC7EDD66EE0
```

To confirm the NFT is now correctly stored on-chain, run the query command, specifying the token_id declared in the minting transaction:

```
archway contracts query smart basic-nft --args '{"nft_info":{"token_id":"1"}}'
# Show output here
```

## STEP06. Sending Tokens
To transfer a token, we have to send a message of the type TransferNft, which we achieve by sending a transaction to the transfer_nft entrypoint exposed by the contract. The params we send to the entrypoint are: the recipient address; and the token_id to be sent to the receiver.
In JSON format, our transaction arguments look like this:
```
{
  "transfer_nft": {
    "recipient": "archway1y00hm50lffnxt5m0kuy9afk83gyuye684zwcr5",
    "token_id": "1"
  }
}
```
Using the Developer CLI, we broadcast the transaction and include the above parameters like this:
```
archway contracts execute basic-nft --args '{"transfer_nft":{"recipient":"archway1y00hm50lffnxt5m0kuy9afk83gyuye684zwcr5","token_id":"1"}}'
```

make yout own transactions
```
archway contracts execute testnft --args '{"transfer_nft":{"recipient":"archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p","token_id":"1"}}'
```

result
```
✔ Enter the name or address of the account that will send the transaction … arch
Executing contract testnft
  Chain: constantine-3
  Signer: arch

✅ Executed contract  testnft-0.1.0
  Transaction: E62D3C7EFF88228F90339D7AF7F135305D2B161B3A89CED54A46CA91598872E0
```

```
archway accounts list

Name: arch
Address: archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz

Name: test
Address: archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p
```

Once the transaction is confirmed, ownership of the token will be changed from the address declared as owner at minting (archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz in this guides's example), to the new receiver address (archway1pdl88mh90dp4xeewna75shn774qxq7u2ez765p in this guides's example). To verify that's the case, we can query the contract again to see who owns the token_id with the value of 1.

```
archway contracts query smart testnft --args '{"nft_info":{"token_id":"1"}}'
```

result
```
{
  "token_uri": null,
  "extension": {
    "image": "ipfs://QmZdPdZzZum2jQ7jg1ekfeE3LSz1avAaa42G6mfimw9TEn",
    "image_data": null,
    "external_url": null,
    "description": "All about Arcway making NFT guide",
    "name": "All about Archway NFT #1",
    "attributes": [
      {
        "display_type": null,
        "trait_type": "tutorial",
        "value": "https://docs.archway.io/developers/guides/nft-project/start"
      }
    ],
    "background_color": null,
    "animation_url": null,
    "youtube_url": null
  }
}
```

Now that the contract is up and running, read on to learn how to build a dapp around the minting and transfer functionality we just tested.

Also you can check your transaction here : https://www.mintscan.io/archway-testnet/address/archway1tf629qemlglefs2g8c2hurds8xrwt3wp728ehmts3cv6jaz4xjdqdvn2lg

## SETP07. make NFT Project
you can build your nft project from here
https://github.com/archway-network/dapp-examples/tree/main/vuejs/nft-basic

https://docs.archway.io/developers/guides/nft-project/start

```
git clone https://github.com/archway-network/dapp-examples.git
```

## Sites Where you can check NFTs
- nft marketplace in archway

https://blog.archway.io/ambur-archways-premier-nft-marketplace-b4bf70ea861f


- exploreres in archway

https://docs.archway.io/resources/blockexplorers

- check in mintscan
you can check tx in mintscan

https://www.mintscan.io/archway-testnet/address/archway1a8k9rf2ql98wgu5j955j9mucrk3w6salpzrddz