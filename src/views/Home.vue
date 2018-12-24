<template>
  <div>
    <button @click="$router.push('/items')">Itemの管理</button>
  </div>
</template>
<script lang="ts">
import { Vue, Component, Prop, Watch } from 'vue-property-decorator';
@Component({})
export default class Home extends Vue {
}
</script>
<style lang="scss" scoped>
</style>
