<template>
  <v-container>
    <v-row>
      <v-col cols="3">
        <h3>Tags</h3>
        <TagChooser :tags="availableTags" @tagsUpdated="onTagsUpdated" />
      </v-col>
      <v-col cols="9">
        <h3>Cards</h3>
        <ColorCard
          v-for="(card, idx) in allCards"
          :key="idx"
          :id="card.id"
          :color="card.tag"
          :selectedTags="selectedTags"
        />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ColorCard from "@/components/ColorCard";
import TagChooser from "@/components/TagChooser";
import * as _ from "lodash";

import Chance from "chance";
const chance = new Chance();

export default {
  name: "Workbench",

  components: {
    TagChooser,
    ColorCard,
  },

  data() {
    return {
      allCards: [], // All card data; normally fetched from API
      availableTags: [], // All tags for tag chooser
      selectedTags: [], // Tags that are currently selected
    };
  },

  methods: {
    // A tag has been selected or deselected in the TagChooser. The event argument
    // is the new list of selected tags. Update our local version of that list,
    // which will update the `selectedTags` in all of the cards. They will respond
    // by showing/hiding themselves.
    onTagsUpdated(event) {
      this.selectedTags = event;
    },
  },

  // Fake up some cards. Normally, the data would come from the API.
  mounted() {
    this.availableTags = [
      "red",
      "orange",
      "yellow",
      "green",
      "blue",
      "indigo",
      "purple",
    ];
    this.allCards = _.times(42, (n) => ({
      id: n,
      tag: chance.pickone(this.availableTags),
    }));
  },
};
</script>
