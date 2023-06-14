<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <!--    <el-button type='primary'>哈哈哈</el-button>-->
    <el-table ref="tableRef" :data="data" stripe>
      <el-table-column>
        <div class="drag-handle">☰</div>
      </el-table-column>
      <el-table-column v-for="col in columns" :label="col.label" :key="col.col" draggable="true">
        <template v-slot="{ row }">
          <span>{{ row[col.col] }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script setup lang="ts">
  import { ElButton, ElTable, ElTableColumn } from 'element-plus';
  import Sortable from 'sortablejs';
  import { onMounted, ref } from 'vue';
  const tableRef = ref()
  onMounted(() => {
    let tbody = document.querySelector('.el-table__body-wrapper tbody') as HTMLElement;
    Sortable.create(tbody, {
      group: {
        // 相同的组之间可以相互拖拽
        name: 'table',
        pull: true,
        put: true,
      },
      animation: 150, // ms, number 单位：ms，定义排序动画的时间
      onAdd: function (e: any) {
        // 拖拽时候添加有新的节点的时候发生该事件
        // console.log('onAdd.foo:', e);
      },
      onUpdate: function (e: any) {
        // 拖拽更新节点位置发生该事件
        // console.log('onUpdate.foo:', e);
      },
      onRemove: function (e: any) {
        // 删除拖拽节点的时候促发该事件
        // console.log('onRemove.foo:', e);
      },
      onStart: function (e: any) {
        // 开始拖拽出发该函数
        // console.log('onStart.foo:', e);
      },
      onSort: function (e: any) {
        // 发生排序发生该事件
        // console.log('onUpdate.foo:', e);
      },
      onEnd(e: any) {
        // 结束拖拽
        // 如果拖拽结束后顺序发生了变化，则对数据进行修改
        if (e.oldIndex !== e.newIndex) {
          moveTable(e.oldIndex, e.newIndex); // 排序后和后端的交互函数
        }
      },
    });
  });
  const moveTable = (oldIndex: number, newIndex: number) => {
    const draggedItem = tableRef.value.data?.splice(oldIndex, 1)[0];
    tableRef.value.data?.splice(newIndex, 0, draggedItem);
  };
  defineProps<{
    msg: string;
  }>();
  const data = [
    {
      id: Math.random().toString(10),
      name: '张三',
      sex: 'man',
      age: 30,
      department: '技术部',
      position: 'CTO',
    },
    {
      id: Math.random().toString(10),
      name: '李四',
      sex: 'man',
      age: 23,
      department: '技术部',
      position: '后端开发',
    },
    {
      id: Math.random().toString(10),
      name: '赵八',
      sex: 'man',
      age: 22,
      department: '技术部',
      position: '前端开发',
    },
    {
      id: Math.random().toString(10),
      name: '王三',
      sex: 'man',
      age: 28,
      department: '技术部',
      position: '项目总监',
    },
  ];
  const columns = [
    {
      col: 'id',
      label: 'ID',
    },
    {
      col: 'name',
      label: '姓名',
    },
    {
      col: 'sex',
      label: '性别',
    },
    {
      col: 'age',
      label: '年龄',
    },
    {
      col: 'department',
      label: '部门',
    },
    {
      col: 'position',
      label: '职位',
    },
  ];
</script>

<style scoped>
  h1 {
    font-weight: 500;
    font-size: 2.6rem;
    top: -10px;
  }

  h3 {
    font-size: 1.2rem;
  }

  .greetings h1,
  .greetings h3 {
    text-align: center;
  }

  @media (min-width: 1024px) {
    .greetings h1,
    .greetings h3 {
      text-align: left;
    }
  }
</style>
