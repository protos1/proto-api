<template>
  <div class="s1-U__full-width s1-U__align-children--center">
    <md-avatar class="md-avatar-icon md-primary s1-U__mg--rt8" :class="avatarSize || ''">
      <img :src="person.Photo" alt="Avatar" v-if="person.Photo">
      <md-ripple
        class="s1-U__text-uppercase"
        v-else
      >{{person.FullAkName.charAt(0) || person.Email.charAt(0)}}</md-ripple>
    </md-avatar>
    <div class="s1-U__full-width s1-U__text-ellipsis" :title="person.Email">
      <p
        class="s1-U__full-width s1-U__text-ellipsis"
        :title="person.FullAkName"
        v-if="person.FullAkName"
      >{{person.FullAkName}}</p>
      <p
        class="s1-U__full-width s1-U__text-ellipsis"
        :class="{'md-caption': person.FullAkName}"
        :title="person.Email"
      >{{person.Email}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PersonSummary",
  props: {
    person: Object,
    avatarSize: String
  }
};
</script>
