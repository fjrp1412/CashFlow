<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume :label="label" :amount="amount" :totalAmount="totalAmount">
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
      movements: [],
    };
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));
    if (Array.isArray(movements)) {
      this.movements = movements?.map((movement) => {
        return { ...movement, time: new Date(movement.time) };
      });
    }
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
    totalAmount() {
      return this.movements.reduce((acc, curr) => acc + curr.amount, 0);
    },
  },
  methods: {
    create(payload) {
      payload.id = this.movements.length + 1;
      this.movements.push(payload);
      this.save();
    },
    remove(id) {
      this.movements = this.movements.filter((movement) => movement.id !== id);
      this.save();
    },

    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
  },
};
</script>
