<template>
<div v-if="photo.length" class="desc-text desc-image__entrance outer_container" ref="outer">
            <hr>
            <div class="parent-img" v-bind:style="{ height: height +'px' }">
                    <div class="desc-controls left-control" v-on:click="clickControl('left', control.disableLeftControl)" v-bind:class="{ disabled: control.disableLeftControl }">
                        <i class="fas fa fa-angle-left"></i>
                    </div>
                    <div class="desc-image__container" ref="inner_container">
                        <div v-for="( pic, index ) in photo" v-bind:pic="pic" v-bind:key="index" class='entrance-child' ref="test" v-on:click="$emit('show-preview', pic)">
                            <img class="desc-entrance_image" v-bind:src="require(`@/assets/${pic}`)" /> 
                        </div>
                    </div>
                    <div class="desc-controls right-control" v-on:click="clickControl('right', control.disableRightControl)" v-bind:class="{ disabled: control.disableRightControl }">
                        <i class="fas fa fa-angle-right"></i>
                    </div>
                    </div>
                <div class="desc-entrance__container" > 
                </div>
            <hr>
        </div>
</template>

<script>
export default  {
  name : "entranceSlider",
  props : ['photo', 'height'],
  data : function(){
      return {
          control : {
            disableLeftControl : true,
            disableRightControl : false,
            translateX : 0,
            index: 0,
            padding: 0,
            innerW: 0,
            outerW: 0
        }
      };
  },
  methods : {
   clickControl(direction, disable){
        if(disable) return;
        this.control.outerW = this.$refs.outer.clientWidth;
        this.control.innerW = this.$refs.inner_container.clientWidth;
        if(this.control.innerW <= this.control.outerW) {
                this.control.disableRightControl = true;
                return;
        }
        if(!this.control.index) this.getIndex();
        direction === "right" ? this.flowRight() : this.flowLeft();  
    },
    getIndex: function(){
        var w = 0;
        for(var i = 0; i < this.$refs.test.length; i++){
            w+=this.$refs.test[i].clientWidth;
            if(w > this.control.outerW){
                this.control.padding = w - this.control.outerW - this.$refs.test[i].clientWidth;
                this.control.index = i;
                break;
            }
        }
    },
    getMaxTranslate: function(){
        var maxTranslate = this.control.innerW - this.control.outerW;
        return maxTranslate;
    },
    flowRight: function(){
        this.control.translateX += this.$refs.test[this.control.index].clientWidth;
        var translate = this.control.translateX + this.control.padding;
        this.$refs.inner_container.style.transform = "translatex(-" + translate  + "px)";
        // console.log(translate);
        var newInd = this.control.index+1;
        this.control.disableLeftControl = false; 
        this.control.index = newInd;
        if( this.control.translateX >= this.getMaxTranslate() ){
            this.control.disableRightControl = true; 
            this.control.disableLeftControl = false; 
            return false;
        }
    },
    flowLeft: function(){
        this.control.translateX -= this.$refs.test[this.control.index - 1].clientWidth;
        var translate = this.control.translateX;
        this.$refs.inner_container.style.transform = "translatex(-" + translate  + "px)";
        //console.log(translate);
        var newInd = this.control.index-1;
        this.control.disableRightControl = false;  
        this.control.index=newInd;
        if( this.control.translateX <= 0 ){
            this.control.disableRightControl = false; 
            this.control.disableLeftControl = true; 
            return false;
        }
    }
  }
};
</script>