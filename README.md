# Crowdfunding-PupperCoin
Advanced Solidity


![kisspng](/Images/kiss.png)

## Project: Crowdsale PupperCoin token in order to help fund the network development

The network will be used to track the dog breeding activity across the globe in a decentralized way, and allow humans to track the genetic trail of their pets after all the necessary legal bodies give approval on creating a crowdsale open to the public. The requirements are to enable refunds if the crowdsale is successful and the goal is met, and only a maximum of 300 Ether are allowed to be raised. The crowdsale will run for 24 weeks.

An ERC20 token will be created which will be minted through a `Crowdsale` contract that can be leveraged from the OpenZeppelin Solidity library. This crowdsale contract will manage the entire process, allowing users to send ETH and get back PUP (PupperCoin). This contract will mint the tokens automatically and distribute them to buyers in one transaction. It will need to inherit `Crowdsale`, `CappedCrowdsale`, `TimedCrowdsale`, `RefundableCrowdsale`, and `MintedCrowdsale`. The crowdsale will be conducted on the Kovan or Ropsten testnet in order to get a real-world pre-production test in.

## Project Guidelines

### Creating the project

- Create a file called `PupperCoin.sol` and a standard `ERC20Mintable` using Remix. 

- Create a new contract named PupperCoinCrowdsale.sol, and prepare it like a standard crowdsale.


### Designing the contracts

#### ERC20 PupperCoin

- Use a standard `ERC20Mintable` and `ERC20Detailed` contract, hardcoding `18` as the `decimals` parameter, and leaving the `initial_supply` parameter alone. We didn't need to hardcode the decimals, however since most use-cases match Ethereum's default, you may do so.


#### PupperCoinCrowdsale

- Create a file named `Crowdsale.sol` in Remix.

- Bootstraped the contract by inheriting the following OpenZeppelin contracts:

  * `Crowdsale`

  * `MintedCrowdsale`

  * `CappedCrowdsale`

  * `TimedCrowdsale`

  * `RefundablePostDeliveryCrowdsale`

- Provide parameters for all of the features of the crowdsale, such as the `name`, `symbol`, `wallet` for fundraising, `goal`, etc. It can be configured to your liking.

- Hhardcode a `rate` of 1, to maintain parity with Ether units (1 TKN per Ether, or 1 TKNbit per wei). If you'd like to customize your crowdsale rate, follow the [Crowdsale Rate](https://docs.openzeppelin.com/contracts/2.x/crowdsales#crowdsale-rate) calculator on OpenZeppelin's documentation. Essentially, a token (TKN) can be divided into TKNbits just like Ether can be divided into wei. When using a `rate` of 1, just like 1000000000000000000 wei is equal to 1 Ether, 1000000000000000000 TKNbits is equal to 1 TKN.

- Call the `RefundableCrowdsale` constructor from your `PupperCoinCrowdsale` constructor as well as the others because `RefundablePostDeliveryCrowdsale` inherits the `RefundableCrowdsale` contract, which requires a `goal` parameter. `RefundablePostDeliveryCrowdsale` does not have its own constructor, so just use the `RefundableCrowdsale` constructor that it inherits.

- Don't forget to call the `RefundableCrowdsale` constructor because the `RefundablePostDeliveryCrowdsale` will fail since it relies on it (it inherits from `RefundableCrowdsale`), and does not have its own constructor.

- Use `now` and `now + 24 weeks` to set the times properly from the `PupperCoinCrowdsaleDeployer` contract when passing the `open` and `close` times.

#### PupperCoinCrowdsaleDeployer

Build out the contracts below for deployment. 


![PUP_Contract1](/screenshots_pup/PUP_Contract1.png)


![PUP_Contract2](/screenshots_pup/PUP_CONTRACT2.png)


### Testing the Crowdsale

- Test the crowdsale by sending Ether to the crowdsale from a different account (**not** the same account that is raising funds), then once you confirm that the crowdsale works as expected, try to add the token to MyCrypto and test a transaction. 

- Test the time functionality by replacing `now` with `fakenow`, and creating a setter function to modify `fakenow` to whatever time you want to simulate. You can also set the `close` time to be `now + 5 minutes`, or whatever timeline you'd like to test for a shorter crowdsale.

- Make sure you hit your `goal` that you set, and `finalize` the sale using the `Crowdsale`'s `finalize` function when sending Ether to the contract. In order to finalize, `isOpen` must return false (`isOpen` comes from `TimedCrowdsale` which checks to see if the `close` time has passed yet). Since the `goal` is 300 Ether, you may need to send from multiple accounts. If you run out of prefunded accounts in Ganache, you can create a new workspace.

#### Notes: 

Reminber the refund feature of `RefundablePostDeliveryCrowdsale` only allows for refunds once the crowdsale is closed **and** the goal is met. See the [OpenZeppelin RefundableCrowdsale](https://docs.openzeppelin.com/contracts/2.x/api/crowdsale#RefundableCrowdsale) documentation for details as to why this is logic is used to prevent potential attacks on your token's value.

## Send Transaction to contract wallet in Mycrypto

![SEND2WALLET](/screenshots_pup/SEND2WALLET.png)


## Deploy PupperCoinSaleDeployer Contract

![SALEDEPLOYER](/screenshots_pup/SALEDEPLOYER.png)


## Deploy PupperCoinSale Contract

![SALE](/screenshots_pup/SALE.png)


## Deploy PupperCoin Contract
![PUPPERCOIN](/screenshots_pup/PUPPERCOIN.png)


## Pupper_Sale_Address & Token_Address
![SALE_TOKEN_ADDRESSES](/screenshots_pup/SALE_TOKEN_ADDRESSES.png)


## First Token Purchase 100

![1_TOKEN](/screenshots_pup/1_token.png)

## Second Token Purchase 100

![2_TOKEN_BUY](/screenshots_pup/2_token_buy.png)


## Sale Goal Reached
![GOAL_REACHED](/screenshots_pup/GOAL_REACHED.png)



## You can add custom tokens in MyCrypto from the `Add custom token` feature:

![add-custom-token](https://i.imgur.com/p1wwXQ9.png)


## Added the PC token to Mycrypto Account

![PPC_MYCRYPTO](/screenshots_pup/PPC_MYCRYPTO.png)


## You can also do the same for MetaMask. Make sure to purchase higher amounts of tokens in order to see the denomination appear in your wallets as more than a few wei worth.

![PPCMETA](/screenshots_pup/PPCMETA.png)


### Deploying the Crowdsale

- Deploy the crowdsale to the Kovan or Ropsten testnet, and store the deployed address. 
  * Switch MetaMask to your desired network, and use the `Deploy` tab in Remix to deploy the contracts. T
  * Take note of the total gas cost, and compare it to how costly it would be in reality. Since you are deploying to a network that you don't have control over, faucets will not likely give out 300 test Ether. 
  * Reduce the goal when deploying to a testnet to an amount much smaller, like 10,000 wei.


Deployed Address: PupperCoinSale(pupper_sale_address)-0x

#### Token 

Name: PupperCoin

Symbol: PC

Goal: 300

Duration: 2 hours


