# Basic Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, a sample script that deploys that contract, and an example of a task implementation, which simply lists the available accounts.

Try running some of the following tasks:

```shell
npx hardhat accounts
npx hardhat compile
npx hardhat clean
npx hardhat test
npx hardhat node
node scripts/sample-script.js
npx hardhat help
```
**Since I kept gettin insuficient founds...**
tutorial adress: 0xa9816a5aef50f220beb9692df9d4249fd6f2bd8f

## Well commented BUY ME A COFFE
```js
const hre = require("hardhat");

// returns the ETH balance of a given address
async function getBalance(address) {
  // gets the balance of the contract (in the format Solidity works whit no decimals)
  const BalanceDigits = await hre.waffle.provider.getBalance(address);
  // formats the number to decimal number
  return hre.ethers.util.formatEther(BalanceDigits);
}

// Logs the ETH blance from a list of addresses
async function printBalances(addresses) {
  let index = 1;

  for (const address of addresses) {
    //? test this later
    // console.log(`Addres N.${index} did a deposit of ${ await getBalance(address)}`);
    console.log(`Addres N.${index} did a deposit of`, await getBalance(address));
    index++;
  }
}

async function printMemos(memos) {
  /* From contract struct
  * memo.timestamp = time at wich the block was mined
  * memo.name = name of the tipper
  * memo.from = address of the tipper
  * memo.msg = message from the tipper
  */
  for (const memo of memos) {
    console.log(`At ${memo.timestamp}, 
  ${memo.name}(${memo.from}) said ${memo.msg}`);
  }
}

async function main() {
  // Get test accounts from hardhat
  const [owner, tipper1, tipper2, tipper3] = await hre.ethers.getSigners();

  // Get an instance of the contract & Deploy it locally
  const BuyMeCoffe = await hre.ethers.getContractFactory("BuyMeCoffe");
  const buyMeCoffe = await BuyMeCoffe.deploy();
  await buyMeCoffe.deployed();
  console.log("Contract buyMeCoffe deployed to ", buyMeCoffe.address);
  // console.log('OWNER', owner.address, '\nTIPPER 1 ', tipper1.address);

  // Check contract balances tips
  const adresses = [owner.adress, tipper1.adress, buyMeCoffe.address];
  console.log("*** START ***");
  await printBalances(adresses);

  // Check balances after tips

  // Withdraw founds

  // Check balance after withdraw

  // Read all the memos left for the owner

}


main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```