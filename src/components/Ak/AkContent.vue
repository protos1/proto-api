<template>
  <section class="s1-U__width--900px" style="margin: 0 auto;">
    <!-- MAIN TITLE -->
    <div class="s1-U__mg--bt32 s1-U__mg--tp32">
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
        <md-button class="s1-md-bordered s1-U__mg--bt16">
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
          <md-table-cell>
            <h4>{{Ak.Name}}</h4>
          </md-table-cell>
          <md-table-cell>
            <p>
              <span
                v-for="(ak, index) in Ak.Apis"
                :key="ak"
              >{{index === Ak.Apis.length - 1 ? `${getNameById(Apis, ak)}` : `${getNameById(Apis, ak)}; `}}</span>
            </p>
          </md-table-cell>
          <md-table-cell md-numeric>
            <md-button class="md-icon-button" @click="remove('Ak', Ak.Id, 'Name', 'API client')">
              <md-icon>delete</md-icon>
            </md-button>
            <md-button class="md-icon-button" @click="edit('Ak', Ak.Id, 'Ak-Name')">
              <md-icon>edit</md-icon>
            </md-button>
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
    remove: Function
  }
};
</script>