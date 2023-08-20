<template>
  <a :href="item.url" target="_blank">
    <h4 v-html="hightlight(item.name)"></h4>
  </a>
  <h6 class="mb-3" v-html="hightlight(item.datecreated)"></h6>
  <p class="mb-4" v-html="hightlight(item.description)"></p>
  <hr />
</template>

<script>
export default {
  name: "ListItem",
  props: {
    item: {
      name: String,
      url: String,
      description: String,
      datecreated: String,
    },
    searchValue: String
  },
  methods: {
    hightlight(text) {
      if (this.searchValue.length <= 0) return text;
      return text.replace(new RegExp(this.searchValue, "gi"), (match) => {
        return "<mark>" + match + "</mark>";
      });
    },
  },
};
</script>