<template>
  <v-col>
    <v-btn class="mr-2" :disabled="areAllSelected" @click="selectAll">
      All
    </v-btn>
    <v-btn :disabled="!areAnySelected" @click="clearAll">None</v-btn>

    <v-checkbox
      v-for="(tag, idx) in tags"
      :key="idx"
      v-model="selectedTags"
      :label="tag"
      :color="tag"
      :value="tag"
      @click="tagsChanged"
    />
  </v-col>
</template>

<script>
export default {
  name: "TagChooser",

  props: {
    // All possible tags
    tags: {
      type: Array,
      required: true,
    },
  },

  data() {
    return {
      // Currently-selected tags. This array is the model for the all
      // check boxes. When one is checked its value (tag) will be added
      // to this array. When unchecked, its value will be removed.
      selectedTags: [],
    };
  },

  computed: {
    // Are all available tags selected? Used to enable/disable "All" button.
    areAllSelected() {
      return this.selectedTags.length === this.tags.length;
    },

    // Are any tags selected? Used to enable/disable "None" button.
    areAnySelected() {
      return this.selectedTags.length > 0;
    },
  },

  methods: {
    // A check box has changed state. Let any listeners know.
    tagsChanged() {
      this.$emit("tagsUpdated", this.selectedTags);
    },

    // Select all the tags and notify listeners.
    selectAll() {
      this.selectedTags = this.tags;
      this.tagsChanged();
    },

    // Deselect all the tags and notify listeners.
    clearAll() {
      this.selectedTags = [];
      this.tagsChanged();
    },
  },
};
</script>
