<template>
  <div class="text-center"  style="position: fixed; bottom: 0;maring-top:-10px" >
    <Button :disabled="!isMultiple" @click="previewCustomImage" type="primary" shape="circle" icon="md-albums">
      Group into Custom Image
    </Button>
    <Modal 
      v-model="groupState" 
      title="Custom Image Creation"
      ok-text = "Create"
      width="50%"
      style="margin-top:-50px"
      >
        <template #header>
          <h4 style="text-align:center">Custom Image Creation</h4>
        </template>
        <div class="row">
          <label class="col-md-3">Name</label>
          <b-form-input class="col-md-5" size="sm" v-model="customImageName"></b-form-input>
          <div style="width:100%;margin-top:10px" class="text-center">
            <img class="ivu-image-img" style=" height: calc(100vh - 300px);width:calc(100vh - 300px)" alt="" id='previewCustomImageBox' src=""  loading="eager">
          </div>        
        </div>
        <template #footer>
          <Button type="error" size="large" long @click="createCustomImage">save</Button>
        </template>
    </Modal>    
  </div>
</template>

<script>
import select from '@/mixins/select';

export default {
  name: 'ToolBar',
  mixins: [select],
  data() {
    return {
      customImageName:'',
      groupState:false,
    };
  },
  created(){
    this.event.on('selectMultiple', (e) => {
      this.mSelectMode = 'multiple';
      this.mSelectId = '';
      this.mSelectIds = e.map((item) => item.id);  
    }); 
  },
  computed: {
    // Single select and equal to group element
    isGroup() {
      return this.mSelectMode === 'one' && this.mSelectOneType === 'group';
    },
    // Is it multiple choice
    isMultiple() {
      return this.mSelectMode == 'multiple';
    },
  },
  methods: {
    createCustomImage(){

      if(this.customImageName == ''){
        this.$Notice.warning({
            desc: 'Please input Name.'
        });
        return true;
      }else{
        this.canvas.editor.group(this.customImageName);
        this.groupState=false;
      }

    },
    previewCustomImage(){
      var state = true;
      var jsonFile = this.canvas.editor.getJson();
      var tempArr = [];
      const activeObj = this.canvas.c.getActiveObject()._objects;
      jsonFile.objects.forEach((el,index)=>{
        activeObj.forEach((item)=>{
          if(item.item_name == el.item_name || index ==0){
            if(el.id == "productImage" || el.id == "trimImage" || el.id == "nonBgImage"){
              state = false;
            }
            tempArr.push(el);
          }
        });
      });
      if(state == false){
        alert("Product image can't be group");
        this.groupState = false;
        return false;
      }
      jsonFile.objects = tempArr;
      var canvas = document.createElement("CANVAS");
      canvas.id = "previewCustomImageCanvas";
      canvas.style.display = "none";
      var customImageCanvas = new fabric.Canvas("previewCustomImageCanvas",{
        fireRightClick:true,
        stopContextMenu:true,
        controlsAboveOverlay:true
      })
      customImageCanvas.loadFromJSON(jsonFile, () => {
        customImageCanvas.renderAll.bind(canvas.c);              
        const workspace = customImageCanvas.getObjects().find((item) => item.id === 'workspace');
        const { left, top, width, height } = workspace;                  
          const option = {
            name: 'New Image',
            format: 'png',
            quality: 1,
            left,
            top,
            width,
            height,
          };
          var oldViewport = customImageCanvas.viewportTransform;
          customImageCanvas.setViewportTransform([1, 0, 0, 1, 0, 0]);
          const imgUrl = customImageCanvas.toDataURL(option);
          customImageCanvas.setViewportTransform(oldViewport);  
          customImageCanvas.requestRenderAll();
          customImageCanvas.renderAll();          
          document.getElementById("previewCustomImageBox").src =imgUrl;         
      });          
      this.groupState = true;
    },
  },
};
</script>
<style scoped lang="less">

</style>
