<template>
  <section class="s1-U__width--900px" style="margin: 0 auto;">
    <header class="s1-U__mg--bt32 s1-U__mg--tp32">
      <p
        class="md-caption s1-U__mg--lt48 s1-U__pd--lt4"
        v-if="Ak.Form.Id"
      >{{getNameById(StoreData.Ak, Ak.Form.Id)}}</p>
      <div class="s1-U__align-children--center">
        <md-button class="md-icon-button s1-U__mg--rt8" @click="Ak.DiscardEditingInterface = true">
          <md-icon>arrow_back</md-icon>
        </md-button>
        <div>
          <h1 class="md-display-1">API Client editing</h1>
        </div>
      </div>
    </header>
    <md-card>
      <div
        class="md-layout md-alignment-center-center s1-loc__loading"
        :class="Ak.EditingFormLoading && 'active'"
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
          @click="saveEdited('Ak')"
        >
          <span class="s1-U__pd--lt8 s1-U__pd--rt8">Save changes</span>
        </md-button>
      </md-card-actions>
    </md-card>

    <md-dialog-confirm
      :md-active.sync="Ak.DiscardEditingInterface"
      md-title="Discard Api client editing?"
      md-content="When you discard, the Api client information edited will be discarded."
      md-confirm-text="discard"
      md-cancel-text="back"
      @md-cancel="Ak.DiscardEditingInterface = false"
      @md-confirm="discardEditing('Ak')"
    />
  </section>
</template>

<script>
import AkForm from "./AkForm.vue";

export default {
  name: "AkEditing",
  components: {
    AkForm
  },
  props: {
    Ak: Object,
    StoreData: Object,
    $v: Object,
    saveEdited: Function,
    discardEditing: Function,
    updateScope: Function
  }
};
</script>