<template>
  <div class="Condition">
    <div class="Condition-main">
      <div class="Condition-prefix"
        v-if="(conditionNumber > 1)"
        v-bind:class="[
          { 'Condition-prefix--status': condition === 'status' },
          { 'Condition-prefix--type': condition === 'type' },
          { 'Condition-prefix--ages': condition === 'ages' }
          ]"
      >
        И
      </div>
      <div class="Condition-title"
      v-bind:class="[
        { 'Condition-title--status': condition === 'status' },
        { 'Condition-title--type': condition === 'type' },
        { 'Condition-title--ages': condition === 'ages' }
        ]"
      >
        Условие {{ conditionNumber }}
      </div>

      <select class="Condition-select" v-model="condition">
        <option :value="null">Выберете условие</option>
        <option value="status">Статус карты лояльности</option>
        <option value="type">Тип карты лояльности</option>
        <option value="ages">Возраст респондента</option>
      </select>

      <button class="Condition-button Condition-button--red Condition-delete" @click="$emit('onDelete')">Удалить условие</button>
    </div>

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

<style lang="scss" src="@/styles/components/chose-condition.scss"></style>
