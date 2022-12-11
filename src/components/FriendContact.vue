<!-- Hier steht unser Template für unsere Komponente -->
<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? " **Favorite**" : "" }}</h2>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <button @click="deleteContact">Delete</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ email }}
      </li>
      <li>
        <strong>Age:</strong>
        {{ age }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  emits: ["toggle-favourite", "delete"],

  // props können als array angegeben werden
  // props: ['name','phoneNumber','emailAddress','isFavorite'],

  // props können als Objekte mit speziellen Eigenschaften angegeben werden

  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    age: {
      type: String,
      required: true,
      validator: function (value) {
        return !isNaN(value);
      },
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,

      // Es kann auch ein validator angegeben werden
      // hier wird einfach überprüft, ob '1' oder '0' übergeben wurde
    },
  },

  // created()
  // wird aufgerufen nach der Erstellung der Komponente
  // Kann für Initalisierungen verwendet werden

  data() {
    return {
      detailsAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
      console.log(this.phoneNumber);
    },
    toggleFavorite() {
      //mit $emit wird das ereignis ausgelöst
      this.$emit("toggle-favourite", this.id);
      this.isMyFavorite = !this.isMyFavorite;
    },
    deleteContact() {
      this.$emit("delete", this.id);
    },
  },
};
</script>
