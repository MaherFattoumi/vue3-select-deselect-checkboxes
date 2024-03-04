<script>
import { ref, watchEffect } from 'vue';

export default {
  setup() {
    const items = ref([
	  { name : 'Mohamed Fattoumi', checked: false },
      { name : 'Kamel Fattoumi', checked: false },
      { name : 'Rochdi Fattoumi', checked: false },
      { name : 'Hichem Fattoumi', checked: false },
      // Add more items as needed
    ]);
	const allSelectLabel = ref('Tout Séléctionner');
    const master = ref(false);

    const toggleAll = () => {
      items.value.forEach(item => {
        item.checked = master.value;
      });
    };

    const checkAll = () => {
      master.value = items.value.every(item => item.checked);
    };

    watchEffect(() => {
      master.value = items.value.every(item => item.checked);
    });

    return { items, master, toggleAll, checkAll };
  },
};
</script>

<template>
  <div>
    <input type="checkbox" v-model="master" @change="toggleAll" /> Tout Séléctionner
    <div v-for="(item, index) in items" :key="index">
      <input type="checkbox" v-model="item.checked" @change="checkAll" /> {{ item.name }}
    </div>
  </div>
</template>
