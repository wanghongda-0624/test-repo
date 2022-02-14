/**
 * 资源申请
 */
<template>
  <div>
    <!-- 面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Resource Apply</el-breadcrumb-item>
    </el-breadcrumb>
    <el-steps :active="active" finish-status="success" class="steps">
      <el-step title="App Information" />
      <el-step title="Cloud Information" />
      <el-step title="Others" />
      <el-step title="Finish" />
    </el-steps>
    <el-form
      ref="dataForm"
      :rules="formRules"
      label-position="left"
      label-width="100px"
      style="width: 400px; margin-left: 30px; margin-top: 30px"
    >
      <div v-show="active == 0">
        <el-form-item label="App Name" class="labeltext">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="LoS">
          <el-select v-model="form.region" placeholder="please select your LoS">
            <el-option label="Assurance" value="shanghai"></el-option>
            <el-option label="Advisory" value="beijing"></el-option>
            <el-option label="Tax" value="shanghai"></el-option>
            <el-option label="OFS" value="beijing"></el-option>
            <el-option label="FCS" value="beijing"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Duration">
          <el-col :span="11">
            <el-date-picker
              type="date"
              placeholder="Start date"
              v-model="form.date1"
              style="width: 100%"
            ></el-date-picker>
          </el-col>
          <el-col class="line" :span="2">--</el-col>
          <el-col :span="11">
            <el-date-picker
              type="date"
              placeholder="End date"
              v-model="form.date1"
              style="width: 100%"
            ></el-date-picker>
          </el-col>
        </el-form-item>
        <el-form-item label="Internal">
          <el-switch v-model="form.delivery"></el-switch>
        </el-form-item>
        <el-form-item label="App type">
          <el-checkbox-group v-model="form.type">
            <el-checkbox label="Online activities" name="type"></el-checkbox>
            <el-checkbox label="Promotion activities" name="type"></el-checkbox>
            <el-checkbox label="Offline activities" name="type"></el-checkbox>
            <el-checkbox
              label="Simple brand exposure"
              name="type"
            ></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-form-item label="Resources">
          <el-radio-group v-model="form.resource">
            <el-radio label="Sponsor"></el-radio>
            <el-radio label="Venue"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="Descriptions">
          <el-input type="textarea" v-model="form.desc"></el-input>
        </el-form-item>
      </div>
      <div v-show="active == 1">
        <el-form-item label="Tenant Name">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="Provider">
          <el-select
            v-model="form.region"
            placeholder="please select cloud provider"
          >
            <el-option label="Zone one" value="shanghai">
              <label> Ali Cloud</label>
              <img
                src="../../assets/img/阿里云.svg"
                width="25px"
                height="15px"
                class="hwicon"
                @click="openLink()"
              />
            </el-option>
            <el-option label="Zone two" value="beijing">
              <label> Huawei Cloud</label>
              <img
                src="../../assets/img/华为1.svg"
                width="25px"
                height="25px"
                class="hwicon"
                @click="openLink()"
              />
            </el-option>
            <el-option label="Zone two" value="beijing">
              <label> Tencent Cloud</label>
              <img
                src="../../assets/img/tx.svg"
                width="25px"
                height="25px"
                class="hwicon"
                @click="openLink()"
              />
            </el-option>
            <el-option label="Zone two" value="beijing">
              <label>Microsoft Azure</label>
              <img
                src="../../assets/img/Azure.svg"
                width="25px"
                height="25px"
                class="hwicon"
                @click="openLink()"
              />
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Tenant Owner">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="Contact No.">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="Public Access">
          <el-select
            v-model="form.region"
            placeholder="please select access way"
          >
            <el-option label="Zone one" value="shanghai"></el-option>
            <el-option label="Zone two" value="beijing"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Resources">
          <el-radio-group v-model="form.resource">
            <el-radio label="Sponsor"></el-radio>
            <el-radio label="Venue"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="Descriptions">
          <el-input type="textarea" v-model="form.desc"></el-input>
        </el-form-item>
      </div>
      <div v-show="active == 2">
        <el-form-item label="Resource As Code">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="LoS">
          <el-select
            v-model="form.region"
            placeholder="please select your zone"
          >
          </el-select>
        </el-form-item>
        <el-form-item label="Duration">
          <el-col :span="11">
            <el-date-picker
              type="date"
              placeholder="Pick a date"
              v-model="form.date1"
              style="width: 100%"
            ></el-date-picker>
          </el-col>
          <el-col class="line" :span="2">--</el-col>
          <el-col :span="11">
            <el-time-picker
              placeholder="Pick a time"
              v-model="form.date2"
              style="width: 100%"
            ></el-time-picker>
          </el-col>
        </el-form-item>
        <el-form-item label="Internal">
          <el-switch v-model="form.delivery"></el-switch>
        </el-form-item>
        <el-form-item label="Activity type">
          <el-checkbox-group v-model="form.type">
            <el-checkbox label="Online activities" name="type"></el-checkbox>
            <el-checkbox label="Promotion activities" name="type"></el-checkbox>
            <el-checkbox label="Offline activities" name="type"></el-checkbox>
            <el-checkbox
              label="Simple brand exposure"
              name="type"
            ></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-form-item label="Resources">
          <el-radio-group v-model="form.resource">
            <el-radio label="Sponsor"></el-radio>
            <el-radio label="Venue"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="Descriptions">
          <el-input type="textarea" v-model="form.desc"></el-input>
        </el-form-item>
      </div>
      <div v-show="active == 3"></div>
    </el-form>

    <el-button
      v-if="active > 0"
      class="transfer-footer"
      slot="left-footer"
      @click="pre"
      >Previous</el-button
    >
    <el-button
      v-if="active < 4"
      class="transfer-footer"
      slot="right-footer"
      @click="next"
      >Next Step</el-button
    >
  </div>
</template>

<script>
import { deptList, deptSave, deptDelete } from "../../api/userMG";
import Pagination from "../../components/Pagination";
export default {
  data() {
    return {
      active: 0,
      form: {
        name: "",
        region: "",
        date1: "",
        date2: "",
        delivery: false,
        type: [],
        resource: "",
        desc: "",
      },
      value: "",
    };
  },

  created() {
    this.$store.state.showright = false
  },

  methods: {
    next() {
      if (this.active++ > 2) {
        this.active = 0;
        if ((this.active = 3)) {
          this.$alert("You have successfuly submited your request", "Success Information", {
            confirmButtonText: "OK",
            callback: action => {
              this.$router.push({ path: '/' })
          }
          });
        }
      }
    },
    pre() {
      if (this.active-- < 1) this.active = 1;
    },
  },
};
</script>

<style>
.steps {
  margin-top: 20px;
}
.input {
  width: 30%;
}
.transfer-footer {
  margin-left: 30px;
  padding: 12px 8px;
}
.nextBtn {
  margin-left: 840px;
}
.preBtn {
  margin-left: 700px;
}
.hwicon {
  /* margin-top:0px; */
}
.el-form-item__label{
  color: #000 !important;
  font-size: 16px;
}
</style>

 
 