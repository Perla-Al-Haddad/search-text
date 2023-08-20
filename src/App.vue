<script setup>
</script>

<template>
  <main>
    <h2 class="mb-4">Search</h2>
    <div class="input-group mb-3">
      <input
        v-model="searchValue"
        type="text"
        class="form-control"
        placeholder="What are you looking for"
        aria-label="What are you looking for"
        aria-describedby="button-addon2"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
      >
        <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      </button>
    </div>
    <p class="mb-5">
      <strong v-if="numberOfPosts">{{ numberOfPosts }} posts</strong
      ><span v-else>No posts were</span> found.
    </p>

    <div class="col col-lg-8">
      <div v-for="(item, index) in itemsList" :key="index" class="mb-5">
        <ListItem :searchValue="searchValue" :item="item"/>
      </div>
    </div>
  </main>
</template>

<script>
import ListItem from "./components/ListItem.vue";

export default {
  components: { ListItem },
  data() {
    const items = [
      {
        name: "W3C advances technology to streamline payment authentication",
        description: `Secure Payment Confirmation (SPC), published as W3C Candidate
          Recommendation, is feature-complete and ready for further
          implementations.`,
        url: "https://www.w3.org/press-releases/2023/spc-cr/",
        datecreated: "15 June 2023",
      },
      {
        name: "EPUB 3.3 becomes a W3C Recommendation",
        description: `EPUB 3.3 becomes a W3C Recommendation`,
        url: "https://www.w3.org/press-releases/2023/epub33-rec/",
        datecreated: "25 May 2023",
      },
      {
        name: "World Wide Web Consortium seeking next CEO",
        description: "World Wide Web Consortium seeking next CEO",
        url: "https://www.w3.org/press-releases/2023/w3c-ceo-search/",
        datecreated: "21 April 2023",
      },
      {
        name: "W3C re-launched as a public-interest non-profit organization",
        description:
          "W3C re-launched as a public-interest non-profit organization",
        url: "https://www.w3.org/press-releases/2023/w3c-le-launched/",
        datecreated: "31 January 2023",
      },
      {
        name: "Decentralized Identifiers (DIDs) v1.0 becomes a W3C Recommendation",
        description:
          "A new tool to empower everyone on the web with privacy-respecting online identity and consent-based data sharing",
        url: "https://www.w3.org/press-releases/2022/did-rec/",
        datecreated: "19 July 2022",
      },
    ];
    return {
      searchValue: "",
      items: items,
      numberOfPosts: items.length,
    };
  },
  computed: {
    itemsList() {
      const cleanSearchValue = this.searchValue.trim().toLowerCase();
      if (cleanSearchValue.length > 0) {
        const filteredItems = this.items.filter(
          (item) =>
            item.name.toLowerCase().includes(cleanSearchValue) ||
            item.description.toLowerCase().includes(cleanSearchValue) ||
            item.datecreated.toLowerCase().includes(cleanSearchValue)
        );
        this.numberOfPosts = filteredItems.length;
        return filteredItems;
      }
      this.numberOfPosts = this.items.length;
      return this.items;
    },
  },
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
