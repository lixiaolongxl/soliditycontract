<script setup>
import { ethers } from "ethers";
import { onMounted, reactive } from "vue";
import { ref } from "vue";
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
const count = ref(0);
const blance = ref(0);
const address = ref("");
const amount = ref("");
const data = reactive({ count: null });
let url ="https://eth-ropsten.alchemyapi.io/v2/gisRzIrsRjPEifAyhwmR7nGiG8BwP7E0";
const praykey ="39b8c35b6d7a2e010b696eedda843e3696d8970e1e5861fd5bb970fbda3b5407";

// let customHttpProvider = new ethers.providers.JsonRpcProvider(url);
let customHttpProvider = ethers.getDefaultProvider("ropsten");
// let provider = new ethers.providers.Web3Provider(web3.currentProvider);
let provider = new ethers.providers.Web3Provider(window.ethereum);





// let walletPath = {
//     "standard": "m/44'/60'/0'/0/0",

//     // @TODO: Include some non-standard wallet paths
// };

// let mnemonic = "field today burden puppy mercy bind plate despair pumpkin deny walk element";
// // debugger
// let hdnode = ethers.utils.HDNode.fromMnemonic(mnemonic);
// let node = hdnode.derivePath(walletPath.standard);

// let wallet1 = new ethers.Wallet(node.privateKey);
// console.log(wallet1);






// console.log(provider);
// console.log(provider.getSigner(0))

const wallet = new ethers.Wallet(praykey, provider);
const abi = [
	{
		"inputs": [
			{
				"internalType": "address",
				"name": "funderadderss",
				"type": "address"
			},
			{
				"internalType": "uint256",
				"name": "index",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "_amount",
				"type": "uint256"
			}
		],
		"name": "contribute",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "index",
				"type": "uint256"
			}
		],
		"name": "isComplete",
		"outputs": [
			{
				"internalType": "bool",
				"name": "",
				"type": "bool"
			}
		],
		"stateMutability": "payable",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "kill",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "address",
				"name": "_needer",
				"type": "address"
			},
			{
				"internalType": "uint256",
				"name": "_goal",
				"type": "uint256"
			}
		],
		"name": "newNeeder",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "address",
				"name": "_account",
				"type": "address"
			}
		],
		"name": "transfer",
		"outputs": [],
		"stateMutability": "payable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "amount",
				"type": "uint256"
			}
		],
		"name": "withdraw",
		"outputs": [],
		"stateMutability": "payable",
		"type": "function"
	},
	{
		"stateMutability": "nonpayable",
		"type": "fallback"
	},
	{
		"inputs": [],
		"stateMutability": "payable",
		"type": "constructor"
	},
	{
		"inputs": [],
		"name": "getblance",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "index",
				"type": "uint256"
			}
		],
		"name": "getInfo",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "getNeederList",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "pure",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "neederAccount",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"name": "needermap",
		"outputs": [
			{
				"internalType": "address",
				"name": "neederaddress",
				"type": "address"
			},
			{
				"internalType": "uint256",
				"name": "goal",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "amount",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "fountCount",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	}
]
const contractAddress = "0xC82316F84BE60F183D8E4EE4278aD67d4478151c";
// 合约实例
let contract = new ethers.Contract(contractAddress, abi, provider);
let contractWithSigner = contract.connect(wallet);

// let mnemonic =
//   "field today burden puppy mercy bind plate despair pumpkin deny walk element";
// let hdnode = ethers.utils.HDNode.fromMnemonic(mnemonic);
// let node = hdnode.derivePath("m/44'/60'/0'/0");
// console.log(node.privateKey,1);
// let wallet1 = new ethers.Wallet(node.privateKey);
// console.log(wallet1.address,2);

// console.log(wallet.address);
(async () => {
  let bumber = await customHttpProvider.getBlockNumber();
  // console.log(bumber);
  count.value = bumber;
  const signer = provider.getSigner();
//   console.log(signer);

  let num = await customHttpProvider.getBalance(
    "0x70B8C1464B3fb381E3f0b4D0F4d3f0950083d943"
  );
  blance.value = ethers.utils.formatEther(num);
  // let balancePromise = wallet.getBalance();

  // balancePromise.then((balance) => {
  //   console.log(ethers.utils.formatEther(balance));
  // });

  // let transactionCountPromise = wallet.getTransactionCount();

  // transactionCountPromise.then((transactionCount) => {
  //   console.log(transactionCount);
  // });
  // let amount = ethers.utils.parseEther("1.0");
})();
const kill = async () => {
  let tx = await contractWithSigner.kill();
  console.log(tx.hash);
  let res = await tx.wait();
  console.log(res);
};
const getaccount = async () => {
  let tx = await contract.getInfo(1);
  console.log(tx[0].toString());
  console.log(tx[1].toString());
  console.log(tx[2].toString());
};
const transfer = async () => {
  let overrides = {
    value: ethers.utils.hexlify(ethers.utils.parseEther("0.1")),
    from: wallet.address,
  };
  let tx = await contractWithSigner.transfer(address.value, overrides);
  console.log(tx.hash);
  let res = await tx.wait();
  console.log(res);
};
// 转账
const qiyong = async () => {
  let accounts = await ethereum.request({ method: "eth_requestAccounts" });
  
  data.count = accounts;
  console.log(accounts);
};
const createzc = async () => {
  // console.log(address ,amount);

  let tx = await contractWithSigner.newNeeder(address.value, amount.value);
  console.log(tx.hash);
  let res = await tx.wait();
  console.log(res);
};
const getblance = async () => {
  let money = await contract.getblance();
  console.log(money.toString());
};
const shend = async () => {
  //   let tx = {
  //     to: "0x14bc193D8aB5e4952E0CB0dC8F674461911c7312",
  //     value: ethers.utils.parseEther("0.1"),
  //   };9
  //   let send = await wallet.sendTransaction(tx);
  //   let aw = await send.wait();
  //   console.log(aw);

  //   console.log(ethers.utils.hexlify(ethers.utils.parseEther("0.1")));

  let res = await ethereum.request({
    method: "eth_sendTransaction",
    params: [
      {
        from: data.count[0],
        to: "0x70B8C1464B3fb381E3f0b4D0F4d3f0950083d943",
        value: ethers.utils.hexlify(ethers.utils.parseEther("0.1")),
      },
    ],
  });
  console.log(res);
};
</script>

<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <HelloWorld msg="Hello Vue 3 + Vite" />
  <el-input v-model="address" placeholder="请输入众筹人账户地址"></el-input>
  <el-input v-model="amount" placeholder="请输入众筹金额"></el-input>
  <el-button type="primary" @click="shend">转账</el-button>
  <el-button type="primary" @click="qiyong">启用</el-button>
  <el-button type="primary" @click="getblance">获取合约账户的余额</el-button>
  <el-button type="primary" @click="createzc">创建众筹项目</el-button>
  <el-button type="primary" @click="transfer">合约转账</el-button>
  <el-button type="primary" @click="getaccount">获取指定账户金额</el-button>
  <!-- <el-button type="primary" @click="kill">销毁合约</el-button> -->

  <div>快高度 {{ count }}</div>
  <div>当前金额 {{ blance }}</div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
