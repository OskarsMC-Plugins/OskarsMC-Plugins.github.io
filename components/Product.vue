<template>
  <div class="rounded-lg oskarsmc-product py-2">
    <b-card bg-variant="dark">
      <b-media>
        <h5 class="mt-0">{{ name }}</h5>
        <p>
          {{ description }}
        </p>
        <client-only>
          <hr>
          <ul class="oskarsmc-product-info-list list-group list-group-horizontal">
            <li>
              <b-link target="_blank" :href="stargazersUrl">
                <b-icon-star />
                {{ stars }} Stars
              </b-link>
            </li>
            <li v-if="servers !== undefined">
              <b-link target="_blank" :href="bstatsUrl">
                <b-icon-server />
                {{ servers }} Servers
              </b-link>
            </li>
            <li v-if="servers !== undefined">
              <b-link target="_blank" :href="bstatsUrl">
                <b-icon-person />
                {{ players }} Players
              </b-link>
            </li>
          </ul>
        </client-only>
        <hr>
        <b-button target="_blank" :href="releasesUrl" variant="outline-success">
          <b-icon icon="download" />
          Download
        </b-button>
        <b-dropdown class="other-dropdown float-right" text="Other" variant="outline-warning">
          <b-dropdown-item target="_blank" :href="repositoryUrl">Source Code
          </b-dropdown-item>
        </b-dropdown>
      </b-media>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Product",
  props: {
    name: {
      type: String
    },
    bstatsIds: {
      type: Array[Number],
      default: () => []
    },
    defaultDescription: {
      type: String,
      default: () => ""
    }
  },
  computed: {
    repositoryNamespace() {
      return `OskarsMC-Plugins/${this.name}`;
    },
    repositoryUrl() {
      return `https://github.com/${this.repositoryNamespace}`;
    },
    releasesUrl() {
      return `${this.repositoryUrl}/releases/`;
    },
    stargazersUrl() {
      return `${this.repositoryUrl}/stargazers/`;
    },
    bstatsUrl() {
      let bstatsId = -1;
      if (this.bstatsIds.length > 0) {
        bstatsId = this.bstatsIds[0]
      }

      return `https://bstats.org/plugin/*/*/${bstatsId}`
    }
  },
  data() {
    return {
      githubResponse: Object,
      description: String,
      stars: Number,
      servers: Number,
      players: Number
    };
  },
  created() {
    // Defaults
    this.description = this.defaultDescription;
    this.stars = 0;
    this.servers = undefined;
    this.players = undefined;

    // Github request
    axios.get(`https://api.github.com/repos/${this.repositoryNamespace}`)
      .then(response => this.githubResponse = response.data)
      .finally(() => {
        this.description = this.githubResponse["description"];
        this.stars = this.githubResponse["stargazers_count"];
      })
      .catch((error) => {
        let message = typeof error.response !== "undefined" ? error.response.data.message : error.message;
        console.warn(message);
      });

    // BStats requests
    this.bstatsIds.forEach((pluginId) => {
      const bstatsBaseUrl = `https://bstats.org/api/v1/plugins/${pluginId}/charts`;

      // Servers
      axios.get(`${bstatsBaseUrl}/servers/data/?maxElements=1`)
        .then((result) => {
          if (this.servers === undefined) {
            this.servers = 0
          }
          this.servers += result.data[0][1];
        });

      // Players
      axios.get(`${bstatsBaseUrl}/players/data/?maxElements=1`)
        .then((result) => {
          if (this.players === undefined) {
            this.players = 0
          }
          this.players += result.data[0][1];
        });
    });
  }
};
</script>

<style scoped>
.oskarsmc-product {
  color: white;
}

.oskarsmc-product-info-list {
  font-size: 15px;
  padding: 0;
}

.oskarsmc-product-info-list li {
  list-style-type: none;
  padding: 0 10px;
}

.oskarsmc-product-info-list li a {
  text-decoration: none;
  color: gray;
  transition: color 100ms ease-in-out 0s;
}


.oskarsmc-product-info-list li a:hover {
  color: lightgray;
}
</style>
