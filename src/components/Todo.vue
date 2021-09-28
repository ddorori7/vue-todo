<template>
  <div class="d-flex align-items-start p-2 justify-content-between">
    <div class="d-flex align-items-start justify-content-center">
      <input
        class="my-auto"
        type="checkbox"
        :checked="todo.checked"
        @change="toggleCheckbox"
      />
      <span class="ml-3" :class="todo.checked ? 'todo-complete' : ''">{{
        todo.text
      }}</span>
    </div>
    <button class="btn btn-danger btn-sm" @click="clickDelete">삭제</button>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  methods: {
    toggleCheckbox(e) {
      // toggle-checkbox 라는 이름으로 {} 안의 값을 부모 컴포넌트로 보내줌
      this.$emit("toggle-checkbox", {
        id: this.todo.id,
        checked: e.target.checked,
      });
    },
    clickDelete() {
      this.$emit("click-delete", {
        id: this.todo.id,
      });
    },
  },
};
</script>

<style>
.todo-complete {
  color: gray;
  text-decoration: line-through;
}
</style>
