<template>
  <b-navbar toggleable="lg" type="dark" variant="dark">
    <b-navbar-brand>
      <img src="https://avatars.githubusercontent.com/u/81993477" alt="" height="32" width="32" class="rounded-lg" />
      <b-dropdown split-to="/" split text="OskarsMC Plugins" class="m-2" variant="outline-primary">
        <b-dropdown-item href="https://oskarsmc.com/">OskarsMC</b-dropdown-item>
        <b-dropdown-item href="https://software.oskarsmc.com/">OskarsMC Software</b-dropdown-item>
        <b-dropdown-item href="https://quantum.oskarsmc.com/">OskarsMC Quantum</b-dropdown-item>
      </b-dropdown>
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav class="ml-auto">
        <b-dropdown right variant="outline-info" text="Socials" class="m-2">
          <b-dropdown-item href="https://github.com/OskarsMC-Plugins" target="_blank">
            <b-img class="rounded-lg" height="30"
                   src="https://img.shields.io/github/stars/oskarsmc-plugins?color=pink&label=github&logo=github&logoColor=pink&style=for-the-badge" />
          </b-dropdown-item>
          <b-dropdown-item href="https://twitter.com/oskarsmcnetwork/" target="_blank">
            <b-img class="rounded-lg" height="30"
                   src="https://img.shields.io/twitter/follow/oskarsmcnetwork?color=pink&label=twitter&logo=twitter&logoColor=pink&style=for-the-badge" />
          </b-dropdown-item>
          <b-dropdown-item href="https://discord.oskarmc.com/" target="_blank">
            <b-img class="rounded-lg" height="30"
                   src="https://img.shields.io/discord/840618521611337759?color=pink&label=Discord&logo=discord&logoColor=pink&style=for-the-badge" />
          </b-dropdown-item>
        </b-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>

</template>

<script>
export default {
  name: "Navbar"
};
</script>

<style scoped>

</style>
