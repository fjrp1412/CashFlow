<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume :label="label" :amount="amount" :totalAmount="100000">
        <template #graphic>Graphic</template>
        <template #action>Action</template>
      </Resume>
    </template>

    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>

<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from "@/components/Resume/Index.vue";
import Movements from "@/components/Movements.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
  },

  data() {
    return {
      amount: null,
      label: null,
    };
  },
};
</script>
