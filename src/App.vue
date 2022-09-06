<template>
  <div>
    <h1>App根组件</h1>
    <hr />
    <TodoInput @add="onAddNewTasks"></TodoInput>
    <!-- 绑定的是数据的引用，所以在子组件中对于数据的修改相当于对于父组件数据的修改 -->
    <TodoList :list="tasklist" class="mt-2"></TodoList>
    <TodoButton v-model:active="activeBtnIndex"></TodoButton>
  </div>
</template>

<script>
// 导入todolist组件
import TodoList from "./components/todo-list/TodoList.vue";
// 导入todoinput组件
import TodoInput from "./components/todo-input/TodoInput.vue";
// 导入todobutton组件
import TodoButton from "./components/todo-button/TodoButton.vue";

export default {
  name: "MyApp",
  data() {
    return {
      // 任务列表的数据
      todolist: [
        {
          id: 1,
          task: "早晨帮太宰先生准备早饭（昨天太宰先生没有入水奖励蟹肉罐头）",
          done: false,
        },
        {
          id: 2,
          task: "下午去鹤见川捞入水的太宰先生（太宰先生入水晚餐的蟹肉取消）",
          done: false,
        },
        {
          id: 3,
          task: "准备和乱步先生出差的资料，安慰因此不满的太宰先生",
          done: true,
        },
      ],
      // 下一个可用的id值
      nextId: 4,
      activeBtnIndex: 0,
    };
  },
  methods: {
    onAddNewTasks(taskname) {
      // 向任务中新增新的任务信息
      this.todolist.push({
        id: this.nextId,
        task: taskname,
        done: false,
      });
      // 让id自增加一
      this.nextId++;
    },
  },
  computed: {
    tasklist() {
      switch (this.activeBtnIndex) {
        case 0:
          return this.todolist;
        case 1:
          return this.todolist.filter((x) => x.done);
        case 2:
          return this.todolist.filter((x) => !x.done);
      }
    },
  },
  components: {
    TodoList,
    TodoInput,
    TodoButton,
  },
};
</script>

<style lang="less" scoped></style>
