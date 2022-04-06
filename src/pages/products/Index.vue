<template>
  <q-page padding>
    <q-card v-if="action === 'list'" flat square bordered>
      <q-item>
        <q-item-section avatar>
          <q-icon name="las la-th-list"></q-icon>
        </q-item-section>

        <q-item-section>
          <q-item-label>Products list</q-item-label>
          <q-item-label caption> Lorem ipsum dolor sit amet </q-item-label>
        </q-item-section>
      </q-item>

      <q-separator></q-separator>

      <q-table flat :rows="productsList" row-key="id"></q-table>
    </q-card>

    <q-card v-if="action === 'add'" flat square bordered>
      <q-item>
        <q-item-section avatar>
          <q-icon name="las la-file-alt"></q-icon>
        </q-item-section>

        <q-item-section>
          <q-item-label>Add new product</q-item-label>
          <q-item-label caption> Lorem ipsum dolor sit amet </q-item-label>
        </q-item-section>
      </q-item>

      <q-separator></q-separator>

      <q-card-section class="q-pa-lg">
        <q-form @submit="addProduct" novalidate class="q-gutter-sm">
          <q-input type="name" v-model="name" label="Name"> </q-input>

          <q-select v-model="typeId" :options="typeOptions" label="Type">
          </q-select>

          <div class="row q-mb-sm">
            <q-btn
              type="submit"
              label="Add"
              color="primary"
              class="full-width"
            ></q-btn>
          </div>
        </q-form>
      </q-card-section>
    </q-card>
  </q-page>

  <w-toolbar>
    <q-list>
      <q-item-label header>Actions</q-item-label>

      <q-item tag="label" to="/products/add">
        <q-item-section side>
          <q-icon name="las la-plus-circle"></q-icon>
        </q-item-section>
        <q-item-section>
          <q-item-label>Add new product</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </w-toolbar>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";
import { api } from "boot/axios";
import WToolbar from "waves/components/WToolbar.vue";

export default defineComponent({
  name: "ProductsIndex",

  components: {
    WToolbar,
  },

  setup() {
    const action = ref("list");

    const productsList = ref([]);
    const getProducts = async function () {
      await api
        .get("catalog/product")
        .then((response) => (productsList.value = response.data));
    };
    onMounted(getProducts);

    const name = ref("");
    const typeId = ref(null);

    const addProduct = async function () {
      await api
        .post("catalog/product", {
          name,
          typeId,
        })
        .then($router.push("/products"));
    };

    return {
      action,

      productsList,

      name,
      typeId,

      addProduct,
    };
  },
});
</script>
