<template>
    <div class="setBox">
      <div v-show="textType.includes(mSelectOneTypeProps[0])" class="mt-3 mb-3">
        <!-- control part -->
        <div class="control" style="margin-left:15px">
          <div class="row mt-3 mb-3" style="align-items: center;">
            <div class="col col-lg-7">
              Size
            </div>
            <div class="input-size">
              <div class="content">
                <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
                  <span class="ivu-input-suffix">
                    <i style="font-style: normal; font-size: 11px;">w</i>
                  <!-- W -->
                  </span>
                  <input
                    style="width:100%"
                    autocomplete="off" 
                    type="number" 
                    class="ivu-input ivu-input-with-suffix" 
                    placeholder="Enter text"
                    v-model="baseAttr.width"
                    @change="(value) => changeCommon('width', value)"
                    number="true" />
                </div>
              </div>
            </div>
            <div class="input-size">
              <div class="content">
                <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
                  <span class="ivu-input-suffix">
                    <i style="font-style: normal; font-size: 11px;">h</i>
                  <!-- H -->
                  </span>
                  <input
                    autocomplete="off" 
                    type="number" 
                    class="ivu-input ivu-input-default ivu-input-with-suffix" 
                    placeholder="Enter text"
                    v-model="baseAttr.height"
                    @change="(value) => changeCommon('height', value)"
                    number="true" />
                </div>
              </div>
            </div>
          </div>

          <!-- --------------------- Position ----------------------->
          <div class="row mb-3" style="align-items: center;">
            <div class="col col-lg-7">
              Position
            </div>
            <div class="input-size">
              <div class="content">
                <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
                  <span class="ivu-input-suffix">
                    <i style="font-style: normal; font-size: 11px;">x</i>
                  <!-- X -->
                  </span>
                  <input
                    autocomplete="off" 
                    type="number" 
                    class="ivu-input ivu-input-default ivu-input-with-suffix" 
                    placeholder="Enter text"
                    v-model="baseAttr.left"
                    @change="(value) => changeCommon('left', value)"
                    number="true" />
                </div>
              </div>
            </div>
            <div class="input-size">
              <div class="content">
                <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
                  <span class="ivu-input-suffix">
                    <i style="font-style: normal; font-size: 11px;">y</i>
                  <!-- Y -->
                  </span>
                  <input
                    autocomplete="off" 
                    type="number" 
                    class="ivu-input ivu-input-default ivu-input-with-suffix" 
                    placeholder="Enter text"
                    v-model="baseAttr.top"
                    @change="(value) => changeCommon('top', value)"
                    number="true" />
                </div>
              </div>
            </div>
          </div>
          <!-- --------------------- End Position ----------------------->

        </div>
        <!-- control part -->        
        <div class="customborder mt-3"></div>
        <div class="mt-3" style="margin-left: 15px;"> 
          <label>Text</label>
          <Input v-model="this.fontAttr.string" @on-change="(value) =>changeString(value)" @on-keyup="(value) =>textKeyPress(value)" class="mb-2 mt-2" style="width:98%;">
            <template #append>
              <Select style="width:70px" @on-change="changeAddTag" size="small">
                <Option v-for="tag in tags" :value="'['+tag+']'" :key="tag"></Option>
              </Select>
            </template>
          </Input>
        </div>

        <!-- -------------------  Text Setting  ---------------- -->
        <div class="customborder mt-3"></div>
        <div class="mt-3" style="margin-left:15px;">
          <!-- -------------------  text handling  ---------------- -->
          <div class="row" style="">
            <div class="col-8" >
              <b-form-select class="mb-3" v-model="fontAttr.selected_fontfamily" @change="changeFontFamily" size="sm">
                <option v-for="item in fontAttr.fontFamilyList" :value="item.name"  :key="item.name">{{ item.name }}</option>
              </b-form-select>                
            </div>
            <div class="col-3" style="">
              <Button class="ivu-btn ivu-btn-text" @click="uploadFontClick">
                Add custom font
                <Icon type="ios-cloud-upload-outline" />
                <input type="file" id="uploadFont" @change="uploadFont" style="display:none" accept=".woff,.ttf"/>
              </Button>
            </div>
          </div>
          <!-- -------------------  End text handling  ---------------- -->

          <!-- -------------------  font setting  ---------------- -->
          <div class="mt-4 row" style="">
            <!-- -------------------  font size & color  ---------------- -->
            <div class="col-6 row">
              <div class="col-6">
                <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text" style="width: auto;">
                  <i class="ivu-icon ivu-icon-ios-loading ivu-load-loop ivu-input-icon ivu-input-icon-validate"></i>
                  <input 
                    v-model="this.fontAttr.fontSize"
                    type="number" 
                    class="ivu-input ivu-input-default ivu-input-with-prefix" 
                    @change="(value) => changeCommon('fontSize', value)"
                  />
                    <span class="ivu-input-prefix">
                      <i class="ivu-icon ivu-icon-ios-appstore"></i>
                    </span>
                </div>
              </div>
              <div class="col-6">
                <Color style="margin-top:-10px;margin-left:10px;width:100%" :color="baseAttr.fill" @change="(value) => changeCommon('fill', value)"></Color>
              </div>
            </div>
            <!-- -------------------  End font size & color  ---------------- -->

            <!-- -------------------  font style  ---------------- -->
            <div class="col-6" style="text-align: right;">
              <ButtonGroup class="button-group">
                <Tooltip  content="Bold" placement="top">
                  <Button @click="changeFontWeight('fontWeight', this.fontAttr.fontWeight)" class="border-btn" style="margin-left:5px">
                    <svg viewBox="0 0 1024 1024" width="14" height="14">
                      <path
                        d="M793.99865 476a244 244 0 0 0 54-130.42C862.75865 192.98 743.01865 64 593.85865 64H195.01865a32 32 0 0 0-32 32v96a32 32 0 0 0 32 32h63.74v576H195.01865a32 32 0 0 0-32 32v96a32 32 0 0 0 32 32h418.64c141.6 0 268.28-103.5 282-244.8 9.48-96.9-32.78-184.12-101.66-239.2zM418.33865 224h175.52a96 96 0 0 1 0 192h-175.52z m175.52 576h-175.52V576h175.52a112 112 0 0 1 0 224z"
                        :fill="this.fontAttr.fontWeight === 'bold' ? '#305ef4' : '#666'"
                      ></path>
                    </svg>
                  </Button>
                </Tooltip>
                <Tooltip  content="Italic" placement="top">
                  <Button @click="changeFontStyle('fontStyle', this.fontAttr.fontStyle)" class="border-btn" style="margin-left:5px">
                    <svg viewBox="0 0 1024 1024" width="14" height="14">
                      <path
                        d="M832 96v64a32 32 0 0 1-32 32h-125.52l-160 640H608a32 32 0 0 1 32 32v64a32 32 0 0 1-32 32H224a32 32 0 0 1-32-32v-64a32 32 0 0 1 32-32h125.52l160-640H416a32 32 0 0 1-32-32V96a32 32 0 0 1 32-32h384a32 32 0 0 1 32 32z"
                        :fill="this.fontAttr.fontStyle === 'italic' ? '#305ef4' : '#666'"
                      ></path>
                    </svg>
                  </Button>
                </Tooltip>
                <Tooltip  content="Underline" placement="top">
                  <Button @click="changeUnderline('underline', this.fontAttr.underline)" class="border-btn" style="margin-left:5px">
                    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="20px" height="20px" viewBox="0 0 24 24" version="1.1" class="kt-svg-icon">
                        <g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                            <rect x="0" y="0" width="24" height="24"/>
                            <path d="M12.12,19.16 C8.78,19.16 6.4,16.98 6.4,13.48 L6.4,4.8 L8.72,4.8 L8.72,13.54 C8.72,15.74 10.1,16.96 12.12,16.96 C14.14,16.96 15.5,15.74 15.5,13.54 L15.5,4.8 L17.82,4.8 L17.82,13.48 C17.82,16.98 15.46,19.16 12.12,19.16 Z" fill="#000000"/>
                            <rect fill="#000000" opacity="0.3" x="4" y="21" width="16" height="2" rx="1"/>
                        </g>
                    </svg>
                  </Button>
                </Tooltip>
                <Tooltip  content="Strikethrough" placement="top">
                  <Button @click="changeLineThrough('linethrough', this.fontAttr.linethrough)" class="border-btn" style="margin-left:5px">
                    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="20px" height="20px" viewBox="0 0 24 24" version="1.1" class="kt-svg-icon">
                        <g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                            <rect x="0" y="0" width="24" height="24"/>
                            <rect fill="#000000" opacity="0.3" x="4" y="11" width="17" height="2" rx="1"/>
                            <path d="M12.06,19.16 C10,19.16 8.28,18.16 7.44,16.96 L8.82,15.76 C9.5,16.64 10.66,17.42 12.04,17.42 C13.68,17.42 14.72,16.66 14.72,15.42 C14.72,14.12 13.92,13.44 12.4,12.78 L11.1,12.22 C8.94,11.3 8,9.98 8,8.2 C8,6.04 10.04,4.64 12.14,4.64 C13.8,4.64 15.16,5.3 16.12,6.46 L14.84,7.74 C14.1,6.86 13.32,6.38 12.08,6.38 C10.88,6.38 9.82,7.06 9.82,8.24 C9.82,9.28 10.42,9.98 11.92,10.64 L13.22,11.2 C15.14,12.04 16.56,13.22 16.56,15.22 C16.56,17.54 14.84,19.16 12.06,19.16 Z" fill="#000000"/>
                        </g>
                    </svg>
                  </Button>
                </Tooltip>
              </ButtonGroup>
            </div>
            <!-- -------------------  End font style  ---------------- -->

          </div>
          <!-- -------------------  End font setting  ---------------- -->
          
          <!-- -------------------  Long text handling  ---------------- -->
          <div class="mt-3 row" style="">
            <div class="" style="width:65%">
              Long text handling
            </div>  
            <div class="col-4" style="margin: 0;">
              <b-form-select class="mb-3" v-model="fontAttr.selected_text_manage_type" @change="changeHandleLongText" size="sm">
                <option value="automatic" selected>Automatic font size</option>
                <option value="shorten">Shorten text</option>                
              </b-form-select>     
<!-- 
              <Select @on-change="changeHandleLongText">
                <Option value="automatic" selected>Automatic font size</Option>
                <Option value="shorten">Shorten text</Option>
              </Select> -->
            </div>   
          </div>
          <!-- -------------------  End Long text handling  ---------------- --> 
          
          <!-- -------------------  Text alignment  ---------------- -->
        <div class="mt-3" style="height:40px;">
          <div class="" style="float:left;">
            Alignment
          </div>           

          <div class="" style="float:right;">
            <align></align>
          </div>
        </div>
          <!-- -------------------  End Text alignment  ---------------- --> 
          
          <!-- -------------------  Text padding  ---------------- -->
          <!-- <div class="mt-3 row">
            <div style="width:78%">
              Text padding
            </div>  
            <div class="input-size">
              <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
                <span class="ivu-input-suffix">
                  <i style="font-style: normal; font-size: 11px;">px</i>
                </span>
                <input
                  type="number" 
                  class="ivu-input ivu-input-default ivu-input-with-suffix" 
                  :max="360"
                  :min="10"
                  v-model="baseAttr.padding"
                  @change="(value)=>changeCommon('padding', value)"
                />
              </div>
            </div>   
          </div> -->
          <!-- -------------------  End Text padding  ---------------- -->
        </div>
        <!-- -------------------  End Text Setting  ---------------- -->

        <!-- -------------------  Round Corners  ---------------- -->
        <div class="customborder mt-3"></div>
        <div class="mt-3 row" style="margin-left:5px;">
          <div style="width:78%">
            Round Corners
          </div>  
          <div class="input-size">
            <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
              <span class="ivu-input-suffix">
                <i style="font-style: normal; font-size: 11px;">px</i>
              <!-- Pixel -->
              </span>
              <input
                autocomplete="off" 
                type="number" 
                class="ivu-input ivu-input-default ivu-input-with-suffix" 
                v-model="fontAttr.round"
                :max="80"
                @change="(value)=>changeCommon('round', value)"
              />
            </div>
          </div>   
        </div>        

        <!-- -------------------  End Round Corners  ---------------- -->

        <!-- -------------------  Fill  ---------------- -->
        <div class="customborder mt-3"></div>
        <div class="mt-4" style="margin-left:15px;align-items: center;">
          <div class="" style="height:40px;margin-right:15px;">
            <div style="float:left">
              Fill
            </div>                
            <div  style="float:right">
              <Switch size="small" v-model="fillState" @on-change="changeFillState" true-color="#13ce66"/>
            </div>
          </div>   
        <div v-if="fillState" class="" style="align-items: center;margin-right:20px;">
          <div class="" style="height:40px;">
            <div style="float:left">
              Color
            </div>                
            <div class="input-size" style="float:right;width:40%">
              <Color style="width:100%;padding:0" :color="fontAttr.rectFill" @change="(value) => changeSelectFillType('colorFilter', value)"></Color>
            </div>
          </div>                                                
        </div>                    
        </div>
        <!-- -------------------  End Fill  ---------------- -->

        <!-- -------------------  Text Border  ---------------- -->
        <div class="mt-4" style="margin-left:15px;align-items: center;">
          <div class="" style="height:40px;margin-right:15px;">
            <div style="float:left">
              Border
            </div>                
            <div  style="float:right">
              <Switch size="small" v-model="borderState" @on-change="changeBorderState" true-color="#13ce66"/>
            </div>
          </div>   
          <div v-if="borderState">
            <div style="height:40px;margin-right:15px;">
              <div style="float:left;width:40%;">
                <Color :color="fontAttr.stroke" @change="(value)=>changeCommon('stroke', value)" style="padding:0"></Color>
              </div>                        
              <div style="float:right;width:40%;">
                
                <Select v-model="baseAttr.strokeDashArray" @on-change="changeBorderWidth">
                  <Option
                    v-for="item in strokeDashList"
                    :value="item.label"
                    :key="'stroke-' + item.label"
                    default-label="solid"
                  >
                    {{ item.label }}
                  </Option>
                </Select> 

              </div>
            </div>     
            <div class="mt-4 row" style="align-items: center;margin-right:5px;"> 
              <div style="width:80%">
                Line thickness
              </div>  
              <div class="input-size">
                <div class="ivu-input-wrapper ivu-input-wrapper-default ivu-input-type-text">
                  <span class="ivu-input-suffix">
                    <i style="font-style: normal; font-size: 11px;">px</i>
                  </span>
                  <input
                    type="number" 
                    class="ivu-input ivu-input-default ivu-input-with-suffix" 
                    v-model="baseAttr.strokeWidth"
                    :max="40"
                    @change="(value)=>changeCommon('strokeWidth', value)"
                  />
                </div>
              </div>   
            </div>              
          </div>                        
        </div>          
        <!-- -------------------  End Text Border  ---------------- -->

      </div>  
    </div>  
</template>

<script>

import select from '@/mixins/select';
import Color from './color.vue';
import Align from './align.vue';
import $ from "jquery";
import {getShortTags} from "@/service/endpoint.js";
import OpenType from 'opentype.js';
export default {
    mixins: [select],
    props:['mSelectOneTypeProps'],
    components: {
        Color,
        Align
    },  
    data(){
        return{
          fontAttr:{selected_text_manage_type:'automatic'},
          fontAttr:{selected_fontfamily:''},
          showModeText:'',
          activeObject:'',
          borderState:false,
          fillState:false,
          showState:false,            
          rectType:["rect"],
          shapeType:["rect","circle"],
          circleType:["circle"],            
          imgType: ['image'],
          textType: ['i-text', 'textbox', 'text'],
          baseAttr: this.mSelectOneTypeProps[1],
          strokeDashArray: [],
          tags:'',
          //
          fillType: [
              'normal',
              'multiply',
              'screen',
              'overlay',
              'darken',
              'lighten',
              'color-dodge',
              'color-burn',
              'hard-light',
              'soft-light',
              'different',
              'exclusion',
              'hue',
              'saturation',
              'color',
              'luminosity'
          ],
          // font properties
          fontAttr: this.mSelectOneTypeProps[2],   
          // Font drop-down list
          strokeDashList: [
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [1, 10],
                strokeLineCap: 'round',
              },
              label: 'dotted',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [15, 15],
                strokeLineCap: 'square',
              },
              label: 'dashed',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [0, 0],
                strokeLineCap: 'square',

              },
              label: 'solid',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [],
                strokeLineCap: 'square',
              },
              label: 'double',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [],
                strokeLineCap: 'round',
              },
              label: 'groove',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [],
                strokeLineCap: 'square',
              },
              label: 'ridge',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [],
                strokeLineCap: 'round',
              },
              label: 'inset',
            },
            {
              value: {
                strokeUniform: true,
                strokeDashArray: [],
                strokeLineCap: 'round',
              },
              label: 'outset',
            },
            {
              label: 'none',
            },                        
          ],                     
        }        
    },
    created(){
      
      this.canvas.c.on("object:moving",(e)=>{
        this.baseAttr.top = this.canvas.c.getActiveObject().top;
        this.baseAttr.left =this.canvas.c.getActiveObject().left;
        if(this.canvas.c.getActiveObject().customType == "text"){
          if(this.fontAttr.selected_text_manage_type == "automatic"){
            this.showOutArea(this.canvas.c.getActiveObject());
          }else{
            this.hiddenOutArea(this.canvas.c.getActiveObject());
          }
        }
        // this.fixTextPosition();
      });
      this.canvas.c.on("object:scaling",(event)=>{
        this.fixTextPosition()
      })

      this.canvas.c.on("object:modified",(e)=>{
        this.baseAttr.width = this.canvas.c.getActiveObject().width;
        this.baseAttr.height =this.canvas.c.getActiveObject().height;
        if(this.canvas.c.getActiveObject().customType == "text"){
          if(this.fontAttr.selected_text_manage_type == "automatic"){
            this.showOutArea(this.canvas.c.getActiveObject());
          }else{
            this.hiddenOutArea(this.canvas.c.getActiveObject());
          }
        }
        // this.fixTextPosition();
      });   

      this.event.on('selectOne', (e) => {
        if(e[0].type == "group"){
          const activeObject = e[0]._objects[1];
          this.activeObject = activeObject;
          this.fontAttr.string = activeObject.get('text');
          this.fontAttr.string = activeObject.get('text');
          this.fontAttr.fontSize = activeObject.get('fontSize');
          this.fontAttr.fontFamily = activeObject.get('fontFamily');
          this.fontAttr.lineHeight = activeObject.get('lineHeight');
          this.fontAttr.textAlign = activeObject.get('textAlign');
          this.fontAttr.underline = activeObject.get('underline');
          this.fontAttr.linethrough = activeObject.get('linethrough');
          this.fontAttr.charSpacing = activeObject.get('charSpacing');
          this.fontAttr.overline = activeObject.get('overline');
          this.fontAttr.fontStyle = activeObject.get('fontStyle');
          this.fontAttr.textBackgroundColor = activeObject.get('textBackgroundColor');
          this.fontAttr.fontWeight = activeObject.get('fontWeight');
          this.fontAttr.stroke = e[0]._objects[0].get('stroke');
          this.fontAttr.round = e[0]._objects[0].get('ry');
          this.fontAttr.strokeWidth = e[0]._objects[0].get('strokeWidth');
          this.fontAttr.selected_text_manage_type = e[0].texthandle;
          if(this.fontAttr.selected_text_manage_type == undefined){
            this.fontAttr.selected_text_manage_type = "automatic";
          }
          this.fontAttr.selected_fontfamily = e[0]._objects[1].fontFamily;
          this.fontAttr.fontFamilyList = e[0].fontFamilyList;

          if(this.fontAttr.stroke == null){
            this.fontAttr.stroke = ''
          }
        }
            
        });

    },

    mounted(){
      this.initSet();
      getShortTags().then((res)=>{
        this.tags = res.data
      });     
    },

    methods:{      
        //<! ----------------   initialize saved settings.   ---------------->
        initSet(){
          var activeObject = this.canvas.c.getActiveObject();
          if(activeObject != null){
            if(activeObject._objects){

              //<---------------fill of rect setting ------------->
              if(activeObject._objects[0].fill != ''){
                this.fillState = true;
                this.fontAttr.rectFill = activeObject._objects[0].fill;
              }
              //<---------------fill of rect setting ------------->

              // <---------border of rect setting ---------->
              if(activeObject._objects[0].stroke != ''){
                this.borderState = true;
              }

              if(activeObject._objects[0].strokeWidth != 0){
                this.borderState = true;
                this.baseAttr.strokeWidth = activeObject._objects[0].strokeWidth;
              }  
              // <---------border of rect setting ---------->
            }
          }
        },
        //<! ----------------   initialize saved settings.   ---------------->
        //<!--------------- set this.baseAttr.width and height depending on current TextObject's size 
        reSetObj(){
          const activeObject = this.canvas.c.getActiveObject();
          this.baseAttr.width = activeObject.width;
          this.baseAttr.height = activeObject.height;
          this.baseAttr.left = activeObject.left;
          this.baseAttr.top = activeObject.top;
        },         
        //<!--------------- set this.baseAttr.width and height depending on current TextObject's size 
        
        //<!--------------- when textobjectbox's size increase ad decrease, text position and size fix    ---------------->
        fixTextPosition(){
          const activeObject = this.canvas.c.getActiveObject();
          if(activeObject.customType == "text"){
            var obj = activeObject,
            w = obj.width * obj.scaleX,
            h = obj.height * obj.scaleY

            obj.set({
                'height'     : h,
                'width'      : w,
                'scaleX'     : 1,
                'scaleY'     : 1,
            });

            obj._objects[0].set({
                'height'     : h,
                'width'      : w,
                'scaleX'     : 1,
                'scaleY'     : 1,
                "left":0 - (obj.width) / 2,
                "top":0 - (obj.height) / 2
            });

            var position = this.canvas.editor.getPosition(obj);

            obj._objects[1].set({
              "left":position.left,
              "top":position.top,
            });

            //center text object
            activeObject._objects[0].set({
              left: 0 - (activeObject.width) / 2-Number(this.fontAttr.strokeWidth)/2,
              top: 0 - (activeObject.height) / 2-Number(this.fontAttr.strokeWidth)/2,
            });            
          }    


        },
        //<!--------------- when textobjectbox's size increase ad decrease, text position and size fix    ---------------->
        //<!---------------- stroke boder set ------------>
        changeBorderWidth(key) {
          const activeObject = this.canvas.c.getActiveObject()._objects[0];
          if (activeObject) {
            const stroke = this.strokeDashList.find((item) => item.label === key);
            activeObject.set(stroke.value).setCoords();
            this.canvas.c.renderAll();
          }
        },      
        changeFillState(value){

          if(value == false){
            const activeObject = this.canvas.c.getActiveObject();
            activeObject._objects[0].set('fill','').setCoords();
            this.fontAttr.rectFill = '';
            this.canvas.c.renderAll();
          }
        } ,       
        changeBorderState(value){
          if(value == false){
            const activeObject = this.canvas.c.getActiveObject();
            activeObject._objects[0].set('stroke','').setCoords();
            activeObject._objects[0].set('strokeWidth',0).setCoords();
            this.baseAttr.strokeWidth = 0;
            this.fontAttr.stroke = '';
            activeObject._objects[0].set("width",activeObject.width);
            activeObject._objects[0].set("height",activeObject.height);
            //center text object
            activeObject._objects[0].set({
              left: 0 - (activeObject.width) / 2,
              top: 0 - (activeObject.height) / 2,
            });      
            this.canvas.c.renderAll();
          }
        },
        //<!---------------- stroke boder set ------------>

        //<!--------------------- add tag ------------------->
        changeAddTag(value){
          this.changeString(this.fontAttr.string+value);
        },        
        //<!--------------------- add tag ------------------->
        //<!----------------------------  upload font   --------------------->
        uploadFontClick(){

          $("#uploadFont").click();

        },

        uploadFont(e){
          const file = e.target.files[0];
          const reader = new FileReader();
          
          reader.onload = () => {
            const activeObject = this.canvas.c.getActiveObject()._objects[1];
            const fontBuffer = reader.result;
            const font = OpenType.parse(fontBuffer);
            var fontName = font.names.fontFamily.en;            
            this.fontFace = new FontFace(fontName, fontBuffer);
            document.fonts.add(this.fontFace);
            activeObject.set("fontFamily",fontName);
            if (this.fontAttr.fontFamilyList.includes(fontName)) {

              activeObject && activeObject.set('fontFamily', fontName).setCoords();
              setTimeout(()=>{
                this.canvas.c.renderAll();
              },300);

            }else{

              this.fontAttr.fontFamilyList.push({
                name:fontName,
                ttf_base64:''
              });

              activeObject && activeObject.set('fontFamily', fontName).setCoords();
              this.canvas.c.getActiveObject().set('fontFamilyList', this.fontAttr.fontFamilyList)
              setTimeout(()=>{
                this.canvas.c.renderAll();
              },300);

            }            
            this.fontAttr.selected_fontfamily = fontName;
          };
          reader.readAsArrayBuffer(file);      
        },
        //<!----------------------------  upload font   --------------------->
        // <!----------- control box size   -------->
        changeSelectFillType(key,value){

          if(key == "colorFilter"){
            const activeObject = this.canvas.c.getActiveObject()._objects[0];
            activeObject.set("fill",value).setCoords();
            this.canvas.c.renderAll();
          }

          // if(key == "textFilter"){

          //   var filter = new fabric.Image.filters.BlendColor({
          //     color: '#c9f364',
          //     mode: 'multiply'
          //   });

          //   var a = this.canvas.c.getActiveObject();
          //   a.filters = [];
          //   a.filters.push(filter);

          // }

        },        
        // <!----------- control box size   -------->
        //<!---------------- handle long text -------------->
        changeHandleLongText(evt){

          var activeObject = this.canvas.c.getActiveObject()._objects[1];
            if(evt == 'automatic'){

              this.fontAttr.selected_text_manage_type = "automatic";
              this.canvas.c.getActiveObject().set("texthandle",this.fontAttr.selected_text_manage_type);
              this.showOutArea(this.canvas.c.getActiveObject());

            }else{

              activeObject.set("fontSize",this.fontAttr.fontSize).setCoords();
              this.fontAttr.selected_text_manage_type = "shorten";
              this.canvas.c.getActiveObject().set("texthandle",this.fontAttr.selected_text_manage_type);
              activeObject.set("fontSize",activeObject.fontSize).setCoords();
              activeObject.set("scaleX",1);
              activeObject.set("scaleY",1);
              this.hiddenOutArea(this.canvas.c.getActiveObject());

            }
            this.canvas.c.renderAll();
        },
        //<!---------------- handle long text -------------->

        //<!---------------- change text font setting --------------->
        // bold
        changeFontWeight(key, value) {
            const nValue = value === 'normal' ? 'bold' : 'normal';
            this.fontAttr.fontWeight = nValue;
            this.canvas.c.getActiveObject()._objects[1].set(key, nValue).setCoords();
            this.canvas.c.renderAll();
        },
        // italics
        changeFontStyle(key, value) {
            const nValue = value === 'normal' ? 'italic' : 'normal';
            this.fontAttr.fontStyle = nValue;
            this.canvas.c.getActiveObject()._objects[1].set(key, nValue).setCoords();
            this.canvas.c.renderAll();
        },
        // middle stroke
        changeLineThrough(key, value) {
            const nValue = value === false;
            this.fontAttr.linethrough = nValue;
            this.canvas.c.getActiveObject()._objects[1].set(key, nValue).setCoords();
            this.canvas.c.renderAll();
        },
        // underline
        changeUnderline(key, value) {
            const nValue = value === false;
            this.fontAttr.underline = nValue;
            this.canvas.c.getActiveObject()._objects[1].set(key, nValue).setCoords();
            this.canvas.c.renderAll();
        },        
        // modify font family
        changeFontFamily(fontName) {
          if (!fontName) return;
          this.canvas.c.getActiveObject()._objects[1].set("fontFamily",fontName).setCoords();
          this.canvas.c.renderAll();

        },          
        // change string
        changeString(value){

            if(typeof(value)=="string"){
                var string = value;
            }else{
                var string = value.target.value;
            }

            this.fontAttr.string = string;
            this.canvas.c.getActiveObject()._objects[1].set("text", string).setCoords();
            this.changeHandleLongText(this.fontAttr.selected_text_manage_type);

        },
        //<!---------------- change text font setting --------------->

        //<!---------------------- delete shortTag ---------------->
        textKeyPress(value){
          var string = this.fontAttr.string
          if(value.keyCode == 8){
              string = string.slice(0,string.lastIndexOf('['));
              this.changeString(string) 
          }
        },
        //<!---------------------- delete shortTag ---------------->

        //change activeObject
        changeCommon(key,evt){
          if(key=="width" ||key=="height" ||key=="top" ||key=="left"||key=="padding"){

            this.activeObject = this.canvas.c.getActiveObject();
            this.changeProperty(key,evt);
            this.fixTextPosition();
            return;

          }else if(key=="stroke" || key=="strokeWidth" || key=="fill"){

            this.activeObject = this.canvas.c.getActiveObject()._objects[0];
            this.changeProperty(key,evt);
            this.fixTextPosition();
            return;

          }else{

            this.activeObject = this.canvas.c.getActiveObject()._objects[1]
            this.changeProperty(key,evt);
            this.fixTextPosition();
            return;   

          }
        },

        showOutArea(activeObject){
          if(activeObject.width<activeObject._objects[1].width){
            var position = this.canvas.editor.getPosition(activeObject);

            if(Number.isInteger(position.left) == true){
              var diff = (activeObject.width) / 2 - position.left; 
            }else{
              var diff = (activeObject.width) / 2 + position.left; 
            }

            activeObject._objects[1].set("scaleX",activeObject.width/(activeObject._objects[1].width-diff/2)).setCoords();
            activeObject._objects[1].set("scaleY",activeObject.width/(activeObject._objects[1].width-diff/2)).setCoords();
            activeObject._objects[0].set("width",activeObject.width-diff/2).setCoords();
            activeObject._objects[1].set("width",activeObject.width-diff/2).setCoords();
            activeObject._objects[1].clipPath = '';
            this.canvas.c.renderAll();

          }
        },

        hiddenOutArea(activeObject){

          var textObject = activeObject._objects[1];
          var clipRect = new fabric.Rect({
            originX: 'left',
            originY: 'top',
            left: activeObject.left,
            top: activeObject.top,
            width: activeObject.width,
            height: activeObject.height,
            angle:activeObject.angle,
            absolutePositioned: true,
          });     

          textObject.clipPath = clipRect;
          this.canvas.c.renderAll();  

        },
        //change property
        changeProperty(key, evt) {

          if (key === 'width'|| key === 'height'||key === 'left'|| key === 'top') {
            this.activeObject.set(key, Number(evt.target.value));
            this.activeObject._objects[0].set("width",this.activeObject.width).setCoords();
            this.activeObject._objects[0].set("left",-(this.activeObject.width/2)).setCoords();    
            this.activeObject._objects[0].set("height",this.activeObject.height).setCoords();              
            this.activeObject._objects[0].set("top",-(this.activeObject.height / 2)).setCoords();
            this.canvas.c.requestRenderAll();
            return;
          }       
          
          if (key === 'stroke') {
            this.activeObject.set(key, evt);
            this.fontAttr.stroke = evt;
            this.canvas.c.renderAll();
            return;
          }      
          
          if(key === "round"){
            this.activeObject = this.canvas.c.getActiveObject()._objects[0];
            this.activeObject.set("ry", Number(evt.target.value)).setCoords();
            this.activeObject.set("rx", Number(evt.target.value)).setCoords();
            this.canvas.c.renderAll();
            return;
          }
          
          if (key === 'strokeWidth') {
            var activeObject = this.canvas.c.getActiveObject()._objects[0];
            activeObject.set(key, Number(evt.target.value)).setCoords();
            this.fontAttr.strokeWidth = Number(evt.target.value);
            this.canvas.c.renderAll();
            return;
          }

          // control rect's size and group's size depending on padding value
          if (key === "padding") {
            var rect = this.canvas.c.getActiveObject()._objects[0];
            //
            if(!this.activeObject.tempValueForPadding){
              this.activeObject.tempValueForPadding = evt.target.value;
            }
            if(this.activeObject.tempValueForPadding<evt.target.value){
              // rect.set("width",Number(this.activeObject.width)+ Number(evt.target.value)*2).setCoords();
              // rect.set("height",Number(this.activeObject.height) + Number(evt.target.value)*2).setCoords();
              // this.activeObject.set("width",Number(this.activeObject.width) + Number(evt.target.value)*2).setCoords();
              // this.activeObject.set("height",Number(this.activeObject.height) + Number(evt.target.value)*2).setCoords();
              rect.set("left",Number(rect.left) - Number(evt.target.value)).setCoords();
              rect.set("top",Number(rect.top) - Number(evt.target.value)).setCoords();

            }else{
              // rect.set("width",Number(this.activeObject.width)- Number(this.activeObject.tempValueForPadding)*2);
              // rect.set("height",Number(this.activeObject.height) - Number(this.activeObject.tempValueForPadding)*2);
              // this.activeObject.set("width",Number(this.activeObject.width) - Number(this.activeObject.tempValueForPadding)*2);
              // this.activeObject.set("height",Number(this.activeObject.height) - Number(this.activeObject.tempValueForPadding)*2);
              rect.set("left",Number(rect.left)+Number(this.activeObject.tempValueForPadding)).setCoords();
              rect.set("top",Number(rect.top)+Number(this.activeObject.tempValueForPadding)).setCoords();     
            }

            this.activeObject.tempValueForPadding = evt.target.value;


            if(this.canvas.c.getActiveObject().customType == "text"){
              this.hiddenOutArea(this.canvas.c.getActiveObject());
            }
            this.fixTextPosition();            
            this.canvas.c.requestRenderAll();
            return;                
          }
          
          // Rotation Angle Adaptation
          if (key === 'angle') {
              this.activeObject.rotate(Number(evt.target.value)).setCoords();
              this.canvas.c.renderAll();
              return;
          }
          if(key == "fill"){
            this.activeObject = this.canvas.c.getActiveObject()._objects[1];
            this.activeObject.set("fill", evt).setCoords()
            this.canvas.c.renderAll();
            return;              
          }

          if(key == "fontsize"){
            this.activeObject.set(key, Number(evt.target.value)).setCoords();
            this.changeHandleLongText();
            this.fixTextPosition();
            this.hiddenOutArea(this.canvas.c.getActiveObject());
            this.canvas.c.renderAll();
            return;
          }
          
          this.activeObject && this.activeObject.set(key, Number(evt.target.value)).setCoords();
          this.canvas.c.renderAll();
        },    
  }    
}
</script>
<style scoped>
.input-size{
  width:20%
}  
</style>