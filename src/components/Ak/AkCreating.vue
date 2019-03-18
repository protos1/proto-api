<template>
  <section class="s1-U__width--900px" style="margin: 0 auto;">
    <header class="s1-U__mg--bt32 s1-U__mg--tp32">
      <div class="s1-U__align-children--center">
        <md-button class="md-icon-button s1-U__mg--rt8" @click="Ak.DiscardCreatingInterface = true">
          <md-icon>arrow_back</md-icon>
        </md-button>
        <h1 class="md-display-1">API client creation</h1>
      </div>
    </header>
    <md-card>
      <div
        class="md-layout md-alignment-center-center s1-loc__loading"
        :class="Ak.CreatingFormLoading && 'active'"
      >
        <md-progress-spinner md-mode="indeterminate"></md-progress-spinner>
      </div>
      <md-content class="md-scrollbar s1-U__pd16 s1-U__pd--lt48" style="overflow: auto">
        <ak-form :StoreData="StoreData" :updateScope="updateScope" :Ak="Ak" :$v="$v"></ak-form>
      </md-content>
      <md-card-actions class="s1-U__pd16 s1-U__border--top1 s1-U__flex-shrink-0">
        <md-button
          class="md-primary md-raised"
          :disabled="$v.Ak.Form.$invalid"
          @click="saveCreated('Ak')"
        >
          <span class="s1-U__pd--lt8 s1-U__pd--rt8">Create API Client</span>
        </md-button>
      </md-card-actions>
    </md-card>

    <md-dialog-confirm
      :md-active.sync="Ak.DiscardCreatingInterface"
      md-title="Discard API client registration?"
      md-content="When you exit, the API client information provided will be discarded."
      md-confirm-text="discard"
      md-cancel-text="back"
      @md-cancel="Ak.DiscardCreatingInterface = false"
      @md-confirm="discardCreating('Ak')"
    />
  </section>
</template>

<script>
import AkForm from "./AkForm.vue";

export default {
  name: "AkCreating",
  components: {
    AkForm
  },
  props: {
    Ak: Object,
    StoreData: Object,
    $v: Object,
    saveCreated: Function,
    discardCreating: Function,
    genFields: Function,
    updateScope: Function
  },
  mounted() {
    this.genFields();
  }
};
</script>