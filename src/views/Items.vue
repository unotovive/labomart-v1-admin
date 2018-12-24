<template>
<div class="page">
  <h1>Items</h1>
  <h2>Stock List</h2>
  <div class="cards">
    <div v-for="(item, index) in items" :key="index" class="card">
      <img class="image" :src="item.img">
      <div class="info">
        <div class="data">
          <h3>&yen;{{item.price}}</h3>
          <h3 :class="{ warn: item.amount < 10 }">{{item.amount}}<span style="font-size: 0.8rem; color: #96A0B8;">pcs</span></h3>
        </div>
        <p class="name">{{item.name}}</p>
      </div>
    </div>
  </div>
  <div class="add" @click="isAddMenuOpened = true">×</div>
  <div class="modal" @click="isAddMenuOpened = false" v-if="isAddMenuOpened">
    <div class="form" @click.stop="">
      <h1>Add new items</h1>
      <div class="inputs">
        <input v-model="form.jan" placeholder="JANを入力"/>
        <input v-model="form.price" placeholder="金額を入力"/>
        <input v-model="form.amount" placeholder="個数を入力"/>
        <input v-model="form.name" placeholder="商品名を入力"/>
        <input v-model="form.img" placeholder="画像のＵＲＬを入力"/>
      </div>
      <div class="addsubmit" @click="submit"><p>登録</p></div>
    </div>
  </div>
</div>
</template>
<script lang="ts">
import { Vue, Component, Prop, Watch } from 'vue-property-decorator';
import axios from 'axios';
@Component({})
export default class Items extends Vue {
  private form = {
    jan: null,
    price: null,
    amount: null,
    img: '',
  };
  private items = null;
  private isAddMenuOpened: boolean = false;
  private created() {
    this.itemGetAll();
  }

  private async itemGetAll() {
    const res = await axios.get('http://localhost:3000/api/item/all');
    this.items = res.data;
  }
  private async submit() {
    const param = this.form;
    const req = await axios.post('http://localhost:3000/api/item/add', param);
    const res = await axios.get('http://localhost:3000/api/item/all');
    this.items = res.data;
  }
}
</script>
<style lang="scss" scoped>
.page {
  width: calc( 100% -280px );
  height: 100%;
  overflow: auto;
  background: rgba($color: #F6F6FC, $alpha: 0.99);
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.addform {
  margin: 5%;
  height: 100px;
  width: 90%;
  background: #000;
}

h1 {
  margin-top: 1.8rem;
  margin-left: 1.2em;
}

h2 {
  margin-left: 1.8rem;
  font-size: 1em;
}

.cards {
  display: flex;
  flex-wrap: wrap;
}

.card {
  width: 200px;
  height: 300px;
  background: #fff;
  border-radius: 10px;
  margin: 1em;
  cursor: pointer;
}

.card:hover {
  box-shadow: 0 0 15px rgba(0,0,0,.3);
}

.image {
  width: 180px;
  height: 190px;
  margin-top: 10px;
  padding-bottom: 10px; 
  border-bottom: 3px solid;
  img {
    box-shadow: inset 0 0 15px rgba(0,0,0,.3);
  }
}
.info {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 70px;
}

.warn {
  color: rgb(219, 58, 71) !important;
}

h3 {
  padding: 0;
  margin: 0 10px;
  font-size: 2em;
}
.data {
  display: flex;
  justify-content: space-between;
}
.name {
  font-size: 0.8em;
  padding: 0;
  margin: 0;
}

.add {
  width: 100px;
  height: 100px;
  border-radius: 30px;
  transform: rotate(45deg);
  padding: 0;
  margin: 0;
  position: absolute;
  bottom: 60px;
  right: 60px;
  background: rgb(124, 255, 130);
  color: #fff;
  font-size: 2.2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 10px 10px 86px -23px rgba(0,0,0,0.75);
  cursor: pointer;
  user-select: none;
}

.addsubmit{
  width: 50px;
  height: 50px;
  border-radius: 15px;
  transform: rotate(45deg);
  padding: 0;
  margin: 0;
  background: rgb(124, 255, 130);
  color: #fff;
  font-size: 1.2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 10px 10px 86px -23px rgba(0,0,0,0.75);
  cursor: pointer;
  user-select: none;
  p {
    transform: rotate(-45deg)
  }
}

.addsubmit:hover {
  background: rgb(114, 245, 120);
}

.addsubmit:active {
  background: rgb(104, 235, 110);
}

.add:hover {
  background: rgb(114, 245, 120);
}

.add:active {
  background: rgb(104, 235, 110);
}

.modal {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0,0,0,0.75);
  display: flex;
  justify-content: center;
  align-items: center;
}

.form {
  width: 500px;
  height: 500px;
  background: #fff;
  border-radius: 20px;
  padding: 30px;
}

.inputs {
  display: flex;
  flex-direction: column;
}
input {
  height: 2em;
  border: 1px solid #888;
  border-radius: 2px;
  margin-bottom: 1em;
}
</style>
