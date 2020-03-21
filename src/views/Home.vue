<template>
  <div class="Form">
    <div
      class="Form-conditionBlock"
      :key="condition.idEl"
      v-for="(condition, index) of conditions"
    >
      <ChooseCondition
        @onDelete="deleteCondition(index)"
        @conditionType="setConditionType(index, $event)"
        @createForm="setConditionData(index, $event)"
        :conditionNumber="index + 1"
      />
      <br /><br />
    </div>

    <div>
      Нажмите, чтобы добавить новое условие
      <button @click="addCondition()">+</button>
    </div>

    <br /><br />

    <button @click="getForm()">Далее</button>

    <br /><br />
    <pre>{{ result }}</pre>
  </div>
</template>

<script>
import ChooseCondition from "@/components/ChooseCondition.vue";

export default {
  name: "Home",
  components: {
    ChooseCondition
  },
  data: () => ({
    conditions: [],
    idEl: 0,
    result: null
  }),
  methods: {
    /** Добавить условие */
    addCondition: function() {
      this.conditions.push({ idEl: this.idEl++, data: null });
    },
    /** Удалить условие */
    deleteCondition: function(index) {
      this.conditions.splice(index, 1);
    },
    /** Установить значение нового условия */
    setConditionData: function(index, formData) {
      this.conditions[index].data = formData;
    },
    /** Установить тип условия */
    setConditionType: function(index, type) {
      this.conditions[index].type = type;
    },
    /** Получить сформированную форму */
    getForm: function() {
      let result = {};

      function prepareStatusForm(data) {
        let status = [];
        data.forEach(({ data }) => data.status && status.push(data.status));

        return status;
      }

      function prepareTypeForm(data) {
        let type = [];

        data.forEach(({ data }) => data.type && type.push(data.type));

        return type;
      }

      function prepareAgesForm(data) {
        let ages = [];

        data.forEach(
          ({ data }) => (data.from || data.to) && ages.push({ ...data })
        );

        return ages;
      }

      this.conditions.forEach(({ data, type }) => {
        if (type && !result[type]) {
          result[type] = [];
        }

        switch (type) {
          case "status":
            result[type] = result[type].concat(prepareStatusForm(data));
            break;

          case "type":
            result[type] = result[type].concat(prepareTypeForm(data));
            break;

          case "ages":
            result[type] = result[type].concat(prepareAgesForm(data));
            break;
        }
      });

      if (result.status && result.status.length) {
        result.status = [...new Set(result.status)];
      } else {
        delete result.status;
      }

      if (result.type && result.type.length) {
        result.type = [...new Set(result.type)];
      } else {
        delete result.type;
      }

      if (result.ages && !result.ages.length) {
        delete result.ages;
      }

      this.result = result;
    }
  }
};
</script>
