<template>
  <div>
    <div class="s1-loc__md-field-wrapper s1-U__mg--tp16 s1-U__width--180px">
      <md-field
        :class="{'md-invalid md-field-helper-text s1-U__mg--bt32': $v.Ak.Form.Name.$dirty && $v.Ak.Form.Name.$invalid}"
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
    <div class="s1-U__mg--tp16 s1-U__mg--bt16 md-layout md-gutter">
      <p class="s1-U__text-color--dark-2 s1-U__mg--bt8 md-layout-item md-size-100">APIs *</p>
      <div
        class="md-layout-item md-size-25 md-xsmall-size-100 md-small-size-50 s1-U__mg--bt8"
        v-for="a in Apis"
        :key="a.Id"
      >
        <md-checkbox
          class="s1-U__mg0"
          v-model="Ak.Form.Apis"
          :value="a.Id"
          @change="updateScope()"
        >{{a.Name}}</md-checkbox>
      </div>
    </div>
    <div class="s1-loc__md-field-wrapper s1-U__width--540px s1-U__mg--tp8">
      <md-field>
        <label for="Ak-Description">Description</label>
        <md-textarea
          id="Ak-Description"
          name="Ak-Description"
          md-autogrow
          v-model="Ak.Form.Description"
        ></md-textarea>
      </md-field>
    </div>
    <div class="s1-U__border--top1 s1-U__mg--tp32 s1-U__mg--bt32"></div>

    <div class="s1-U__align-children--center s1-U__flex-wrap s1-U__mg--bt8">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Client ID</h4>
      <div class="s1-U__align-children--center" style="min-width: 70%">
        <h5 class="s1-U__text-color--dark-2" style="word-break: break-word">{{ Ak.Form.ClientId }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Form.ClientId)"
        >
          <md-icon>
            <span>filter_none</span>
          </md-icon>
          <md-tooltip md-direction="right">Copy</md-tooltip>
        </md-button>
      </div>
    </div>
    <div class="s1-U__align-children--center s1-U__flex-wrap s1-U__mg--bt8">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Client secret</h4>
      <div class="s1-U__align-children--center" style="min-width: 70%">
        <h5
          class="s1-U__text-color--dark-2"
          style="word-break: break-word"
        >{{ showSecret ? Ak.Form.ClientSecret : '*************' }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="showSecret = !showSecret"
        >
          <md-icon>
            <span>{{ showSecret ? 'visibility_off' : 'visibility' }}</span>
          </md-icon>
          <md-tooltip
            md-direction="left"
          >{{ showSecret ? 'hide client secret' : 'show client secret' }}</md-tooltip>
        </md-button>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Form.ClientSecret)"
        >
          <md-icon>
            <span>filter_none</span>
          </md-icon>
          <md-tooltip md-direction="right">Copy</md-tooltip>
        </md-button>
      </div>
    </div>
    <div class="s1-U__align-children--center s1-U__flex-wrap s1-U__mg--bt8">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Grant type</h4>
      <div class="s1-U__align-children--center" style="min-width: 70%">
        <h5 class="s1-U__text-color--dark-2" style="word-break: break-word">{{ Ak.Form.GrantType }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Form.GrantType)"
        >
          <md-icon>
            <span>filter_none</span>
          </md-icon>
          <md-tooltip md-direction="right">Copy</md-tooltip>
        </md-button>
      </div>
    </div>
    <div class="s1-U__align-children--center s1-U__flex-wrap s1-U__mg--bt8">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Token Endpoint</h4>
      <div class="s1-U__align-children--center" style="min-width: 70%">
        <h5
          class="s1-U__text-color--dark-2"
          style="word-break: break-word"
        >{{ Ak.Form.TokenEndpoint }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Form.TokenEndpoint)"
        >
          <md-icon>
            <span>filter_none</span>
          </md-icon>
          <md-tooltip md-direction="right">Copy</md-tooltip>
        </md-button>
      </div>
    </div>
    <div class="s1-U__align-children--center s1-U__flex-wrap s1-U__mg--bt8">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Scopes</h4>
      <div class="s1-U__align-children--center" style="min-width: 70%">
        <h5 class="s1-U__text-color--dark-2" style="word-break: break-word">{{ Ak.Form.Scopes }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Form.Scopes)"
          v-show="Ak.Form.Apis.length > 0"
        >
          <md-icon>
            <span>filter_none</span>
          </md-icon>
          <md-tooltip md-direction="right">Copy</md-tooltip>
        </md-button>
      </div>
    </div>
    <div
      class="s1-U__align-children--center s1-U__pd8 s1-U__border-solid--1 s1-U__bg-color--body-bg s1-U__border-radius--2px s1-U__mg--tp16"
      style="justify-content: center;"
      v-show="Ak.Form.Apis.length > 0"
    >
      <h5
        class="s1-U__text-color--dark-2"
        style="word-break: break-word;"
      >{{Ak.Form.Apis.length > 0 ? formatConcat() : 'No API selected'}}</h5>

      <md-button
        class="md-icon-button squared md-dense s1-U__mg--lt8"
        @click="copyToClipboard(formatConcat())"
      >
        <md-icon>
          <span>filter_none</span>
        </md-icon>
        <md-tooltip md-direction="right">Copy</md-tooltip>
      </md-button>
    </div>
  </div>
</template>

<script>
import Apis from "../../data/Apis.js";

export default {
  name: "AkForm",
  data: () => ({
    Apis,
    showSecret: false
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