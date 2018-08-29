<template>
 <div class="entrance-component" :style="{maxWidth: maxWidth+'px', margin: marg}">
      <preview :preview="preview" v-on:hide-preview="hidePreview"  :pic="pic"></preview>
      <entrance-slider :photo="photo" v-on:show-preview="showPreview($event)" :height="height" ></entrance-slider>
</div>
</template>

<script>
import Preview from "./Preview.vue";
import entranceSlider from "./EntranceSlider.vue";

export default {
  name : "EntranceComponent",
  props : { photo: Array , height: String, maxWidth: Number, marg: String },
  data: function(){
      return {
           preview: false, 
           pic : ''
      };
  },
  
  components : {
      "preview" : Preview, 
      "entrance-slider" : entranceSlider,
  },

  methods : {
    showPreview: function(pic){
        this.pic = pic;
        this.preview = true;
    },
    hidePreview: function(){
       this.preview = false; 
    }
  },

};
</script>
<style lang="less">
.transition-duration(@t){
    transition-duration: @t;
    -webkit-transition-duration: @t;
    -ms-transition-duration: @t;
}
.transition(@t){
    -webkit-transition: @t;
     -moz-transition: @t;
     -o-transition: @t;
     transition: @t;
}
.align(@a){
    -webkit-align-items: @a;
    -ms-align-tems: @a;
    align-items: @a;
}
.justify(@j){
    -webkit-justify-content: @j;
    -ms-justify-content: @j;
    justify-content: @j;
}
@container_width: 320;
@mobile: ~"(max-width: 400px)";
@mobile_big: ~"(max-width: 440px)";
@height: ~"(max-height: 550px)";

.flex {
    display: -webkit-box; 
    display: -moz-box;
    display: -ms-flexbox;
    display: -webkit-flex; 
    display: flex;
}
.flex-direction(@d){
    flex-direction: @d;
    -webkit-flex-direction: @d;
}
.align-items(@d){
    align-items: @d;
    -webkit-align-items: @d;
}

/*** entrance preview ***/


.desc-image__entrance {
    .parent-img{
        position: relative;
        height: 60px;
        overflow: hidden;
        z-index: 1;
    }
    .desc-image__container {
        display: flex;
        position: absolute;
        height: 100%;
       .transition(1s ease-in-out);
    }
    .entrance-child {
        cursor:pointer;
    }
    .desc-image__container img {
        max-height: 60px;
        margin: 0 2px;
        z-index: 1;
    }
    .desc-controls {
        position: absolute;
        top: 0;
        bottom:0;
        margin: auto;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        background:rgba(0,0,0,0.5);
        color: white;
        cursor: pointer;
        z-index: 3;
        .transition(1s ease-out);
    }
    .desc-controls.disabled {
         background:rgba(0,0,0,0.3);
    }
    .desc-controls .fas {
        margin: 50%;
        transform: translate(-50%, -50%);
    }
    .left-control{
        left:0;
    }
    .right-control{
        right:0;
    }
    hr{
        height:0;
        border: 1px solid #302f2b;
    }
}
.desc-entrance__container {
    overflow: hidden;
}
.entrance_preview{
    position: fixed;
    background: rgba(0,0,0,0.5);
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 100;
    .preview_inner{
        top: 40%;
        left: 50%;
        transform: translate(-50%, -50%);
        max-width: 500px;
        position: absolute;
        cursor: grab;
        img {
            width: 100%;
        }
    }
}

/*** end of entrance preview ***/

@media (max-width: 768px){
    .entrance_preview .preview_inner{
        max-width: 100%;
        padding: 10px;
    }
}

</style>