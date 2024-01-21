<template>
  <Header :totalIncome="totalIncome" />
  <Form @add-income="addIncome" />
  <IncomeList :income="income" @remove-item="removeItem" />
</template>

<script>
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import IncomeList from "./components/IncomeList.vue";
import { reactive, computed, toRefs } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      income: [],
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

    function addIncome(data) {
      let d = data.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);

      state.income = [
        ...state.income,
        {
          id: Date.now(),
          desc: data.desc,
          value: parseInt(data.value),
          date: newD.getTime(),
        },
      ];
    }

    function removeItem(id) {
      state.income = state.income.filter(v => v.id != id);
    }

    return {
      ...toRefs(state),
      addIncome,
      removeItem
    };
  },
  components: {
    Header,
    Form,
    IncomeList,
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
