<template>
  <q-page padding>
    <q-card flat square bordered>
      <q-item>
        <q-item-section avatar>
          <q-avatar>
            <q-icon name="inventory_2"></q-icon>
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label>Products</q-item-label>
          <q-item-label caption>
            Lorem ipsum dolor sit amet
          </q-item-label>
        </q-item-section>
      </q-item>

      <q-separator></q-separator>
      <q-table flat :rows="dataSource" row-key="id"></q-table>
    </q-card>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";
import { api } from "boot/axios";

export default defineComponent({
  setup() {
    const dataSource = ref([]);
    const getProducts = async () => {
      dataSource.value = await api
        .get("catalog/product")
        .then((response) => (dataSource.value = response.data));
    }
    onMounted(getProducts);

    return {
      dataSource
    }
  },
})
</script>
