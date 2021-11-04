<script setup>
import { ethers } from "ethers";
import { onMounted, reactive } from "vue";
import { ref } from "vue";
import json from "./Migrations.json";
// import Web3 from "web3";
// const json = require('./Migrations.json');
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
const count = ref(0);
const blance = ref(0);
const address = ref("");
const amount = ref("");
const data = reactive({ count: null });
//  let web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
// let currentProvider1 = new Web3.providers.HttpProvider('http://localhost:8545');
// console.log(currentProvider1);
const url = "http://localhost:8545";

// Or if you are running the UI version, use this instead:
// const url = "http://localhost:7545"
const praykey ="5895ae9bdb65b71fe0345f11017758eaab12b3d3380d7dfa194dabcb739d7a82";

const contractAddress = '0xBffdae356dc4b7532e11029F111409b775BD8AF5';
const provider = new ethers.providers.JsonRpcProvider(url);
// 合约实例// 
// let provider = new ethers.providers.Web3Provider(web3.currentProvider);
let contract = new ethers.Contract(contractAddress, json.abi, provider);
const wallet = new ethers.Wallet(praykey, provider);
let contractWithSigner = contract.connect(wallet);
(async () => {
  let bumber = await provider.getBlockNumber();
  count.value = bumber;
  const signer = provider.getSigner();
  let num = await provider.getBalance(
    "0x1C1aBC330E7fF700148A2e5D08f148b4a77a5338"
  );
  blance.value = ethers.utils.formatEther(num);
})();
const kill = async () => {
  //   let tx = await contractWithSigner.kill();
  //   console.log(tx.hash);
  //   let res = await tx.wait();
  //   console.log(res);
};
const getaccount = async () => {
    let tx = await contract.getname();
	console.log(tx);
	
  //   console.log(tx[0].toString());
  //   console.log(tx[1].toString());
  //   console.log(tx[2].toString());
};
contractWithSigner.on("HandlesetName", (oldValue, newValue, event) => {
    console.log(oldValue, newValue,event);
});
const transfer = async () => {
	// debuggerconnect(addr1)
	let tx = await contractWithSigner.setname('lxl2221111');
	let res = await tx.wait();
	console.log(res);
	
  //   let overrides = {
  //     value: ethers.utils.hexlify(ethers.utils.parseEther("0.1")),
  //     from: wallet.address,
  //   };
  //   let tx = await contractWithSigner.transfer(address.value, overrides);
  //   console.log(tx.hash);
  //   let res = await tx.wait();
  //   console.log(res);
};
// 转账
const qiyong = async () => {
  let accounts = await ethereum.request({ method: "eth_requestAccounts" });

  data.count = accounts;
  console.log(accounts);
};
const createzc = async () => {
  // console.log(address ,amount);
  //   let tx = await contractWithSigner.newNeeder(address.value, amount.value);
  //   console.log(tx.hash);
  //   let res = await tx.wait();
  //   console.log(res);
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
