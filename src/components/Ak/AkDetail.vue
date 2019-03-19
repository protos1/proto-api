<template>
  <div>
    <div class="s1-U__align-children--top">
      <md-icon class="s1-U__mg--rt16 s1-U__mg--tp8">
        <span class="s1-U__text-color--dark-3">vpn_key</span>
      </md-icon>
      <div class="s1-chip-wrapper--left s1-U__mg--bt16">
        <md-chip
          class="s1-U__border-radius--2px"
          v-for="ak in Ak.Detailed.Apis"
          :key="ak + '-detailed'"
        >{{getNameById(Apis, ak)}}</md-chip>
      </div>
    </div>
    <div class="s1-U__align-children--center s1-U__flex-wrap s1-U__mg--bt8">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Client ID</h4>
      <div class="s1-U__align-children--center" style="min-width: 70%">
        <h5
          class="s1-U__text-color--dark-2"
          style="word-break: break-word"
        >{{ Ak.Detailed.ClientId }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Detailed.ClientId)"
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
        >{{ showSecret ? Ak.Detailed.ClientSecret : '*************' }}</h5>
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
          @click="copyToClipboard(Ak.Detailed.ClientSecret)"
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
        <h5
          class="s1-U__text-color--dark-2"
          style="word-break: break-word"
        >{{ Ak.Detailed.GrantType }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Detailed.GrantType)"
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
        >{{ Ak.Detailed.TokenEndpoint }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Detailed.TokenEndpoint)"
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
        <h5 class="s1-U__text-color--dark-2" style="word-break: break-word">{{ Ak.Detailed.Scopes }}</h5>
        <md-button
          class="md-icon-button squared md-dense s1-U__mg--lt8"
          style="margin-bottom: 4px"
          @click="copyToClipboard(Ak.Detailed.Scopes)"
          v-show="Ak.Detailed.Apis.length > 0"
        >
          <md-icon>
            <span>filter_none</span>
          </md-icon>
          <md-tooltip md-direction="right">Copy</md-tooltip>
        </md-button>
      </div>
    </div>
    <div
      class="s1-U__align-children--center s1-U__pd--tp8 s1-U__pd--bt8 s1-U__pd--lt16 s1-U__pd--rt16 s1-U__border-solid--1 s1-U__bg-color--body-bg s1-U__border-radius--2px s1-U__mg--tp16"
      v-show="Ak.Detailed.Apis.length > 0"
    >
      <h5
        class="s1-U__text-color--dark-2 s1-U__full-width"
        style="word-break: break-word;"
      >{{Ak.Detailed.Apis.length > 0 ? formatConcat() : 'No API selected'}}</h5>

      <md-button
        class="md-icon-button squared md-dense s1-U__mg--lt16 s1-U__flex-shrink-0"
        @click="copyToClipboard(formatConcat())"
      >
        <md-icon>
          <span>filter_none</span>
        </md-icon>
        <md-tooltip md-direction="right">Copy</md-tooltip>
      </md-button>
    </div>

    <div class="s1-U__mg--tp16">
      <h4 class="s1-U__width--144px s1-U__flex-shrink-0">Description</h4>
      <p class="s1-U__mg--tp4">{{Ak.Detailed.Description}}</p>
    </div>
  </div>
</template>

<script>
import Apis from "../../data/Apis.js";

export default {
  name: "AkDetail",
  data: () => ({
    Apis,
    showSecret: false
  }),
  props: {
    Ak: Object
  },
  methods: {
    formatConcat() {
      return `grant_type=${this.Ak.Detailed.GrantType}&scope=${
        this.Ak.Detailed.Scopes
      }&client_id=${"************" ||
        this.Ak.Detailed.ClientId}&cliente_secret=${"************" ||
        this.Ak.Detailed.ClientSecret}`;
    }
  }
};
</script>