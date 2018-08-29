<template>
    <transition name="fade">
          <div v-if="preview" class="entrance_preview" v-on:click="$emit('hide-preview')">
            <div class="preview_inner">
                 <img class="entrance_image__fullsize" v-bind:src="require(`@/assets/${pic}`)" /> 
            </div>
        </div>
     </transition>
</template>
<script>
export default {
  name : "Preview",
  props : ["pic", "preview"],
  methods : {}
};
</script>
<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>