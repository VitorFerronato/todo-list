<template>
  <div class="add-task">
    <input class="form-element" placeholder="Nova tarefa" v-model="name" @keydown.enter="add" type="text" />
    <button class="form-element" @click="add">+</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },

  methods: {
    add() {
      this.$emit("taskAdded", { name: this.name });
      this.name = "";
    },
  },
};
</script>

<style>
.add-task{
  margin: 35px;
}

.form-element{
  outline: none;
  font-size: 2rem;
  border: 1px solid #fff;
  padding: 5px 10px 8px;
  color: #fff;
}

input.form-element{
  width: 500px;
  background-color: #fff2;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

button.form-element{
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  background-color: #2196f3;
  border-left: none;
    cursor: pointer;

}
</style>