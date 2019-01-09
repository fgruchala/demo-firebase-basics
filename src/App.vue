<template>
  <md-app id="app">
    <md-app-toolbar md-elevation="1">
      <div class="md-toolbar-row">
        <div class="md-toolbar-section-start">
          <img alt="logo" src="./assets/logo.png">
        </div>
        <div class="md-toolbar-section-end">
          <div class="md-title">Basics</div>
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

            <form @submit.prevent="signIn"
                  novalidate>

              <md-field>
                <label>Identifiant</label>
                <md-input autofocus
                          v-model.trim="login"/>
              </md-field>
              <md-field>
                <label>Mot de passe</label>
                <md-input type="password"
                          v-model.trim="password"/>
              </md-field>

              <p class="actions">
                <md-button @click="signInWithGoogle"
                           class="md-icon-button">
                  <img src="./assets/logo-btn-google.svg"/>
                </md-button>
                <span class="space"></span>
                <md-button @click="createNewAccount">Créer un nouveau compte</md-button>
                <md-button class="md-primary"
                           type="submit">
                  Se connecter
                </md-button>
              </p>
            </form>

            <p class="results">
              <md-empty-state :md-size="350"
                              class="is-logged"
                              md-icon="lock_open"
                              md-label="Authentifié"
                              md-rounded
                              v-if="!isLogged">
                <md-button @click="signOut">Se déconnecter</md-button>
              </md-empty-state>

              <md-empty-state :md-size="350"
                              class="is-not-logged"
                              md-icon="lock"
                              md-label="Non authentifié"
                              md-rounded
                              v-else/>
            </p>

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
  data() {
    return {
      isLogged: false,
      login: null,
      password: null,
    };
  },
  created() {
    // TODO check if user is logged
  },
  methods: {
    signIn() {
      // TODO authenticate with login/password
    },
    signInWithGoogle() {
      // TODO authenticate with Google SSO
    },
    signOut() {
      // TODO sign out
    },
    createNewAccount() {
      // TODO create new account with login/password
    },
  },
};
</script>

<style lang="scss">
  #app {
    height: 100%;

    .md-toolbar {
      img {
        height: 30px;
        max-width: 100%;
      }
    }

    .content {
      width: 600px;
      margin: auto;

      .actions {
        display: flex;
        align-items: center;

        .space {
          flex: 1;
        }
      }

      .results {
        text-align: center;

        .is-logged {
          background-color: rgba(76, 175, 80, 0.06);

          &,
          .md-icon {
            color: rgb(76, 175, 80);
          }
        }

        .is-not-logged {
          background-color: rgba(244, 67, 54, 0.06);

          &,
          .md-icon {
            color: rgb(244, 67, 54);
          }
        }
      }
    }
  }
</style>
