<template>
  <div id="vue-app" class="centered-position" style="width:100vw; height:100vh; background:#fafafa; box-shadow:0px 0px 0px 1px #f1f1f1; overflow-y:scroll;  ">
    <div id="vue-app" style="width:90%; height:100vh; background:#ffffff; box-shadow:0px 0px 0px 1px #f1f1f1; overflow:auto;  ">


      <div class="centered-position" style="width:100%; height:16vh; background:#ffffff; font-size:18px; font-family:Poppins-Bold;  overflow:auto;  ">
        Frontend Developer Assessment
      </div>
      <a-form @finish="onFinish">
      <div class="centered-position"  style="width:100%; height:auto; background:#ffffff; ">
        <div style="width:100%; height:70vh; background:#ffffff; box-shadow:0px 0px 0px 1px #f1f1f1;   ">
          <div style="width:100%; height:40px; background:#fafafa;    ">
            <div style="width:12%; height:40px; float:left; font-size:14px; text-align:left;  box-shadow:0px 0px 0px 1px #f1f1f1;   ">
              <div style="height:40px; float:left; font-size:14px; margin-left:10px;  text-align:left; line-height:40px;   ">
                Field Name (字段名称)
              </div>
            </div>
            <div style="width:12%; height:40px; float:left; font-size:14px;  box-shadow:0px 0px 0px 1px #f1f1f1;  ">
              <div style="height:40px; float:left; font-size:14px; margin-left:10px; text-align:left; line-height:40px;   ">
                Field Type (字段类型)
              </div>
            </div>
             <div style="width:12%; height:40px; float:left; box-shadow:0px 0px 0px 1px #f1f1f1;  ">
              <div style="height:40px; float:left; font-size:14px; margin-left:10px; text-align:left; line-height:40px;   ">
                Required (是否必填)
              </div>
              </div>
              <div style="width:44%; height:40px; float:left;  box-shadow:0px 0px 0px 1px #f1f1f1;   ">
              <div style="height:40px; float:left; font-size:14px; margin-left:10px; text-align:left; line-height:40px;   ">
                Field Options (字段选项)
              </div>
              </div>
              <div style="width:20%; height:40px; float:left; box-shadow:0px 0px 0px 1px #f1f1f1;   ">
                <div style="height:40px; float:left;  font-size:14px; margin-left:10px; text-align:left; line-height:40px;   ">
                  Operate (操作)
                </div>
              </div>
          </div>
          <div  v-for="(field,index_) in data_" :key="index_" style="width:100%; height:50px; background:#ffffff;   overflow:auto;  ">
            <div style="width:12%; height:50px; float:left; background:#ffffff; font-size:14px; text-align:left;  box-shadow:0px 0px 0px 1px #f1f1f1;   ">
              <div style="height:40px; float:left; background:#ffffff; font-size:12px; font-family:Poppins-SemiBold; margin-left:10px; text-align:left; line-height:40px;   ">
                {{field.fieldName}}
              </div>
            </div>
            <div style="width:12%; height:50px; float:left; background:#ffffff; font-size:14px;  box-shadow:0px 0px 0px 1px #f1f1f1;  ">
              <div style="height:50px; float:left; background:#ffffff; font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                {{field.fieldType}}
              </div>
            </div>
             <div style="width:12%; height:50px; float:left; background:#ffffff; box-shadow:0px 0px 0px 1px #f1f1f1;  ">
              <div style="height:50px; float:left; background:#ffffff; font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                  {{field.required==true?`yes`:`no`}}
              </div>
              </div>
              <div style="width:44%; height:50px; float:left; background:#ffffff;  box-shadow:0px 0px 0px 1px #f1f1f1;   ">
              <div style="height:50px; float:left; background:#ffffff; font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                  <a-form-item v-bind="config" name="field" has-feedback>
                    <a-input v-model:value="render[index_].value" :required="field.required ? true : false" v-if="field.fieldType==='text'"  :bordered="false" placeholder="Text" style="width: 170px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "  />
                    <a-date-picker  v-model:value="render[index_].value" :bordered="false"  v-if="field.fieldType==='date' && field.fieldOptions==='year' " picker="year" placeholder="year"  style="width:80px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "  />
                    <a-date-picker v-model:value="render[index_].value" :required="field.required ? true : false" :bordered="false"  v-if="field.fieldType==='date'  && field.fieldOptions==='year-month'"  picker="month" placeholder="year-month"   style="width:120px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "/>
                    <a-date-picker v-model:value="render[index_].value" :required="field.required ? true : false" :bordered="false" v-if="field.fieldType==='date'  && field.fieldOptions==='year-month-day'"  picker="day" placeholder="year-month-day" style="width:150px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "  />
                    <a-date-picker v-model:value="render[index_].value" :required="field.required ? true : false" :bordered="false" v-if="field.fieldType==='date'  && field.fieldOptions==='year-month-day-time'" @change="onChange" @ok="onOk" show-time placeholder="year-month-day hours: minutes" style="width:220px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "  />
                    <a-input-number v-model:value="render[index_].value"  :required="field.required ? true : false"  v-if="field.fieldType==='number'"  id="inputNumber" placeholder="Number" :bordered="false"  style="width:100px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "  :min="1" :max="10" />
                  </a-form-item>

              </div>
              </div>
              <div style="width:20%; height:50px; float:left; background:#ffffff; box-shadow:0px 0px 0px 1px #f1f1f1;   ">
                <div @click="editForm(index_)" style="height:50px; float:left; background:#ffffff; font-weight:bold; cursor:pointer; color:#4361ee; font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                  Edit
                </div>
              </div>
          </div>

          <a-drawer
            :width="500"
            :height="600"
            title="Edit"
            placement="bottom"
            :visible="editVisible"
            @close="onClose"
          >
            <template #extra>
              <a-button style="margin-right: 8px" @click="onClose()">Cancel</a-button>
              <a-button type="primary" @click="updateForm()">Submit</a-button>
            </template>

            <div class="centered-position"  style="width:100%; height:auto;  ">
              <div style="width:70%; ">
                <div style="width:100%; height:auto; float:left; font-size:14px; text-align:left; ">
                  <div style="width:100%; height:40px; float:left; font-size:14px; text-align:left; ">
                    <div style="height:40px; float:left;  font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                      Field Name
                    </div>
                  </div>
                  <div style="height:40px; float:left;  font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                    <a-input v-model:value="edit.fieldName" :bordered="false"  style="width: 170px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; " placeholder="Basic usage" />
                  </div>
                </div>
                <div style="width:100%; height:auto; float:left;  font-size:14px;   ">
                  <div style="width:100%; height:40px; float:left;  font-size:14px;   ">
                    <div style="height:40px; float:left; font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                      Field Type
                    </div>
                  </div>
                  <div style="height:50px; float:left;  font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                     <a-select
                         :ref="selectedFieldType"
                         style="width: 170px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "
                         :bordered="false" :default-value="edit.fieldType" v-model:value="edit.fieldType"
                         @focus="focus" @change="handleChange2"
                       >
                       <a-select-option v-for="(option,index_) in fieldTypes" :key="index_" :value="option">{{option}}</a-select-option>
                      </a-select>
                  </div>
                </div>
               <div style="width:100%; height:auto; float:left;   ">
                 <div style="width:100%; height:40px; float:left;  ">
                  <div style="height:40px; float:left;  font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                    Is Required
                  </div>
                  </div>
                <div style="height:50px; float:left;  font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                     <a-select
                         :ref="selectedRequired"
                         style="width: 170px; box-shadow:0px 0px 0px 1px #f1f1f1;  background:#fafafa; "
                         :bordered="false" :default-value="edit.required" v-model:value="edit.required"
                         @focus="focus" @change="handleChange"
                       >
                       <a-select-option v-for="(option,index_) in requiredOptions" :key="index_" :value="option">{{option}}</a-select-option>
                      </a-select>
                </div>
                </div>
                <div style="width:100%; height:auto; float:left;    ">

                  <div v-if="edit.fieldType=='date'" style="width:100%; height:40px; float:left;    ">
                  <div style="height40px; float:left;  font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                    Field Options
                  </div>
                  </div>
                  <div v-if="edit.fieldType=='date'" style="height:50px; float:left; font-size:12px; margin-left:10px; text-align:left; line-height:40px;   ">
                    <a-radio-group v-model:value="edit.fieldOptions" name="radioGroup">
                       <a-radio value="year">Year</a-radio>
                       <a-radio value="year-month">Year month</a-radio>
                       <a-radio value="year-month-day">Year Month Day</a-radio>
                       <a-radio value="year-month-day-time"> Year month-day hours: minutes</a-radio>
                     </a-radio-group>
                  </div>
                </div>

              </div>
            </div>
          </a-drawer>

          <a-drawer
          v-model:visible="previewVisible"
          class="custom-class"

          title="Preview"
          placement="right"
          :width="600"
          @after-visible-change="afterVisibleChange"
        >
        <div style="width:600px; height:40px; background:#fafafa;    ">
          <div style="width:30%; height:40px; float:left; font-size:14px; text-align:left;   ">
            <div style="height:40px; float:left; font-size:14px; margin-left:10px;  text-align:left; line-height:40px;   ">
              Field Name (字段名称)
            </div>
          </div>
          <div style="width:70%; height:40px; float:left; font-size:14px;                                                                                                                                                                                                                                                                                                                                                                                                                ">
            <div style="height:40px; float:left; font-size:14px; margin-left:10px; text-align:left; line-height:40px;   ">
              Value
            </div>
          </div>
        </div>
        <div   v-for="(item,index_) in render" :key="index_"  style="width:600px; height:40px;   ">
          <div style="width:30%; height:40px; float:left; font-size:14px; text-align:left;    ">
            <div style="height:40px; float:left; font-size:14px; margin-left:10px;  text-align:left; line-height:40px;   ">
              {{data_[index_].fieldName}}
            </div>
          </div>
          <div style="width:70%; height:40px; float:left; font-size:14px;  ">
            <div style="height:40px; float:left; font-size:12px; margin-left:10px; text-align:left; overflow:hidden; line-height:40px;   ">
                {{data_[index_].fieldType=='date' && data_[index_].fieldOptions=='year'  ? item.value.$y: '' }}
                {{data_[index_].fieldType=='date' && data_[index_].fieldOptions=='year-month'  ? item.value.$y+`-`+item.value.$M : '' }}
                {{data_[index_].fieldType=='date' && data_[index_].fieldOptions=='year-month-day'  ? item.value.$y+`-`+item.value.$M+`-`+item.value.$D : '' }}
                {{data_[index_].fieldType=='date' && data_[index_].fieldOptions=='year-month-day-time'  ? item.value.$y+`-`+item.value.$M+`-`+item.value.$D+` `+item.value.$H+`-`+item.value.$m : '' }}
                {{data_[index_].fieldType=='text' ? item.value: '' }}
                {{data_[index_].fieldType=='number' ? item.value: '' }}
            </div>
          </div>
        </div>
        </a-drawer>

        </div>
      </div>
            <button type="submit" style="float:right; margin-right:40px; width:100px; height:40px; margin-top:20px; border:none; border-radius:10px; " @click="submitData()"  >Submit</button>
    </a-form>


    </div>
  </div>

</template>
<script lang="jsx">
import { defineComponent, reactive } from 'vue';

// :::::::::
//import accountPopupWidget from  '../../modal/accountPopup.vue';
export default {
  name: 'App',
  props: {
    msg: Object
  },
  data(){
    return {
      previewVisible:false,
      selectedRequired:'',
        selectedFieldType:'',
      noneOption:'none',
      fieldTypes:[
        'text','date','number'
      ],
      fieldOptions:[
        'none','year-month-day','options'
      ],
      requiredOptions:[
          'no','yes'
      ],
      render:[
        {value:''},
        {value:''},
        {value:''}
      ] ,
      editVisible:false,
      editIndex:0,
      //fieldOptions:{'year':'year', 'year-month':'year-month','year-month-day': 'year-month-day', 'year-month-day-time':'year-month-day hours: minutes'},

      edit:{
        fieldName:'Field 1',
        fieldType:'text',
        required:true,
        fieldOptions:'',
        value:'',
      },
      data_:[
       {
         fieldName:'Field 1',
         fieldType:'text',
         required:true,
         fieldOptions:'',
         value:'',

       },
       {
         fieldName:'Field 2',
         fieldType:'date',
         required:true,
         fieldOptions:'year',
         value:'',

       },
       {
         fieldName:'Field 3',
         fieldType:'number',
         required:false,
         fieldOptions:'text',
         value:'',

       },



      ],
      isLoggedIn: false,
      userCookieData:{},

    }
   },
  components: {
   // TopBarWidget,TopBarLoggedInWidget,HomeFooterWidget,

     // accountPopupWidget,
  },
  created(){
     console.log("router params id:: ",this.$route.params.id);
     this.checkUserExists('auto-login')==1?this.isLoggedIn=true:this.isLoggedIn=false;
     //this.$router.push('userProfileWidget' );

  },
  mounted() {
    //this.$router.push('/home');
    window.require = (name) => new URL(name, import.meta.url).href;
  },
  methods:{
    focus(){

    },
    onOk(index){
      //this.edit.fieldOptions=this.data_[index].fieldOptions

    },
    editForm(index){
      this.editVisible=true
      this.edit.fieldName=this.data_[index].fieldName
      this.edit.fieldType=this.data_[index].fieldType
      this.edit.required=this.data_[index].required==true?'yes':'no'
      this.edit.fieldOptions=this.data_[index].fieldOptions
      console.log(this.edit)
      this.editIndex=index

    },
    handleChange(ev){
      //this.edit.required=this.selectedRequired
      console.log(this.edit)
    },
    handleChange2(){
      //this.edit.fieldType=this.selectedFieldType
      console.log(this.edit)


    },
    onFinish (values){
      alert(values)
    console.log('Success:', values, formState);
  },

    updateForm(){
      this.data_[this.editIndex].fieldName = this.edit.fieldName
      this.data_[this.editIndex].fieldType = this.edit.fieldType
      this.data_[this.editIndex].required = this.edit.required=='yes'?true:false
      this.data_[this.editIndex].fieldOptions = this.edit.fieldOptions
      console.log(this.data_[this.editIndex])
      this.onClose()

    },
    submitData(){
      //e.preventDefault()
      console.log(this.render[0].value)

      let noInput=false
      for(let i=0; i<this.render.length; i++ ){
        if(this.render[i].value==''){
          noInput=true
        }
      }

      if(noInput!=true){
        this.previewVisible=true;


      }





    },
    onClose(){
      this.editVisible=false
    },

    goUserHome(){
      //this.$router.push('/yop/');
      // this.$router.push('/home');

    },
    goHome(){
      //this.$router.push('/home/');
      this.$router.push('/yop/');

    },
    checkUserExists(type){
    let result
    if(type=='auto-login'){
      console.log('check user ')
      //window.localStorage.getItem("username") === null
      let userCookieData
      let localStoreData
      if(this.$cookies.isKey('siteAccessT') ){
        userCookieData=this.$cookies.get("siteAccessT")
        this.userCookieData=userCookieData
        //$cookies.isKey(keyName)
        // localStorage.getItem("siteAccessT") !== null
        console.log(userCookieData)
        localStoreData = JSON.parse( window.localStorage.getItem("siteAccessT"))
        console.log( localStoreData ,window.localStorage.getItem("siteAccessT"))
        console.log("true")
        result=1;
        this.goUserHome();

      }else{
        result=0
        console.log("false")
      }
      console.log("local storage:  ",window.localStorage.getItem("siteAccessT"),localStoreData,"user cookies: ",userCookieData )



    }
    return result
  },
  },


}
</script>

<style>
@font-face {
    font-family: "Poppins-Bold";
    src: url("@/assets/fonts/Poppins/Poppins-Bold.ttf") format("truetype");
}

@font-face {
    font-family: "Poppins-SemiBold";
    src: url("@/assets/fonts/Poppins/Poppins-SemiBold.ttf") format("truetype");
}

@font-face {
    font-family: "Poppins-Medium";
    src: url("@/assets/fonts/Poppins/Poppins-Medium.ttf") format("truetype");
}

@font-face {
    font-family: "Poppins-Regular";
    src: url("@/assets/fonts/Poppins/Poppins-Regular.ttf") format("truetype");
}

@font-face {
    font-family: "Montserrat-Bold";
    src: url("@/assets/fonts/Montserrat/Montserrat-Bold.ttf") format("truetype");
}

@font-face {
    font-family: "Montserrat-SemiBold";
    src: url("@/assets/fonts/Montserrat/Montserrat-SemiBold.ttf") format("truetype");
}

@font-face {
    font-family: "Montserrat-Medium";
    src: url("@/assets/fonts/Montserrat/Montserrat-Medium.ttf") format("truetype");
}

@font-face {
    font-family: "Montserrat-Regular";
    src: url("@/assets/fonts/Montserrat/Montserrat-Regular.ttf") format("truetype");
}




#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
  margin:0px;
  padding:0px;
  width:100vw;

  height:100vh;
  position:absolute;
  left:0px;
  top:0px;
  float:left;
  background:#fafafa;
  display:flex;
  justify-content:center;

}


.title-text{
  width:74px; height:30px; font-size:16px;
  font-family: Montserrat-Regular;
  color:#404040; top:10px; position:relative;

}
.title-text-center{
  text-align: center;
  width:74px; height:30px; font-size:16px;
  font-family: Montserrat-Regular; color:#404040;
  top:10px; position:relative;

}
.title-text-left{
  text-align: left;
  width:74px; height:30px; font-size:16px;
  font-family: Montserrat-Regular;
  color:#404040; top:10px; position:relative;

}
.title-text-right{
  text-align: right;
  width:74px; height:30px; font-size:16px;
  font-family: Montserrat-Regular;
  color:#404040; top:10px; position:relative;

}
.bold-medium-text{
  font-size:16px; line-height:16px;
  position:relative; font-weight: bold;

}
.bold-medium-text-center{
  text-align: center;
  font-weight: bold;
  font-size:16px; line-height:16px;
  position:relative;

}
.bold-medium-text-left{
  text-align: left;
  font-weight: bold;
  font-size:16px; line-height:16px;
  position:relative;

}
.bold-medium-text-right{

  text-align: right;
  font-weight: bold;
  font-size:16px; line-height:16px;
  position:relative;


}
.bold-large-text{
  font-weight: bold;
  font-size:20px; line-height:20px;
  position:relative;

}
.bold-large-text-center{
  text-align: center;
  font-weight: bold;
  font-size:20px; line-height:20px;
  position:relative;

}
.bold-large-text-left{
  text-align: left;
  font-weight: bold;
  font-size:20px; line-height:20px;
  position:relative;

}
.bold-large-text-right{
  text-align: right;
  font-weight: bold;
  font-size:20px; line-height:20px;
  position:relative;

}
.bold-small-text{
  font-weight: bold;
  font-size:13px; line-height:13px;
  position:relative;

}
.bold-small-text-center{
  font-weight: bold;
  text-align: center;
  font-size:13px; line-height:13px;
  position:relative;

}
.bold-small-text-left{
  font-weight: bold;
  text-align: left;
  font-size:13px; line-height:13px;
  position:relative;

}
.bold-small-text-right{
  font-weight: bold;
  text-align: right;
  font-size:13px; line-height:13px;
  position:relative;

}

/* */
.normal-medium-text{
  font-size:13px; line-height:13px;
  position:relative;

}
.normal-medium-text-center{
  text-align: center;
  font-size:16px; line-height:16px;
  position:relative;

}
.normal-medium-text-left{
  text-align: left;
  font-size:16px; line-height:16px;
  position:relative;

}
.normal-medium-text-right{
  text-align: right;
  font-size:16px; line-height:16px;
  position:relative;
}
/* */
.normal-large-text{
  font-size:20px; line-height:20px;
  position:relative;

}
.normal-large-text-center{
  text-align: center;
  font-size:20px; line-height:20px;
  position:relative;
}
.normal-large-text-left{
  text-align: left;
  font-size:16px; line-height:16px;
  position:relative;

}
.normal-large-text-right{
  text-align: right;
  font-size:16px; line-height:16px;
  position:relative;

}
/* */
.normal-small-text{
  font-size:13px; line-height:13px;
  position:relative;
}
.normal-small-text-center{
  text-align: center;
  font-size:13px; line-height:13px;
  position:relative;

}
.normal-small-text-left{
  text-align: left;
  font-size:13px; line-height:13px;
  position:relative;
}
.normal-small-text-right{
  text-align: right;
  font-size:13px; line-height:13px;
  position:relative;

}

/***/
.title-highlight{
  height:20px; width:7px; background:#5757F6; float:left;
   overflow:hidden; position:relative;
   top:10px; left:10px; border-radius:14px;
}

.centered-position{
  align-items: center;
  vertical-align:middle;
  justify-content:center;
  text-align:center;
  display:flex;

}
.basic-button{
  border:none;
  outline:none;
  border-radius:10px;
}

/******/

.menu-list-container {
    height: 40px;
    width: 100vw;
    list-style-type: none;
    display: flex;
    text-align: center;
    flex-direction: row;
    vertical-align:middle;
    justify-content: center;
    align-items: center;
    margin-bottom:0px;
}

.menu-item {
  height:20px;
  line-height:20px;
  cursor: pointer;
  font-size: 14px;
  padding-left: 2px;
  padding-right: 2px;
  padding-bottom: 6px;
  min-width: 30px;
  text-align: center;
  letter-spacing: 0.01612em;
  display: inline-block;
  position: relative;
  font-family: Poppins-SemiBold;

}
.menu-item-active {
  height:20px;
  line-height:20px;
  cursor: pointer;
  border-bottom: 1px solid rgba(117, 0, 252, 1);
  font-size: 14px;
  padding-left: 2px;
  padding-right: 2px;
  padding-bottom: 6px;
  color:rgba(117, 0, 252, 1);
  min-width: 30px;
  text-align: center;
  letter-spacing: 0.01612em;
  display: inline-block;
  position: relative;
  font-family: Poppins-SemiBold;

}

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition-duration: 0.5s;
  transition-property: height, opacity, transform;
  transition-timing-function: cubic-bezier(0.55, 0, 0.1, 1);
  overflow: hidden;
}

.slide-left-enter,
.slide-right-leave-active {
  opacity: 0;
  transform: translate(2em, 0);
}

.slide-left-leave-active,
.slide-right-enter {
  opacity: 0;
  transform: translate(-2em, 0);
}

 .fade-enter-active,
 .fade-leave-active {
   transition-duration: 0.3s;
  transition-property: opacity;
  transition-property: height, opacity;
   transition-timing-function: ease;
  overflow: hidden;


 }
 router-link{
    text-decoration: none;
}


.category-menu-item{
  cursor: pointer;
  font-size: 11px;
  padding: 2px;
  padding-left: 16px;
  padding-right: 16px;
  min-width: 16px;
  color:#000000;
  max-width: 130px;
  margin: 4px;
  border-radius: 6px;
  text-align: center;
  letter-spacing: 0.01612em;
  display: inline-block;
  position: relative;
  top:4px;
  font-family: Poppins-Medium;
  transition: 0.3s all;
  transition-delay: 0.3s;

}
.product-category-menu{
  padding-left:10%;
  width:90%; font-family:Montserrat-Medium; cursor:pointer; height:24px; font-size:11px; line-height:24px; text-align:left; margin-left:0%;
  color:#888888;
}
.product-category-menu:hover{
  padding-left:10%;

  background:#fff1e6;
  width:90%; font-family:Montserrat-Medium; cursor:pointer; height:24px; font-size:11px; line-height:24px; text-align:left; margin-left:0%;
  transition: 100ms all;
  transition-delay: 100ms;
  color:#000000;
}

.sub-category-menu{
  padding-left:8%;
  width:100%; font-family:Montserrat-Medium; cursor:pointer; height:24px; font-size:10px; line-height:24px; text-align:left; margin-left:0%;
  color:#888888;
}
.sub-category-menu:hover{
  padding-left:8%;
  background:#fff1e6;
  width:100%; font-family:Montserrat-Medium; cursor:pointer; height:24px; font-size:10px; line-height:24px; text-align:left; margin-left:0%;
  transition: 50ms all;
  transition-delay: 50ms;
  color:#000000;
}


.product-detail-menu{
  padding-left:20px; padding-right:20px;
float:left;
  min-width:40px; font-family:Montserrat-Medium; cursor:pointer; height:40px; font-size:11px; line-height:40px; text-align:center; margin-left:0px;
  color:#888888;
}
.product-detail-menu:hover{

  min-width:40px; font-family:Montserrat-Medium; cursor:pointer; height:40px; font-size:11px; line-height:40px; text-align:center; margin-left:0px;
  transition: 50ms all;
  transition-delay: 50ms;
  color:#000000;
}


.product-detail-menu-active{

    background:#fff1e6;
  padding-left:20px; padding-right:20px;
float:left;
  min-width:40px; font-family:Montserrat-SemiBold; cursor:pointer; height:40px; font-size:11px; line-height:40px; text-align:center; margin-left:0px;
  color:#000000;
}
.product-detail-menu-active:hover{

  min-width:40px; font-family:Montserrat-SemiBold; cursor:pointer; height:40px; font-size:11px; line-height:40px; text-align:center; margin-left:0px;
  transition: 50ms all;
  transition-delay: 50ms;
  color:#000000;
}






li a {
    text-decoration: none  !important;
}
a { text-decoration: none  !important; }

.shadow-st{
  box-shadow:0px 0px 4px 1px #f1f1f1;
}


.dashboard-menu-block{
  width:14%; height:auto; border-radius:10px; float:left; position:relative;  left:1%; margin-top:0px;
}
.dashboard-content-block{
  width:82%; height:auto;  position:relative; left:2%; margin-top:0px; float:left;
}
.dashboard-content-block-inner{
  width:98%; height:auto;  position:relative; border-radius:10px; background:#ffffff; overflow:hidden; box-shadow:0px 0px 0px 1px #f1f1f1; margin-top:20px;  left:1%; float:right;
}
.dashboard-background{
  width:100%; height:auto; overflow-y:hidden;  background:rgb(228,193,249,0.08); position:fixed; padding-bottom:200px;
}
.modern-shadow{
}

.input-shadow{
  box-shadow:0px 0px 4px 1px rgb(255,153,200,0.3);

}

.context-menu-container{
  height:200px !important;
}


.v3-search{
  border:none !important;
  outline:none !important;


}
</style>
