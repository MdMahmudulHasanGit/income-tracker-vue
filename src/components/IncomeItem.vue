<template>
  <div class="income-item">
    <div class="removeItem" @click="removeItem">x</div>
    <div class="desc">{{ desc }}</div>
    <div class="price">${{ value }}</div>
    <div class="date">{{ date }}</div>
  </div>
</template>

<script>
import { reactive, toRefs, computed } from "vue";
export default {
  name: "IncomeItem",
  props: {
    data: Object,
  },
  setup(props, { emit }) {
    const incomeData = reactive({
      desc: props.data.desc,
      value: props.data.value,
      date: computed(() => {
        let date = new Date(props.data.date);
        let day = date.getDate();
        let month = date.getMonth();
        let year = date.getFullYear();

        return day + "/" + month + "/" + year;
      }),
    });

    function removeItem() {
      emit("remove-item", props.data.id);
    }

    return {
      ...toRefs(incomeData),
      removeItem,
    };
  },
};
</script>

<style scoped>
.income-item {
  position: relative;
  display: flex;
  padding: 15px 15px 15px 0px;
  background-color: #fff;
  border-radius: 8px;
  max-width: 600px;
  margin: 0 auto 30px;
}

.removeItem {
  color: #ef2d2d;
  font-weight: 600;
  font-size: 20px;
  line-height: 1;
  text-align: center;
  margin: 0 15px;
}

.desc {
  color: #666;
  flex: 1 1 100%;
  font-size: 20px;
}

.price {
  color: #666;
  min-width: 100px;
  font-size: 20px;
}

.date {
  color: #666;
  text-align: right;
  font-size: 20px;
}
</style>