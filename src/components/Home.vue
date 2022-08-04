<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume :label="label" :amount="amount" :totalAmount="100000">
        <template #graphic>
          <Graphic :amounts="amounts" />
        </template>
        <template #action>
          <Action />
        </template>
      </Resume>
    </template>

    <template #movements>
      <Movements :movements="movements" />
    </template>
  </Layout>
</template>

<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from "@/components/Resume/Index.vue";
import Movements from "@/components/Movements/Movements.vue";
import Action from "@/components/Action.vue";
import Graphic from "@/components/Resume/Graphic.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
    Action,
    Graphic,
  },

  data() {
    return {
      amount: null,
      label: null,
      movements: [
        {
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 1000,
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 500,
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: -100,
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: -1000,
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: -1000,
        },
      ],
    };
  },
  computed: {
    amounts() {
      return this.movements.map((movement) => movement.amount);
    },
  },
};
</script>
