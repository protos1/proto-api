<template>
  <div id="app">
    <my-account-panel/>
    <md-app class="s1-md-app">
      <md-app-drawer
        class="md-xsmall-hide md-small-hide"
        :md-active.sync="Settings.menuVisible"
        md-persistent="mini"
      >
        <div class="s1-logo__wrapper">
          <img class="s1-logo__img" src="https://s1vm.netlify.com/logo.svg" alt="company logo">
        </div>
        <md-list :md-expand-single="true">
          <md-list-item @click="toggleMenu">
            <md-icon v-if="!Settings.menuVisible">menu</md-icon>
            <md-icon v-if="Settings.menuVisible">keyboard_arrow_left</md-icon>
            <span class="md-list-item-text">Esconder</span>
            <md-tooltip md-direction="right" v-show="!Settings.menuVisible">Expandir menu</md-tooltip>
          </md-list-item>
          <md-list-item @click="setPage('Home')">
            <md-icon>home</md-icon>
            <span class="md-list-item-text">Home</span>
            <md-tooltip md-direction="right" v-show="!Settings.menuVisible">Home</md-tooltip>
          </md-list-item>
          <md-list-item @click="setPage('Ak')">
            <md-icon>vpn_key</md-icon>
            <span class="md-list-item-text">API Clients</span>
            <md-tooltip md-direction="right" v-show="!Settings.menuVisible">API Clients</md-tooltip>
          </md-list-item>
        </md-list>
      </md-app-drawer>
      <md-app-content class="s1-loc__body-bg s1-U__pd--tp0 s1-U__bg-color--body-bg">
        <Ak
          v-if="Page.Current === 'Ak'"
          :StoreData="StoreData"
          :Settings="Settings"
          :updateStoreData="updateStoreData"
          :setPage="setPage"
        />
      </md-app-content>
    </md-app>
  </div>
</template>

<script>
import MyAccountPanel from "./components/MyAccountPanel/index";
import Ak from "./components/Ak/Ak";

export default {
  name: "App",
  components: {
    Ak,
    MyAccountPanel
  },
  data: () => ({
    Page: {
      Current: "Ak"
    },
    StoreData: {
      Ak: []
    },
    Settings: {
      menuVisible: false,
      snackbarDuration: 3000
    }
  }),
  methods: {
    updateStoreData(entityName, data) {
      this.StoreData[entityName] = [...data];
    },
    setPage(entityName) {
      this.Page.Current = entityName;
    },
    toggleMenu() {
      this.Settings.menuVisible = !this.Settings.menuVisible;
    }
  }
};
</script>