<template>
  <md-app id="app">
    <md-app-toolbar md-elevation="1">
      <div class="md-toolbar-row">
        <div class="md-title">
          <img alt="logo" src="./assets/logo.png">
          <span>Basics with VueJS</span>
        </div>
      </div>
    </md-app-toolbar>

    <md-app-content>
      <div class="content">
        <md-tabs class="md-elevation-2"
                 md-alignment="fixed"
                 md-dynamic-height>
          <md-tab md-icon="verified_user"
                  md-label="S'authentifier">

          </md-tab>

          <md-tab md-icon="save"
                  md-label="Persister">

          </md-tab>

          <md-tab md-icon="dns"
                  md-label="Déployer">

          </md-tab>
        </md-tabs>
      </div>
    </md-app-content>
  </md-app>
</template>

<script>
export default {
  name: 'app',
};
</script>

<style lang="scss">
  #app {
    height: 100%;

    .md-title {
      display: grid;
      grid-column-gap: 20px;

      span,
      img {
        grid-row: 1;
        align-self: center;
      }

      img {
        height: 30px;
        max-width: 100%;
      }
    }

    .content {
      width: 600px;
      margin: auto;
    }
  }
</style>
