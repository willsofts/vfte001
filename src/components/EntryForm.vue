<template>
  <DialogForm ref="dialogForm">
    <template v-slot:header>
      <h4 class="modal-title" v-if="insertMode">{{ labels.title_new }}</h4>
      <h4 class="modal-title" v-if="updateMode">{{ labels.title_edit }}</h4>
    </template>
    <template v-slot:default>
        <div class="row row-height">
          <div class="col-height col-md-5">
            <label for="programid" class="control-label">{{ labels.programid_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.programid.$error}">
              <input ref="programid" type="text" v-model="localData.programid" id="programid" class="form-control input-md" maxlength="20" :disabled="disabledKeyField" />
              <label class="required">*</label>
            </div>
            <span v-if="v$.programid.$error" class="has-error">{{ v$.programid.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="progname" class="control-label">{{ labels.progname_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.progname.$error}">
              <input type="text" ref="progname" v-model="localData.progname" id="progname" name="progname" class="form-control input-md" maxlength="50" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.progname.$error" class="has-error">{{ v$.progname.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="prognameth" class="control-label">{{ labels.prognameth_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.prognameth.$error}">
              <input tyep="text" ref="prognameth" v-model="localData.prognameth" id="prognameth" name="prognameth" class="form-control input-md" maxlength="50" />
              <label class="required">*</label> 
            </div>
            <span v-if="v$.prognameth.$error" class="has-error">{{ v$.prognameth.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-5">
            <label for="product" class="control-label">{{ labels.product_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.product.$error}">
              <select ref="product" v-model="localData.product" class="form-control input-md">
                <option value=""></option>
                <option v-for="item in dataCategory.tprod" :key="item.id" :value="item.id">{{item.text}}</option>
              </select>
              <label class="required">*</label>
            </div>
            <span v-if="v$.product.$error" class="has-error">{{ v$.product.$errors[0].$message }}</span>
          </div>
          <div class="col-height col-md-5">
            <label for="progtype" class="control-label">{{ labels.progtype_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.progtype.$error}">
              <select ref="progtype" v-model="localData.progtype" class="form-control input-md">
                <option v-for="item in dataCategory.tkprogtype" :key="item.id" :value="item.id">{{item.text}}</option>
              </select>
              <label class="required">*</label>
            </div>
            <span v-if="v$.progtype.$error" class="has-error">{{ v$.progtype.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-5">
            <label for="progsystem" class="control-label">{{ labels.progsystem_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.progsystem.$error}">
              <select ref="progsystem" v-model="localData.progsystem" class="form-control input-md">
                <option v-for="item in dataCategory.tkprogsystem" :key="item.id" :value="item.id">{{item.text}}</option>
              </select>
              <label class="required">*</label>
            </div>
            <span v-if="v$.progsystem.$error" class="has-error">{{ v$.progsystem.$errors[0].$message }}</span>
          </div>
          <div class="col-height col-md-5">
            <label for="appstype" class="control-label">{{ labels.appstype_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.appstype.$error}">
              <select ref="appstype" v-model="localData.appstype" class="form-control input-md">
                <option v-for="item in dataCategory.tkappstype" :key="item.id" :value="item.id">{{item.text}}</option>
              </select>
              <label class="required">*</label>
            </div>
            <span v-if="v$.appstype.$error" class="has-error">{{ v$.appstype.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="shortname" class="control-label">{{ labels.shortname_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.shortname.$error}">
              <input ref="shortname" type="text" v-model="localData.shortname" id="shortname" class="form-control input-md" maxlength="50" />
              <label class="required">*</label>
            </div>
            <span v-if="v$.shortname.$error" class="has-error">{{ v$.shortname.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="shortnameth" class="control-label">{{ labels.shortnameth_label }}</label>
            <div class="input-group has-validation" :class="{'has-error': v$.shortnameth.$error}">
              <input ref="shortnameth" type="text" v-model="localData.shortnameth" id="shortnameth" class="form-control input-md" maxlength="50" />
              <label class="required">*</label>
            </div>
            <span v-if="v$.shortnameth.$error" class="has-error">{{ v$.shortnameth.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="description" class="control-label">{{ labels.description_label }}</label>
            <input ref="description" type="text" v-model="localData.description" id="description" class="form-control input-md" maxlength="100" />
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="parameters" class="control-label">{{ labels.parameters_label }}</label>
            <input ref="parameters" type="text" v-model="localData.parameters" id="parameters" class="form-control input-md" maxlength="50" />
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-10">
            <label for="progpath" class="control-label">{{ labels.progpath_label }}</label>
            <input ref="progpath" type="text" v-model="localData.progpath" id="progpath" class="form-control input-md" maxlength="100" />
          </div>
        </div>
        <div class="row row-height">
          <div class="col-height col-md-6">
            <label class="control-label">{{ labels.iconstyle_label }}</label>
						<div ref="iconstyleswitcher" id="iconstyleswitcher"></div>							
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-5 col-height" id="iconfilelayer">
            <label class="control-label">{{ labels.iconfile_label }}</label>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-1"></div>
          <div class="col-md-9 col-height">
            <img id="iconfileimage" width="128px" height="128px" :src="getIconImage" alt="Program Image"/>
          </div>
        </div>
        <input type="hidden" id="iconstyle" v-model="localData.iconstyle" />
    </template>
    <template v-slot:footer>
      <button ref="savebutton" id="savebutton" class="btn btn-dark btn-sm" @click="saveClick" v-if="insertMode"><em class="fa fa-save fa-btn-icon"></em>{{ labels.save_button }}</button>
      <button ref="updatebutton" id="updatebutton" class="btn btn-dark btn-sm" @click="updateClick" v-if="updateMode"><em class="fa fa-save fa-btn-icon"></em>{{ labels.update_button }}</button>
      <button class="btn btn-dark btn-sm" data-dismiss="modal"><em class="fa fa-close fa-btn-icon"></em>{{ labels.cancel_button }}</button>
    </template>
  </DialogForm>
</template>
<script>
import { ref, computed, watch } from 'vue';
import { useVuelidate } from '@vuelidate/core';
import { required, helpers } from '@vuelidate/validators';
import $ from "jquery";
import { DEFAULT_CONTENT_TYPE, getApiUrl, getImgUrl, disableControls }  from '@willsofts/will-app';
import { startWaiting, stopWaiting, submitFailure, detectErrorResponse }  from '@willsofts/will-app';
import { confirmUpdate, confirmSave, confirmDelete, successbox, serializeParameters } from '@willsofts/will-app';
import DialogForm from './DialogForm.vue';

const defaultData = {
  programid: '',
  progname: "",
  prognameth: "",
  product: "",
  progtype: "E",
  progsystem: "F",
  appstype: "W",
  shortname: "",
  shortnameth: "",
  description: "",
  parameters: "",
  progpath: "",
  iconfile: "",
  iconstyle: "",
};

export default {
  components: {
    DialogForm
  },
  props: {
    modes: Object,
    labels: Object,
    dataCategory: Object
  },
  emits: ["data-saved","data-updated","data-deleted"],
  setup(props) {
    const mode = ref({action: "new", ...props.modes});
    const localData = ref({ ...defaultData }); 
    const disabledKeyField = ref(false);
    const reqalert = ref(props.labels.empty_alert);
    const requiredMessage = () => {
      return helpers.withMessage(reqalert, required);
    }
    const validateRules = computed(() => { 
      return {
        programid: { required: requiredMessage() },
        progname: { required: requiredMessage() },
        prognameth: { required: requiredMessage() },
        product: { required: requiredMessage() },
        progtype: { required: requiredMessage() },
        progsystem: { required: requiredMessage() },
        appstype: { required: requiredMessage() },
        shortname: { required: requiredMessage() },
        shortnameth: { required: requiredMessage() },
      } 
    });
    const v$ = useVuelidate(validateRules, localData, { $lazy: true, $autoDirty: true });
    return { mode, v$, localData, disabledKeyField, reqalert };
  },
  created() {
    watch(this.$props, (newProps) => {      
      this.reqalert = newProps.labels.empty_alert;
    });
  },
  computed: {
    insertMode() {
      return this.mode.action=="insert" || this.mode.action=="new";
    },
    updateMode() {
      return this.mode.action=="update" || this.mode.action=="edit";
    },
    getIconImage() {
      return this.localData.iconfile && this.localData.iconfile.trim().length > 0 ? getImgUrl()+"/img/apps/"+this.localData.iconfile : getImgUrl()+"/img/apps/apps.png";
    },
  },
  mounted() {
    this.$nextTick(function () {
      $("#modaldialog_layer").find(".modal-dialog").draggable();
      $("#iconstyleswitcher").styleswitcher({$styleInput: $("#iconstyle"), width: 210, styleURL : getApiUrl()+"/api/style/category" });	
    });
  },
  methods: {
    reset(newData,newMode) {
      if(newData) this.localData = {...newData};
      if(newMode) this.mode = {...newMode};
    },
    submit() {      
      this.$emit('update:formData', this.localData);
    },
    async saveClick() {
      console.log("click: save");
      console.log("localData",this.localData);
      disableControls($("#savebutton"));
      let valid = await this.validateForm();
      if(!valid) return;
      this.startSaveRecord();
    },
    async updateClick() {
      console.log("click: update");
      console.log("localData",this.localData);
      disableControls($("#updatebutton"));
      let valid = await this.validateForm();
      if(!valid) return;
      this.startUpdateRecord();
    },
    async validateForm(focusing=true) {
      const valid = await this.v$.$validate();
      console.log("validate form: valid",valid);
      console.log("error:",this.v$.$errors);
      if(!valid) {
        if(focusing) {
          this.focusFirstError();
        }
        return false;
      }
      return true;
    },
    focusFirstError() {
      if(this.v$.$errors && this.v$.$errors.length > 0) {
        let input = this.v$.$errors[0].$property;
        let el = this.$refs[input];
        if(el) el.focus(); //if using ref
        else $("#"+input).trigger("focus"); //if using id
      }
    },
    showDialog() {
      //$("#modaldialog_layer").modal("show");
      $(this.$refs.dialogForm.$el).modal("show");
    },  
    hideDialog() {
      //$("#modaldialog_layer").modal("hide");
      $(this.$refs.dialogForm.$el).modal("hide");
    },
    resetRecord() {
      //reset to default data 
      this.reset(defaultData,{action:"insert"});
      //reset validator
      this.v$.$reset();
      //enable key field
      this.disabledKeyField = false;
    },
    startInsertRecord() {
      this.resetRecord();
      this.showDialog();
      $("#iconstyleswitcher").styleupdate();
    },
    startSaveRecord() {
      confirmSave(() => {
        this.saveRecord(this.localData);
      });
    },
    startUpdateRecord() {
      confirmUpdate(() => { 
        this.updateRecord(this.localData);
      });
    },
    startDeleteRecord(dataKeys) {
      confirmDelete(Object.values(dataKeys),() => {
        this.deleteRecord(dataKeys);
      });
    },
    saveRecord(dataRecord) {
        let jsondata = {ajax: true};
        let formdata = serializeParameters(jsondata,dataRecord);
        startWaiting();
        $.ajax({
          url: getApiUrl()+"/api/sfte001/insert",
          data: formdata.jsondata,
          headers : formdata.headers,
          type: "POST",
          dataType: "json",
          contentType: DEFAULT_CONTENT_TYPE,
          error : function(transport,status,errorThrown) {
            console.error("error: status",status,"errorThrown",errorThrown);
            submitFailure(transport,status,errorThrown);
          },
          success: (data) => {
            stopWaiting();
            console.log("success",data);
            if(detectErrorResponse(data)) return;
            successbox(() => {
              //reset data for new record insert
              this.resetRecord();
              setTimeout(() => this.$refs.programid.focus(),100);
            });
            this.$emit('data-saved',dataRecord,data);
          }
      });
    },
    updateRecord(dataRecord) {
        let jsondata = {ajax: true};
        let formdata = serializeParameters(jsondata,dataRecord);
        startWaiting();
        $.ajax({
          url: getApiUrl()+"/api/sfte001/update",
          data: formdata.jsondata,
          headers : formdata.headers,
          type: "POST",
          dataType: "json",
          contentType: DEFAULT_CONTENT_TYPE,
          error : function(transport,status,errorThrown) {
            console.error("error: status",status,"errorThrown",errorThrown);
            submitFailure(transport,status,errorThrown);
          },
          success: (data) => {
            stopWaiting();
            console.log("success",data);
            if(detectErrorResponse(data)) return;
            successbox(() => {
              this.hideDialog();
            });
            this.$emit('data-updated',dataRecord,data);
          }
      });
    },
    retrieveRecord(dataKeys) {
      let jsondata = {ajax: true};
      let formdata = serializeParameters(jsondata,dataKeys);
      startWaiting();
      $.ajax({
        url: getApiUrl()+"/api/sfte001/retrieve",
        data: formdata.jsondata,
        headers : formdata.headers,
        type: "POST",
        dataType: "json",
        contentType: DEFAULT_CONTENT_TYPE,
        error : function(transport,status,errorThrown) {
          console.error("retrieveRecord: error: status",status,"errorThrown",errorThrown);
          submitFailure(transport,status,errorThrown);
        },
        success: (data) => {
          stopWaiting();
          console.log("retrieveRecord: success",data);
          if(data.body.dataset) {
            this.reset(data.body.dataset,{action:"edit"});
            this.v$.$reset();
            this.disabledKeyField = true;
            this.showDialog();
            $("#iconstyleswitcher").styleupdate(this.localData.iconstyle);
          }
        }
      });	
    },
    deleteRecord(dataKeys) {
      let jsondata = {ajax: true};
      let formdata = serializeParameters(jsondata,dataKeys);
      startWaiting();
      $.ajax({
        url: getApiUrl()+"/api/sfte001/remove",
        data: formdata.jsondata,
        headers : formdata.headers,
        type: "POST",
        dataType: "json",
        contentType: DEFAULT_CONTENT_TYPE,
        error : function(transport,status,errorThrown) {
          console.error("deleteRecord: error: status",status,"errorThrown",errorThrown);
          submitFailure(transport,status,errorThrown);
        },
        success: (data) => {
          stopWaiting();
          console.log("deleteRecord: success",data);
          if(detectErrorResponse(data)) return;
          successbox();
          this.$emit('data-deleted',dataKeys,data);
        }
      });	
    },
  }
};
</script>
