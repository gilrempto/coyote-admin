<template>
  <q-page padding>
    <q-card flat square bordered>
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

      <q-item tag="label" to="/products">
        <q-item-section side>
          <q-icon name="las la-arrow-circle-left"></q-icon>
        </q-item-section>
        <q-item-section>
          <q-item-label>Back to products list</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </w-toolbar>
</template>

<script>
import { defineComponent, ref } from "vue";
import { useRouter } from "vue-router";
import { api } from "boot/axios";
import WToolbar from "waves/components/WToolbar.vue";

export default defineComponent({
  name: "ProductsAdd",

  components: {
    WToolbar,
  },

  setup() {
    const $router = useRouter();

    const name = ref("");
    const typeId = ref(null);

    const typeOptions = [
      {
        label: "Type 1",
        value: "7d9a80fc-48c2-45ef-8e38-9e502f54d7b8",
      },
      {
        label: "Type 2",
        value: "059375a7-a864-4c8e-9e91-607d7b6a8573",
      },
      {
        label: "Type 3",
        value: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      },
    ];

    const addProduct = async function () {
      await api
        .post("catalog/product", {
          name,
          typeId,
        })
        .then($router.push("/products"));
    };

    return {
      name,
      typeId,
      typeOptions,
      addProduct,
    };
  },
});
</script>
