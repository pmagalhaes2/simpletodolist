<template>
  <div class="todo-list">
    <h3>Todo List</h3>
    <input type="text" v-on:keyup.enter="addNewItemToList" />

    <ul>
      <li v-for="(item, index) in list" :key="index">
        <ListItem :item="item" :index="index" @delete-item="deleteItem" />
      </li>
    </ul>
  </div>
</template>

<script>
import ListItem from "./LisItem";

export default {
  name: "TodoList",
  components: {
    ListItem,
  },
  data() {
    return {
      list: [
        { label: "Learn HTML", checked: false },
        { label: "Learn CSS", checked: false },
      ],
    };
  },
  created() {
    const itensInLocalStorage = JSON.parse(localStorage.getItem("list"));
    this.list = itensInLocalStorage ? itensInLocalStorage : [];
  },
  methods: {
    addNewItemToList(event) {
      const newItem = event.target.value;
      this.list.unshift({
        label: newItem,
        checked: false,
      });

      this.updateLocalStorage();

      event.target.value = "";
    },
    deleteItem(index) {
      this.list.splice(index, 1);
    },
    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-list {
  width: 500px;
  margin: 100px auto;
}

input[type="text"] {
  width: 80%;
  height: 30px;
}

ul {
  list-style: none;
  padding: 0;
  width: 80%;
  margin: 20px auto;
  text-align: left;
}
</style>
