<template>
  <form @submit.prevent="addFriend">
    <div>
      <label for="name">Name</label>
      <input type="text" v-model="name"/>
    </div>
    <div>
      <label for="phone">Phone</label>
      <input type="tel" v-model="phone"/>
    </div>
    <div>
      <label for="email">Email</label>
      <input type="email" v-model="email"/>
    </div>
    <div>
      <button type="submit">Add Friend</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      phone: "",
      email: "",
    };
  },
  methods: {
    addFriend() {
      const friend = {
        id: new Date().toISOString(),
        name: this.name,
        phone: this.phone,
        email: this.email,
        isFavorite: false,
      };
      this.$emit("add-friend", friend);
    },
  },
};
</script>
