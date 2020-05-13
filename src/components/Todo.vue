<template>
  <li class="d-flex align-items-center list-group-item ">
    <input class="checkmark" type="checkbox" v-model="todo.completed" 
    @change="$emit('on-change')" />
    <span
      class="border-0 flex-grow-1"
      v-if="!isEditing"
      :class="{ mark_completed: todo.completed }"
      >{{ this.todo.description }}</span
    >

    <form v-else class="flex-grow-1" @submit.prevent="finishEditing()">
      <input
        type="text"
        class="form-control"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </form>
    <button
      @click="startEditing()"
      class="btn btn-outline-primary border-0 ml-2"
    >
      <span class="fa fa-edit"></span>
    </button>
    <button
      @click="$emit('on-delete')"
      class="btn btn-outline-danger border-0"
    >
      <span class="fa fa-trash"></span>
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isEditing: false,
      newTodoDescription: ""
    };
  },

  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("on-edit", this.newTodoDescription);
    }
  }
};
</script>

<style lang="scss" scoped>
.mark_completed {
  text-decoration: line-through;
}
span {
  margin-left: 30px;
}
.checkmark {
  height: 18px;
  width: 18px;
}
</style>
