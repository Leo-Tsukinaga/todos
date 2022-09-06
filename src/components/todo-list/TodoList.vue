<template>
  <ul class="list-group">
    <!-- 列表组 -->
    <li
      class="list-group-item d-flex justify-content-between align-items-center"
      v-for="item in list"
      :key="item.id"
    >
      <!-- 复选框 -->
      <div class="custom-control custom-checkbox">
        <!-- 使用双向数据绑定指令v-model绑定数据，因为子组件中的数据是父组件中数据的引用，所以相当于修改了父组件的数据 -->
        <input
          type="checkbox"
          class="custom-control-input"
          :id="'customCheck' + item.id"
          v-model="item.done"
        />
        <!-- 使用样式绑定的方式来美化样式 -->
        <label
          class="custom-control-label"
          :class="item.done ? 'delete' : ''"
          :for="'customCheck' + item.id"
          >{{ item.task }}</label
        >
      </div>

      <!-- 徽标 -->
      <span class="badge badge-success badge-pill" v-if="item.done">完成</span>
      <span class="badge badge-warning badge-pill" v-else>未完成</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    // 列表数据
    list: {
      type: Array,
      required: true,
      default: [],
    },
  },
};
</script>

<style lang="less" scoped>
.list-group {
  width: 400px;
}

// 删除效果
.delete {
  text-decoration: line-through;
  color: gray;
  font-style: italic;
}
</style>
