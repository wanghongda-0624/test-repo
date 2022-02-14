/**
 * 资源申请
 */
<template>
  <div>
    <p>Cloud Provider</p>
    <el-select v-model="value" placeholder="Select">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
    <p>Tenant Name</p>
    <el-input
      placeholder="Please input"
      v-model="input"
      class="input"
    ></el-input>
    <p>Association Account</p>
    <el-input
      placeholder="Please input"
      v-model="input"
      class="input"
    ></el-input>
    <p>Bill Owner</p>
    <el-input
      placeholder="Please input"
      v-model="input"
      class="input"
    ></el-input>
    <p>Resource Stage</p>
    <el-input
      placeholder="Please input"
      v-model="input"
      class="input"
    ></el-input>
    <p></p>
    <el-button class="preBtn" @click="next">Previous</el-button>
    <el-button class="nextBtn" @click="next">Next</el-button>
  </div>
</template>

<script>
import { deptList, deptSave, deptDelete } from "../../api/userMG";
import Pagination from "../../components/Pagination";
export default {
  data() {
    return {
      active: 0,
      options: [
        {
          value: "Option1",
          label: "Option1",
        },
        {
          value: "Option2",
          label: "Option2",
        },
        {
          value: "Option3",
          label: "Option3",
        },
        {
          value: "Option4",
          label: "Option4",
        },
        {
          value: "Option5",
          label: "Option5",
        },
      ],
      value: "",
    };
  },
};
</script>

<style scoped>
.steps {
  margin-top: 15px;
}
.input {
  width: 30%;
}
.nextBtn {
  margin-top: 10px;
  margin-left: 900px;
}
</style>

 
 