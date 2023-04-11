<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toggleIsFavorite">{{ isFavorite ? 'Unfavorite' : 'Favorite' }}</button>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <button @click="$emit('delete',id)">Delete</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  props:{
    id:{
      type: String,
      required: true
    },
    name:{
      type: String,
      required: true
    },
    phoneNumber:{
      type: String,
      required: true
    },
    emailAddress:{
      type: String,
      required: true
    },
    isFavorite:{
      type: Boolean,
      required: true,
      // default: false
    }
  },
  emits: {
    'toggle-favorite': function(id) {
      if(id){
        return true;
      } else {
        console.warn('Id is required to toggle favorite status.');
        return false;
      }
    },
    'delete': function(id) {
      if(id){
        return true;
      } else {
        console.warn('Id is required to delete friend.');
        return false;
      }
    }
  },
  data() {
    return {
      detailsAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleIsFavorite() {
      // this.isFriendFavorite = !this.isFriendFavorite;
      this.$emit('toggle-favorite',this.id);
    }
  }
};
</script>