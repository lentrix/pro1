<template>

    <div class="bg-white p-6 rounded shadow-sm cursor-pointer flex flex-col">
        <div class="flex-1" @click="openItem">
            <img :src="item.picUrl" alt="Product photo" class="aspect-square w-full object-cover mb-4">
            <h4 class="text-2xl">Item: {{ item?.name }}</h4>
            <div class="text-gray-400">{{ item?.description }}</div>
        </div>
        <div class="flex justify-between">
            <div>&nbsp;</div>
            <label :for="'status-' + item.id" class="switch">
                Enabled
                <input type="checkbox" :id="'status-' + item.id" :checked="item.enabled" @change="toggleEnabled(item)">
                <span class="slider"></span>
            </label>
        </div>
    </div>

</template>

<style scoped>

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}


input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

</style>

<script setup>
import { router } from '@inertiajs/vue3';


const prop = defineProps({
    item: Object
})

function openItem() {
    router.visit('/items/' + prop.item.id)
}

function toggleEnabled(item) {
    router.visit('/items/toggle/' + item.id,{
        method: 'post',
        preserveScroll: true
    })
}

</script>
