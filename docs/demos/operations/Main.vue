<template>
  <div class="main">
    <Operate
      :virtListRef="virtListRef"
      :length="list.length"
      :visible="visible"
      @toggleShow="visible = !visible"
    ></Operate>

    <div style="padding: 10px 0">
      <span>Total: {{ list.length }} </span>
      <span>&nbsp;&nbsp;&nbsp;</span>
      <span>RenderBegin: {{ reactiveData.renderBegin }} </span>
      <span>&nbsp;&nbsp;&nbsp;</span>
      <span>RenderEnd: {{ reactiveData.renderEnd }} </span>
    </div>

    <!-- demo -->
    <!-- important: must set a height for Container or VirtList -->
    <!-- important: must set itemKey and keep id is unique -->
    <div
      class="demo-operate"
      style="width: 100%; height: 500px"
      v-show="visible"
    >
      <VirtList ref="virtListRef" :list="list" itemKey="id" :minSize="40">
        <template #default="{ itemData, index }">
          <Item :itemData="itemData" :index="index" />
        </template>
      </VirtList>
    </div>
  </div>
</template>

<script lang="ts">
import { VirtList } from 'vue-virt-list';
import { getList } from '../utils/common';
import Item from './Item.vue';
import Operate from '../components/OperateGroup.vue';

export default {
  name: 'DemoOperate',
  components: {
    Item,
    VirtList,
    Operate,
  },
  data() {
    return {
      visible: true,
      list: [] as any[],
      virtListRef: null as typeof VirtList | null,
      reactiveData: {
        renderBegin: 0,
        renderEnd: 0,
      },
    };
  },
  mounted() {
    this.virtListRef = this.$refs.virtListRef as typeof VirtList;
    this.reactiveData = (this.$refs.virtListRef as any).reactiveData;
    this.list = getList(2000);

    // setTimeout(() => {
    //   this.list = getList(1000);
    // }, 3000);
  },
};
</script>

<style lang="scss" scoped>
.demo-operate {
  background-color: var(--vp-sidebar-bg-color);
  border: 1px solid var(--vp-c-border);
  overflow: hidden;
}
</style>
