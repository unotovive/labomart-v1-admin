<template>
<div class="page">
  <div class="addform">
    <input type="number" v-model="form.jan"/>
    <input type="number" v-model="form.amount"/>
    <input type="number" v-model="form.price"/>
    <input type="text" v-model="form.img"/>
    <button>JANから画像を検索する。</button>
    <button>登録</button>
    <button>クリア</button>
  </div>
  <div>
    <div>
      商品一覧
    </div>
    <div>
      <div>
        <div v-for="(item, index) in items" :key="index">
          {{item.name}}
          {{item.price}}
          {{item.amount}}
          {{item.jan}}
          <img :src="item.img">
        </div>
      </div>
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

  private created() {
    this.itemGetAll();
  }

  private async itemGetAll() {
    const res = await axios.get('http://localhost:3000/api/item/all');
    this.items = res.data;
  }
}
</script>
<style lang="scss" scoped>
.page {
  width: 100%;
  height: 100%;
  overflow: auto;
}
.addform {
  margin: 5%;
  height: 100px;
  width: 90%;
  background: #000;
}
</style>
