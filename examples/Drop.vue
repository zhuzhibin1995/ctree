<template>
  <div>
    <div style="width: 200px;">
      <p>自定义展示 slot ：</p>
      <CTreeDrop v-model="value" :data="data" checkable clearable drop-placeholder="请选择" :placement="placement"
        :dropdown-min-width="300" dropdown-width-fixed @checked-change="handleCheckedChange">
        <template v-slot:display="scope">
          <div style="width: 170px; text-overflow: ellipsis; overflow: hidden;">{{
            scope.checkedNodes.map((node) =>
              node.title).join(',')
          }}</div>
        </template>
        
      </CTreeDrop>
      {{ value }}
    </div>
    <div style="width: 200px;">
      <p>默认：</p>
      <CTreeDrop v-model="value" :data="data" checkable clearable drop-placeholder="请选择" :placement="placement"
        :dropdown-min-width="300" dropdown-width-fixed @checked-change="handleCheckedChange">
        <template #empty>slot 传进来的暂无数据</template>
      </CTreeDrop>
      {{ value }}
    </div>
  </div>
</template>

<script lang="ts">
import { CTreeDrop } from '../src'
import treeDataGenerator from '../tests/tree-data-generator'
import { defineComponent, ref } from 'vue-demi'

const genData = (extra = {}) => {
  return treeDataGenerator(Object.assign({
    treeDepth: 3,
    nodesPerLevel: 5,
    sameIdTitle: true,
    inOrder: true,
    forceString: true,
  }, extra))
}

export default defineComponent({
  name: 'Drop',
  components: {
    CTreeDrop,
  },
  setup() {
    const data = ref(genData().data)
    const value = ref('2')
    const placement = ref('bottom-start')
    function handleCheckedChange(){
      console.log('checked-change')
    }
    return {
      data,
      value,
      placement,
      handleCheckedChange
    }
  }
})
</script>
