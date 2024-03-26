<template>
  <div class="content">
    <span class="header"> {{ item.name }}</span>

    <div class="detail" v-for="attr in props.item.attributes" :key="attr.id">
      <div class="field">
        <span class="title">code:</span>
        <input v-model="attr.code" />
      </div>

      <div class="field">
        <span class="title">name:</span>
        <input v-model="attr.name" />
      </div>

      <div v-if="attr.color" class="field">
        <span class="title">color:</span>
        <input v-model="attr.color" />
      </div>

      <div v-if="attr.size" class="field">
        <span class="title">size:</span>
        <span>
          <input v-model="attr.size.width" type="number" /> x
          <input v-model="attr.size.height" type="number" />
        </span>
      </div>

      <div v-if="attr.weight !== undefined" class="field">
        <span class="title">weight:</span>
        <input v-model="attr.weight" type="number" />
      </div>
    </div>

    <div class="add">
      <label>
        type
        <select ref="selectRef">
          <option value="color">color</option>
          <option value="size">size</option>
          <option value="weight">weight</option>
        </select>
      </label>

      <button @click="emit('click', selectRef.value)">Add</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, ref } from "vue";

const props = defineProps<{
  item: {
    id: number;
    name: string;
    attributes: {
      code: string;
      name: string;
    };
  };
}>();

const emit = defineEmits(["click"]);

const selectRef = ref<HTMLSelectElement>();
</script>

<style scoped lang="css">
.header {
  font-weight: bold;
}
.content {
  display: flex;
  flex-direction: column;
  padding: 20px;
  gap: 20px;
}
.detail {
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.field {
  display: flex;
  gap: 5px;
}
.title {
  font-weight: bold;
}
.add {
  display: flex;
  gap: 10px;
}
</style>
