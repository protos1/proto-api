<template>
  <div id="Ak">
    <!-- MOCK -->
    <div class="s1-prop__auto-gen">
      <md-button class="md-primary md-icon-button squared" @click="setMockData('Ak');">
        <md-icon>person</md-icon>
      </md-button>
    </div>

    <!-- GENERAL LOADING -->
    <div
      class="md-layout md-alignment-center-center s1-loc__loading s1-loc__above-all"
      :class="Ak.Loading && 'active'"
    >
      <md-progress-spinner md-mode="indeterminate"></md-progress-spinner>
    </div>

    <!-- CONTENT -->
    <Ak-content
      :StoreData="StoreData"
      :Ak="Ak"
      :create="create"
      :edit="edit"
      :remove="remove"
      v-if="!Ak.CreatingInterface && !Ak.EditingInterface"
    />

    <!-- DETAILS -->
    <section class="s1-U__width--900px" style="margin: 0 auto;" v-if="Ak.DetailInterface"></section>

    <!-- CREATING -->
    <Ak-creating
      :StoreData="StoreData"
      :Ak="Ak"
      :$v="$v"
      :saveCreated="saveCreated"
      :discardCreating="discardCreating"
      v-if="Ak.CreatingInterface"
      :genFields="genFields"
      :updateScope="updateScope"
    />

    <!-- EDITING -->
    <Ak-editing
      :StoreData="StoreData"
      :Ak="Ak"
      :$v="$v"
      :saveEdited="saveEdited"
      :discardEditing="discardEditing"
      v-if="Ak.EditingInterface"
      :updateScope="updateScope"
    />

    <!-- DELETE -->
    <md-dialog-confirm
      :md-active.sync="Ak.DeleteConfirmation"
      :md-title="Ak.DeleteInfo.Title"
      :md-content="Ak.DeleteInfo.Content"
      md-confirm-text="delete"
      md-cancel-text="back"
      @md-cancel="Ak.DeleteConfirmation = false"
      @md-confirm="removeItem('Ak', Ak.DeleteInfo.Id)"
    />

    <!-- CREATE FEEDBACK -->
    <md-snackbar
      :md-duration="Settings.snackbarDuration"
      :md-active.sync="Ak.SuccessFeedbackCreating"
      md-persistent
    >
      <span>API Client created successfully</span>
      <md-button class="md-accent" @click="Ak.SuccessFeedbackCreating = false">OK</md-button>
    </md-snackbar>

    <!-- EDIT FEEDBACK -->
    <md-snackbar
      :md-duration="Settings.snackbarDuration"
      :md-active.sync="Ak.SuccessFeedbackEditing"
      md-persistent
    >
      <span>API Client edited successfully</span>
      <md-button class="md-accent" @click="Ak.SuccessFeedbackEditing = false">OK</md-button>
    </md-snackbar>

    <!-- DELETE  FEEDBACK -->
    <md-snackbar
      :md-duration="Settings.snackbarDuration"
      :md-active.sync="Ak.SuccessFeedbackDeletion"
      md-persistent
    >
      <span>API Client deleted successfully</span>
      <md-button class="md-accent" @click="Ak.SuccessFeedbackDeletion = false">OK</md-button>
    </md-snackbar>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
import EntityBase from "../EntityBase";

import Aks from "../../data/Aks.js";
import Apis from "../../data/Apis.js";

import AkContent from "./AkContent.vue";
import AkCreating from "./AkCreating.vue";
import AkEditing from "./AkEditing.vue";
import { getPropById, randomString } from "../../assets/utils";

export default {
  name: "Ak",
  extends: EntityBase,
  props: {
    StoreData: Object,
    Settings: Object,
    updateStoreData: Function,
    setPage: Function
  },
  components: {
    AkContent,
    AkCreating,
    AkEditing
  },
  data: () => ({
    Ak: {
      Form: {
        Id: null,
        Name: null,
        ClientId: null,
        ClientSecret: null,
        Apis: [],
        GrantType: "client_credentials",
        TokenEndpoint: "https://authaplha.solutionsone.com.br/connect/token",
        Scopes: "No API selected",
        Description: null
      },
      DefaultForm: {
        Id: null,
        Name: null,
        ClientId: null,
        ClientSecret: null,
        Apis: [],
        GrantType: "client_credentials",
        TokenEndpoint: "https://authaplha.solutionsone.com.br/connect/token",
        Scopes: "No API selected",
        Description: null
      },
      Data: [],
      MockData: Aks,
      Loading: false,
      CreatingFormLoading: false,
      EditingFormLoading: false,
      EditingInterface: false,
      DiscardEditingInterface: false,
      SuccessFeedbackEditing: false,
      CreatingInterface: false,
      DiscardCreatingInterface: false,
      SuccessFeedbackCreating: false,
      DeleteConfirmation: false,
      SuccessFeedbackDeletion: false,
      DeleteInfo: {
        Id: null,
        Title: null,
        Content: null
      }
    }
  }),
  methods: {
    reducer(accumulator, currentValue) {
      return accumulator + "+" + currentValue;
    },
    setScope() {
      if (this.Ak.Form.Apis.length > 0) {
        this.Ak.Form.Scopes = this.Ak.Form.Apis.map(item => {
          return getPropById(Apis, item, "Scope");
        }).reduce(this.reducer);
      } else {
        this.Ak.Form.Scopes = this.Ak.DefaultForm.Scopes;
      }
    },
    genFields() {
      this.Ak.Form.ClientId = randomString(20, "#aA");
      this.Ak.Form.ClientSecret = randomString(20, "#aA");
    },
    updateScope() {
      if (this.Ak.CreatingInterface || this.Ak.EditingInterface)
        this.setScope();
    }
  },
  mounted() {
    this.Ak.Data = [...this.StoreData.Ak];
  },
  validations: {
    Ak: {
      Form: {
        Name: {
          required
        },
        Apis: {
          required
        }
      }
    }
  }
};
</script>
