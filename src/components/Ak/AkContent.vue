<template>
  <section class="s1-U__width--900px" style="margin: 0 auto;">
    <!-- MAIN TITLE -->
    <div class="s1-U__pd--bt32 s1-U__pd--tp32">
      <h1 class="md-display-1">API Clients</h1>
    </div>

    <!-- NO Ak DATA -->
    <article class="s1-U__text-align--center s1-U__pd32" v-if="StoreData.Ak.length === 0">
      <p class="md-body-2 s1-U__mg--bt16 s1-U__text-color--dark-2">No registered API clients</p>
      <md-button class="md-raised md-primary" @click="create('Ak', 'Ak-Name')">
        <div class="s1-U__align-children--center s1-U__pd--rt8 s1-U__pd--lt4">
          <md-icon class="s1-U__mg--rt4">add</md-icon>
          <span>API Client</span>
        </div>
      </md-button>
    </article>

    <!-- LIST -->
    <article v-if="StoreData.Ak.length > 0">
      <header
        class="s1-U__align-children--center s1-U__mg--bt16 s1-U__justify-content--space-between"
      >
        <md-button class="s1-md-bordered s1-U__mg--bt16 s1-U__invisible">
          <div class="s1-U__align-children--center">
            <md-icon>filter_list</md-icon>
            <span>filtros</span>
          </div>
        </md-button>
        <md-button class="md-raised md-primary s1-U__mg--bt16" @click="create('Ak', 'Ak-Name')">
          <div class="s1-U__align-children--center">
            <md-icon>add</md-icon>
            <span class="s1-U__pd--rt8">API Client</span>
          </div>
        </md-button>
      </header>
      <md-table md-card>
        <md-table-row>
          <md-table-head>Name</md-table-head>
          <md-table-head>APIs</md-table-head>
          <md-table-head></md-table-head>
        </md-table-row>
        <md-table-row v-for="Ak in StoreData.Ak" :key="Ak.Id">
          <md-table-cell class="s1-U__pd--tp16" valign="top">
            <div class>
              <h4>{{Ak.Name}}</h4>
            </div>
          </md-table-cell>
          <md-table-cell valign="top">
            <!-- <p>
              <span
                v-for="(ak, index) in Ak.Apis"
                :key="ak"
              >{{index === Ak.Apis.length - 1 ? `${getNameById(Apis, ak)}` : `${getNameById(Apis, ak)}; `}}</span>
            </p>-->
            <ul class="s1-U__pd--lt16">
              <li class="s1-U__mg0" v-for="ak in Ak.Apis" :key="ak">{{getNameById(Apis, ak)}}</li>
            </ul>
          </md-table-cell>
          <md-table-cell md-numeric valign="top">
            <md-menu md-direction="bottom-end">
              <md-button class="md-icon-button" md-menu-trigger>
                <md-icon>more_vert</md-icon>
              </md-button>

              <md-menu-content class="s1-U__width--180px">
                <md-menu-item class="s1-U__border--bottom1">
                  <h4>{{Ak.Name}}</h4>
                </md-menu-item>
                <md-menu-item @click="detail('Ak', Ak)">Details</md-menu-item>
                <md-menu-item @click="edit('Ak', Ak.Id, 'Ak-Name')">Edit</md-menu-item>
                <md-divider></md-divider>
                <md-menu-item @click="remove('Ak', Ak.Id, 'Name', 'API client')">Delete</md-menu-item>
              </md-menu-content>
            </md-menu>
          </md-table-cell>
        </md-table-row>
      </md-table>
    </article>
  </section>
</template>

<script>
import Apis from "../../data/Apis.js";

export default {
  name: "AkContent",
  data: () => ({
    Apis
  }),
  props: {
    Ak: Object,
    StoreData: Object,
    create: Function,
    edit: Function,
    remove: Function,
    detail: Function
  }
};
</script>