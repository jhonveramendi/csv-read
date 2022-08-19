<template>
  <div>
    <input type="file" @change="getCsv" />
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  props: {
    modelValue: {
      type: String,
    },
  },
  setup(props, { emit }) {
    const csv = ref(null);

    const getCsv = function (e) {
      const file = e.target.files[0];
      const reader = new FileReader();
      reader.onload = function (e) {
        csv.value = e.target.result;
        emit('update:modelValue', csv.value)
      };
      reader.readAsText(file);
    };
    return { getCsv, csv };
  },
};
</script>

<style></style>
