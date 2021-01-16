<template>
  <v-card v-show="isSelected">
    <v-card-title>Color Card #{{ id }}</v-card-title>
    <v-card-text :class="`${color}--text`">
      My color is {{ color }}.
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "ColorCard",
  props: {
    id: { type: Number, required: true },
    color: { type: String, required: true },
    selectedTags: { type: Array, required: true },
  },

  computed: {
    // This function will be triggered reactively whenever the list of selected tags
    // changes, causing the card to reevaluate whether it's shown or not.
    isSelected() {
      return this.selectedTags.includes(this.color);
    },
  },
};
</script>
