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
                              v-if="isLogged">
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
            <form @submit.prevent="saveData"
                  novalidate>

              <md-field>
                <label>Nom complet</label>
                <md-input v-model.trim="fullname"/>
              </md-field>

              <p class="actions">
                <span class="space"></span>
                <md-button class="md-primary"
                           type="submit">
                  Ajouter
                </md-button>
              </p>
            </form>

            <md-list v-if="Object.keys(persons).length > 0">
              <md-divider/>
              <md-list-item :key="`person_${id}`"
                            v-for="(person, id) in persons">
                {{ person.fullname }}
              </md-list-item>
            </md-list>
          </md-tab>

          <md-tab md-icon="dns"
                  md-label="Déployer">

            <p>
              Simple comme utiliser ces 2 commandes :
            </p>
            <ul class="cli">
              <li>$ npm run build -- --mode local</li>
              <li>$ firebase deploy</li>
            </ul>

          </md-tab>
        </md-tabs>
      </div>
    </md-app-content>
  </md-app>
</template>

<script>
import firebase from 'firebase/app';
import 'firebase/auth';
import 'firebase/firestore';

firebase.initializeApp({
  apiKey: process.env.VUE_APP_FIREBASE_API_KEY,
  authDomain: process.env.VUE_APP_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.VUE_APP_FIREBASE_PROJECT_ID,
});
firebase.firestore()
  .settings({ timestampsInSnapshots: true });

export default {
  name: 'app',
  data() {
    return {
      isLogged: false,
      login: null,
      password: null,
      persons: {},
      fullname: null,
    };
  },
  created() {
    this.checkIfLogged();
    this.getPersons();
  },
  methods: {
    checkIfLogged() {
      firebase
        .auth()
        .onAuthStateChanged((user) => {
          console.log(user);
          this.isLogged = user !== null;
        });
    },
    signIn() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.login, this.password)
        .then(user => console.log(user))
        .catch(err => console.error(err));
    },
    signInWithGoogle() {
      firebase
        .auth()
        .signInWithPopup(new firebase.auth.GoogleAuthProvider())
        .then(user => console.log(user))
        .catch(err => console.error(err));
    },
    signOut() {
      firebase
        .auth()
        .signOut()
        .then(() => console.log('Je suis déconnecté ...'))
        .catch(err => console.error(err));
    },
    createNewAccount() {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.login, this.password)
        .then(user => console.log(user))
        .catch(err => console.error(err));
    },
    getPersons() {
      firebase
        .firestore()
        .collection('persons')
        .onSnapshot(
          (querySnapshot) => {
            const persons = {};
            querySnapshot.forEach(doc => persons[doc.id] = doc.data());
            this.persons = persons;
          },
          err => console.log(err));
    },
    saveData() {
      firebase
        .firestore()
        .collection('persons')
        .add({ fullname: this.fullname })
        .then(res => console.log(res))
        .catch(err => console.error(err));
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

      .cli {
        list-style-type: none;
        background-color: #FAFAFA;

        li {
          padding: 10px 0;
        }
      }
    }
  }
</style>
