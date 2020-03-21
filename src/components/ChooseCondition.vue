<template>
  <div>
    <div>Условие {{ conditionNumber }}</div>

    <select v-model="condition">
      <option :value="null">Выберете условие</option>
      <option value="status">Статус карты лояльности</option>
      <option value="type">Тип карты лояльности</option>
      <option value="ages">Возраст респондента</option>
    </select>

    <button @click="$emit('onDelete')">Удалить условие</button>

    <br /><br />

    <div v-if="condition === 'status'">
      <StatusCondition @createForm="$emit('createForm', $event)" />
    </div>

    <div v-else-if="condition === 'type'">
      <TypeCondition @createForm="$emit('createForm', $event)" />
    </div>

    <div v-else-if="condition === 'ages'">
      <AgesCondition @createForm="$emit('createForm', $event)" />
    </div>
  </div>
</template>

<script>
import TypeCondition from "@/components/TypeCondition.vue";
import StatusCondition from "@/components/StatusCondition.vue";
import AgesCondition from "@/components/AgesCondition.vue";

export default {
  name: "ChooseCondition",
  components: {
    TypeCondition,
    StatusCondition,
    AgesCondition
  },
  props: {
    conditionNumber: Number
  },
  data: () => ({
    condition: null
  }),
  watch: {
    condition: function() {
      this.condition === null && this.$emit("createForm", null);
      this.$emit("conditionType", this.condition);
    }
  }
};
</script>
