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
          <Action @create="create" />
        </template>
      </Resume>
    </template>

    <template #movements>
      <Movements :movements="movements" @remove="remove" />
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
          amount: 100,
          time: new Date("08-04-2022"),
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 200,
          time: new Date("08-04-2022"),
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: 500,
          time: new Date("08-04-2022"),
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 200,
          time: new Date("08-04-2022"),
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: -400,
          time: new Date("08-04-2022"),
        },
        {
          id: 6,
          title: "Movimiento 6",
          description: "Reparación equipo",
          amount: -600,
          time: new Date("08-04-2022"),
        },
        {
          id: 7,
          title: "Movimiento 7",
          description: "Reparación equipo",
          amount: -300,
          time: new Date("08-04-2022"),
        },
        {
          id: 8,
          title: "Movimiento 8",
          description: "Reparación equipo",
          amount: 0,
          time: new Date("08-04-2022"),
        },
        {
          id: 9,
          title: "Movimiento 9",
          description: "Reparación equipo",
          amount: 300,
          time: new Date("07-04-2022"),
        },
        {
          id: 10,
          title: "Movimiento 10",
          description: "Reparación equipo",
          amount: 500,
          time: new Date("07-04-2022"),
        },
      ],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((mov) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return mov.time >= oldDate;
        })
        .map((movement) => movement.amount);

      return lastDays.map((movement, idx) => {
        const lastMovements = lastDays.slice(0, idx);

        return lastMovements.reduce((sum, movement) => {
          return sum + movement;
        }, 0);
      });
    },
  },
  methods: {
    create(payload) {
      payload.id = this.movements.length + 1;
      this.movements.push(payload);
    },
    remove(id) {
      this.movements = this.movements.filter((movement) => movement.id !== id);
    },
  },
};
</script>
