<template>
  <div>
    <b-container class="py-2 bg-transparent" >
      <Product name="message" :bstats-ids="[11242]"/>
      <Product name="send" :bstats-ids="[11345]"/>
      <Product name="swap" :bstats-ids="[12549]"/>
      <Product name="broadcast"/>
      <Product name="tablist" :bstats-ids="[11443]"/>
      <Product name="execute" :bstats-ids="[11307, 11308, 11309]"/>
      <Product name="transfer"/>
    </b-container>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "IndexPage"
});
</script>
