<template>
  <Header :totalIncome="totalIncome" />
  <Form />
</template>

<script>
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import { reactive, computed, toRefs, onMounted } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      income: [
        {
          value: 400,
        },
      ],
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        }
        return temp;
      }),
    });

    return {
      ...toRefs(state),
    };
  },
  components: {
    Header,
    Form,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}

body {
  background: #eee;
}
</style>
