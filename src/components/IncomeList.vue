<template>
  <div class="income-list">
    <IncomeItem
      v-for="data in income"
      :key="data.id"
      :data="data"
      @remove-item="removeItem"
    />
  </div>
</template>

<script>
import IncomeItem from "./IncomeItem.vue";

export default {
  name: "IncomeList",
  props: {
    income: Array,
  },
  setup(props, { emit }) {
    function removeItem(id) {
      emit("remove-item", id);
    }

    return {
      removeItem,
    };
  },
  components: {
    IncomeItem,
  },
  mounted() {
    console.log(this.income);
  },
};
</script>

<style scoped>
.income-list {
  margin-top: 30px;
  padding: 15px;
}
</style>