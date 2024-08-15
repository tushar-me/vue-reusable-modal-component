<h1>Vue3 Reusable Modal Component</h1>

`src/components/Modal.vue`

```javascript
<script setup>
    import { defineProps, defineEmits, ref } from "vue";
    const props = defineProps({
        isOpen: Boolean,
        title:String,
    });
    const emit = defineEmits(["modal-close"]);
</script>
<template>
    <div v-if="isOpen" class="fixed top-0 left-0 bottom-0 right-0 z-50 bg-black bg-opacity-60 w-full h-screen flex items-center justify-center">
        <div class="w-full max-w-xl min-h-28 bg-white p-4 shadow-lg z-[99999]">
            <div class="flex items-center justify-between">
                <h3 class="font-medium text-lg">{{ title }}</h3>
                <button class="" @click.stop="emit('modal-close')">
                    <Icon name="material-symbols:close" class="text-primary text-3xl" />
                </button>
            </div>
            <div>
                <slot></slot>
            </div>
        </div>
    </div>
</template>
```




### Use Modal Component in Parent Component
`src/views/Index.vue`

```javascript
<script setup>
    import Modal from '@/components/Modal.vue';

    const isModalOpened = ref(false);
    const openModal = () => {
      isModalOpened.value = true;
    };
    const closeModal = () => {
      isModalOpened.value = false;
    };
</script>

<template>
    <section>
        //modal open button
        <button  @click="openModal">
            Open Modal
        </button>
        
        // modal
        <Modal title="Modal Title" :isOpen="isModalOpened" @modal-close="closeModal">
            <div>
                <h3>Your Design</h3>
            <div>
        </Modal>
    </section>
</template>
```
