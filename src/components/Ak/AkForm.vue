<template>
  <div>
    <div class="s1-loc__md-field-wrapper s1-U__width--180px">
      <md-field
        :class="{'md-invalid md-field-helper-text': $v.Ak.Form.Name.$dirty && $v.Ak.Form.Name.$invalid}"
      >
        <label for="Ak-Name">Client Name</label>
        <md-input
          id="Ak-Name"
          name="Ak-Name"
          type="text"
          @blur="$v.Ak.Form.Name.$touch()"
          @focus="$v.Ak.Form.Name.$reset()"
          v-model="Ak.Form.Name"
          required
        ></md-input>
        <span class="md-error" v-if="!$v.Ak.Form.Name.required">Required field</span>
      </md-field>
    </div>
    <div class="s1-U__mg--tp16 s1-U__mg--bt24">
      <p class="s1-U__text-color--dark-2 s1-U__mg--bt8">APIs *</p>
      <md-checkbox
        class="s1-U__mg0 s1-U__mg--rt64"
        v-for="a in Apis"
        :key="a.Id"
        v-model="Ak.Form.Apis"
        :value="a.Id"
        @change="updateScope()"
      >{{a.Name}}</md-checkbox>
    </div>
    <div class="s1-loc__md-field-wrapper s1-U__align-children--center s1-U__width--300px">
      <md-field>
        <label for="Ak-ClientId">ClientId</label>
        <md-input
          id="Ak-ClientId"
          name="Ak-ClientId"
          type="text"
          v-model="Ak.Form.ClientId"
          disabled
        ></md-input>
      </md-field>
      <md-button
        class="md-icon-button squared s1-U__mg--lt8"
        style="margin-bottom: 4px"
        @click="copyToClipboard(Ak.Form.ClientId)"
      >
        <md-icon>filter_none</md-icon>
      </md-button>
    </div>
    <div class="s1-loc__md-field-wrapper s1-U__align-children--center s1-U__width--300px">
      <md-field>
        <label for="Ak-ClientSecret">Client secret</label>
        <md-input
          id="Ak-ClientSecret"
          name="Ak-ClientSecret"
          type="password"
          v-model="Ak.Form.ClientSecret"
          disabled
        ></md-input>
      </md-field>
      <md-button
        class="md-icon-button squared s1-U__mg--lt8"
        style="margin-bottom: 4px"
        @click="copyToClipboard(Ak.Form.ClientSecret)"
      >
        <md-icon>filter_none</md-icon>
      </md-button>
    </div>
    <div class="s1-loc__md-field-wrapper s1-U__align-children--center s1-U__width--210px">
      <md-field>
        <label for="Ak-GrantType">GrantType</label>
        <md-input
          id="Ak-GrantType"
          name="Ak-GrantType"
          type="text"
          v-model="Ak.Form.GrantType"
          disabled
        ></md-input>
      </md-field>
      <md-button
        class="md-icon-button squared s1-U__mg--lt8"
        style="margin-bottom: 4px"
        @click="copyToClipboard(Ak.Form.GrantType)"
      >
        <md-icon>filter_none</md-icon>
      </md-button>
    </div>
    <div class="s1-loc__md-field-wrapper s1-U__align-children--center s1-U__width--540px">
      <md-field>
        <label for="Ak-TokenEndpoint">Token endpoint</label>
        <md-input
          id="Ak-TokenEndpoint"
          name="Ak-TokenEndpoint"
          type="text"
          v-model="Ak.Form.TokenEndpoint"
          disabled
        ></md-input>
      </md-field>
      <md-button
        class="md-icon-button squared s1-U__mg--lt8"
        style="margin-bottom: 4px"
        @click="copyToClipboard(Ak.Form.TokenEndpoint)"
      >
        <md-icon>filter_none</md-icon>
      </md-button>
    </div>
    <div
      class="s1-loc__md-field-wrapper s1-U__align-children--center"
      :style="`width: ${Ak.Form.Apis.length > 0 ? Ak.Form.Scopes.length * 7 + 72 : 210}px; max-width: 100%`"
    >
      <md-field>
        <label for="Ak-Scopes">Scopes</label>
        <md-input
          id="Ak-Scopes"
          name="Ak-Scopes"
          type="text"
          placeholder="No API selected"
          v-model="Ak.Form.Scopes"
          disabled
        ></md-input>
      </md-field>
      <md-button
        class="md-icon-button squared s1-U__mg--lt8"
        style="margin-bottom: 4px"
        @click="copyToClipboard(Ak.Form.Scopes)"
        v-show="Ak.Form.Apis.length > 0"
      >
        <md-icon>filter_none</md-icon>
      </md-button>
    </div>
    <div class="s1-U__mg--tp8 s1-U__mg--bt24">
      <p class="s1-U__text-color--dark-2 s1-U__mg--bt8">Summary</p>
      <div
        class="s1-U__border-solid--1 s1-U__bg-color--body-bg s1-U__pd16 s1-U__pd--tp8 s1-U__pd--bt8 s1-U__align-children--center s1-U__width--540px"
      >
        <p
          style="word-break: break-word;"
        >{{Ak.Form.Apis.length > 0 ? formatConcat() : 'No API selected'}}</p>
        <md-button
          class="md-icon-button squared s1-U__mg--lt8"
          @click="copyToClipboard(formatConcat())"
          v-show="Ak.Form.Apis.length > 0"
        >
          <md-icon>filter_none</md-icon>
        </md-button>
      </div>
    </div>
    <div class="s1-loc__md-field-wrapper s1-U__width--540px">
      <md-field>
        <label for="Ak-Description">Description</label>
        <md-textarea id="Ak-Description" name="Ak-Description" v-model="Ak.Form.Description"></md-textarea>
      </md-field>
    </div>
  </div>
</template>

<script>
import Apis from "../../data/Apis.js";

export default {
  name: "AkForm",
  data: () => ({
    Apis
  }),
  props: {
    Ak: Object,
    StoreData: Object,
    $v: Object,
    updateScope: Function
  },
  methods: {
    formatConcat() {
      return `grant_type=${this.Ak.Form.GrantType}&scope=${
        this.Ak.Form.Scopes
      }&client_id=${"************" ||
        this.Ak.Form.ClientId}&cliente_secret=${"************" ||
        this.Ak.Form.ClientSecret}`;
    }
  }
};
</script>