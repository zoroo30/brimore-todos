<template>
  <form @submit.prevent="add">
    <a-input
      class="dark-input"
      placeholder="What do you need to do?"
      v-model:value="newTodo"
      @keydown.esc="cancel"
    >
      <template #prefix>
        <plus-outlined @click="add" />
      </template>
    </a-input>
  </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { PlusOutlined } from '@ant-design/icons-vue';
import { Input } from 'ant-design-vue';
import { mapActions } from 'vuex';

export default defineComponent({
  components: {
    PlusOutlined,
    'a-input': Input,
  },
  data() {
    return {
      newTodo: '',
    };
  },
  methods: {
    ...mapActions('todos', ['addTodo']),
    add() {
      this.addTodo(this.newTodo);
      this.newTodo = '';
    },
    cancel() {
      (document.activeElement as HTMLElement).blur();
      this.newTodo = '';
    },
  },
});
</script>

<style scoped></style>

<style lang="scss">
.ant-input-affix-wrapper,
.dark-input.ant-input-affix-wrapper input.ant-input {
  border: 0 !important;
  background-color: var(--light3) !important;
}

.dark-input.ant-input-affix-wrapper {
  padding: 10px !important;
  border-radius: 5px !important;
}

.dark-input.ant-input-affix-wrapper input.ant-input {
  font-weight: 700;
  color: var(--dark);
}

.dark-input.ant-input-affix-wrapper .ant-input-prefix {
  margin-right: 10px !important;
  cursor: pointer;
}

.dark-input.ant-input-affix-wrapper input.ant-input::-webkit-input-placeholder {
  /* WebKit, Blink, Edge */
  color: var(--light) !important;
}
.dark-input.ant-input-affix-wrapper input.ant-input:-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: var(--light) !important;
  opacity: 1;
}
.dark-input.ant-input-affix-wrapper input.ant-input::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: var(--light) !important;
  opacity: 1;
}
.dark-input.ant-input-affix-wrapper input.ant-input:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: var(--light) !important;
}
.dark-input.ant-input-affix-wrapper input.ant-input::-ms-input-placeholder {
  /* Microsoft Edge */
  color: var(--light) !important;
}

.dark-input.ant-input-affix-wrapper input.ant-input::placeholder {
  /* Most modern browsers support this now. */
  color: var(--light) !important;
}
</style>
