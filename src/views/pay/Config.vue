/**
 * 支付管理 支付配置
 */
<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Best Practice</el-breadcrumb-item>
    </el-breadcrumb>
    <el-row
      style="margin-top: 3%" type="flex" :span="8" v-for="(o, index) in 1" :key="o" :offset="index > 0 ? 2 : 0"
    >
      <el-card :body-style="{ padding: '0px' }" class="card" v-for="items in datalist">
        <img :src="items.src" class="image" />
        <div style="padding: 14px">
          <span>{{items.sdesc}}</span>
          <div class="bottom clearfix">
            <time class="time">{{ currentDate }}</time>
            <!-- <el-button type="text" class="button">Operating</el-button> -->
            <el-link :underline="false" :href="items.href" class="button">Operating</el-link>
          </div>
        </div>
      </el-card>
    </el-row>
    <el-row
      style="margin-top: 3%" type="flex" :span="8" v-for="(o, index) in 1" :key="o" :offset="index > 0 ? 2 : 0"
    >
      <el-card :body-style="{ padding: '0px' }" class="card" v-for="items in datalist2">
        <img :src="items.src" class="image" />
        <div style="padding: 14px">
          <span>{{items.sdesc}}</span>
          <div class="bottom clearfix">
            <time class="time">{{ currentDate }}</time>
            <el-button type="text" class="button">Operating</el-button>
          </div>
        </div>
      </el-card>
    </el-row>
  </div>
</template>

<script>
import { ConfigList, ConfigSave, ConfigDelete } from "../../api/payMG";
import Pagination from "../../components/Pagination";
export default {
  data() {
    return {
      datalist: [
        {
          id: "carousel-item-1",
          src: require("../../assets/img/micro.png"),
          sdesc: "Micro-service",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/AKS%20Best%20Practices%20Deepdive%20for%20BMW.pdf?AccessKeyId=8IFV4ZOO2JX0OI60KO4O&Expires=1644912501&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00ig-jzYQrjBV5TTpH1kQ8T-YmxzcWK2lkThZLcMCORvMTcv0slUCSEP3lBv0y_Uo3_rL0jGwCQL4WgnFcRulgAQCHFyr-OyVR1v0w_5YS7QYc9-3XnWyDMKHlegItPYF4B-bFGd_TlpaufrwZUbTwma6_LzFPVdImbVt8P3wpFaVT09iVmc900nA_NGHKHipX0A94MtPs7pffcRQ-S8OkpuDdMHc30wXLFIAN2fnoAp1BWX3iTWNFbRf6bIhxWAQk9KELjva23zUKb6kdLICRBIC7SHyrPLA4Zw5z6JWnsToAFvnLqadK1sthTmV0vvwXywjCSbihZoOlRrRgKeDlBmAYdisQ3SaMNFBvwlmiE520Wae1bZK6Z6hb9EzBZ2km2pjPXM4IUT_WpDbMQDaJbzFbtZg-i0R2aZ08_mbNtBqTSWKuR1gYAhSymm2syo11HRIQcGg05cC1LOl6JNwy0YqNiqgC9vxHIFf9NJ6BxNZ-n70fQCBN1pRpo6U2HwLICMNywCXrSEcpLwArbJ8w8VBJo0JeSFQtyyemvD4-Q-kWeld_mb_R5euo9mSiNwumksJ3onmI7jGVFnffOjv3UnD7PMmIkZfdOLNIe9bQ6MI8bhMNLV5EqN6Dcujc8w2t2UueAyt7IGwA_dK1qUhqiRxSo7M4raXnQ2Ip7-lRsyu7HPmsVKItloxsh06UJJxkKyPpPdbLHRUSPqWAK0x5HFtUU5CHoBFDs2rZbWkOiJgC1o5GUN3bHgPgu7DxE7DQDkqkg_Mex7tSDr1uoh1mnto%3D&Signature=bsF11m0qDOksqonlL3bpeaUmtzE%3D",
        },
        {
          id: "carousel-item-2",
          src: require("../../assets/img/baobiao.png"),
          sdesc: "Data Visualization",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/2022-gartner-top-strategic-technology-trends-ebook-cn.pdf?AccessKeyId=LRKSDIEEK8CQZ1ST22N0&Expires=1643090277&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00igGI6PXn-M4ffEBtUQ9LLRdb1yMgvWJrWWD0IhIVZg0oswNptEQv18x2mnxi7f1-2PZFTQ9XJJf8dEJ2LQsbGZ3EqwKdZahuQvN4O7iICgqBBd6i_aXFKOP-ZTb7Z_kpYHLCjCGWEh58RXyeeOatPDv-qLk3eTHasu2vU7CztjmeuX6WHvzXyxckzNn5g_0LuyOKVW1KClIQwQ9Qtss_p-6rTJgmGoo7j2Xuch7bQ0wrxRjDmuCGv9tChAGcLwkN1zexpRbBK7PmZTT4qbBbpsil_HTROqX0-vKSZAn7bsNr_6-KCc9MrluTAykcKR_zAyNcbg3GNrl4q9qNBx60772IHPplnktPMS17Ito99skmnPjJw-tOYlMbBpqu0kXLMXpWVgFjk7PCU5SxUZLssHqHh9Es5HHjW_9UjQyxmjCFH0Dwvgjq5x9NCGmPn184gk-pvcZThkQPz7unwckM0WuGX9RJ_pm9HWKyxh2-PvIqgaH-Jyg1Nj2zQOwH1pr3ldDXh1x1qj17iRXbi3eV3FjeQpYhWLKUvEsCDHibmUqn8zVo0kJUWGp4gO7w6FgsTu1cOOmjV2hXFIiQDy_swbVFB-hgTTi0P8o9d5vAuQR8AYg0f2-tZ8XR2fkHP4S_0Zwc2AtcINy17tNQjZEtNZLwjOX8JeCG-ATcz0Jh_hBDri9_EMo-4inn6kcIDzpCicDJo_TFIrFLURjP7sqF0nygHgwQ6ZRiDGasT49fe7TOYBsGslSKJxsE9rmuuIWTlOhDwUhvv0ivvKGvTIIqH44%3D&Signature=msmzYUo5eSQvMIChXE12Q0HSgQw%3D",
        },
        {
          id: "Basic Springboot",
          src: require("../../assets/img/springboot.png"),
          sdesc: "Basic Springboot",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/prisma-cloud-for-alibaba-cloud-datasheet.pdf?AccessKeyId=0QUCYGDO1B00ZP8WTLJW&Expires=1643090832&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00irekuV3NGBWpby9e40r0oVKyykmJUg55nR4rxziSQQMNeeWC5zoLQiomJ4OAjKlFdIsioAMdfESEw4zWPm6zwe4OMYzMk3M4H2d27eMrkWDO7BpBFaB7y2xV8Kfpov6ALyPMJ962wTCJohN9bRqH5TL8hyj9rcgNe1-9q5wqsNd5yO4TbSdgCzze5lJBf0-gKixzqcs9xnlOFfrucB4STdnHl_IqcxIuNn6Fup0dm3GPTg59DPuc9A4pFVv-nQhNjZp3cp2D6g_OO2dFAW36wOSELq6s92g5dCJ55kT6yfnCHGhrTlABwYo19nupFdbsAkr44MNdYwroB56alaCh7k2XdRIFJgdpE83FGhAa5g6oTPWXtXoZ-q7xBLZskLvLL4A4fCxBpMx9FkNXA3sEQi9YjIwmgZsYjf_q_lMCL8AsYgr7EmuSLuv3WDCr2Bs5AqKi0vnOLSUSay0E6SeCZDX3049K0lvgJcm2Bk_b01LeoRhlUvaQQswI5Tu5HjsOmZacYq__xreex9zJa2gPwbqbJ7_sSaVASNsZFlCxR3LpnDPRi4qctVxHNZQI1BNBNPkAg3Kpjr5TTAZi5vnCgx4ugF9tN9S9ebLlFxrBUYim4uP6iWB0xIHrGhgkuX01SmCYGmXxtjfF5Tv0uxmXtefU7yz_xuNDDIpmPnAskOK0WS1KzSkGnz167URuTMblo0eOGFmKdpRJxxsH1E5uxKA0-hDGqOGMAKcLP4IJkpTvgO4u96ASul__KejGoHH1Hil7uqCeWpVwzh4Mt24b3gg%3D&Signature=dV7WZzNWTGL2/uxgbLfKcpW06ro%3D",
        },
      ],
      datalist2: [
        {
          id: "carousel-item-1",
          src: require("../../assets/img/function.png"),
          sdesc: "Functions&Logics App",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/%E9%98%BF%E9%87%8C%E4%BA%91%E7%99%BD%E7%9A%AE%E4%B9%A6.pdf?AccessKeyId=25NVRDFMMN3NWTISQ8EK&Expires=1643088745&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00ipXJYzHHwqCR2FQP3Agb_JzRp2XlzMbWGA7eImTbypqNosV2lBT286Bxk9lSxcWTicXTWJxMKbU4vTYNWZOmF0uPxt-Y_jiHNTXx4vWtgwm5tEHCUqQxkra9MUKsvQ4vFUP4iCKm1OWXWyMgaRHPtm43WjGng4WrMaNaLUfecOZHL9LMcIZtqWFLcv_VkKgwKW5cQ0FaNiaw7-VGiN3T1pctlxz0Z9Oz12rEsP_f1-6CIvgCcFVKGLvYryrdo6Mx6_n6V5c3JHVJ9yu15gAQwdSdGCQpo5QNhHHGpi0oF4B4b6t4ne_2wlFw0nlM4jEt8sETfRYTnJCifN-zbG1aiOOaZoSi40039MVaQysctVId5g1sTOMR0DpmLgWHJNMe2Dxwa7qmqXrmoLNd0LRv93OBos8H22aIBZn60Mn0GgYgfDLUI7KZ1YCwVzRhma1o9YpyALJ3uBJJggN4KsWY7vSwYDozX35EhZRhDw-E502GrbkBXCR052CpaplS0FkaiXK4a08U9Yod9o0gXGbZQctf9ucfEBxS-wQilNesDYfJznOnOBnbMER_vqzsze3jEzt22kO_VgGu8ZikWusWHAk5YCDSUg1YGJbw16jerDZhEBiJKoWVLo9CSa07vLCicmwRRnlEKIQV2rlYE6rp6SLK8WPhGDUvR_2a4aK8S1-HYJg8pGUV03dCCEaICNljwQz5KcBPk--OV8RKlSqLtG25c7waDUwV2c9lOY98ohskr_kvNUNAWbEjkZ2vqTNkeQm_R-Iu61SvzYIJhTeaXaE%3D&Signature=9k67%2BtiHQCQdNc795L8RTcDn6tc%3D",
        },
        {
          id: "carousel-item-2",
          src: require("../../assets/img/batch.png"),
          sdesc: "Batch&High Performance Computing",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/2022-gartner-top-strategic-technology-trends-ebook-cn.pdf?AccessKeyId=LRKSDIEEK8CQZ1ST22N0&Expires=1643090277&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00igGI6PXn-M4ffEBtUQ9LLRdb1yMgvWJrWWD0IhIVZg0oswNptEQv18x2mnxi7f1-2PZFTQ9XJJf8dEJ2LQsbGZ3EqwKdZahuQvN4O7iICgqBBd6i_aXFKOP-ZTb7Z_kpYHLCjCGWEh58RXyeeOatPDv-qLk3eTHasu2vU7CztjmeuX6WHvzXyxckzNn5g_0LuyOKVW1KClIQwQ9Qtss_p-6rTJgmGoo7j2Xuch7bQ0wrxRjDmuCGv9tChAGcLwkN1zexpRbBK7PmZTT4qbBbpsil_HTROqX0-vKSZAn7bsNr_6-KCc9MrluTAykcKR_zAyNcbg3GNrl4q9qNBx60772IHPplnktPMS17Ito99skmnPjJw-tOYlMbBpqu0kXLMXpWVgFjk7PCU5SxUZLssHqHh9Es5HHjW_9UjQyxmjCFH0Dwvgjq5x9NCGmPn184gk-pvcZThkQPz7unwckM0WuGX9RJ_pm9HWKyxh2-PvIqgaH-Jyg1Nj2zQOwH1pr3ldDXh1x1qj17iRXbi3eV3FjeQpYhWLKUvEsCDHibmUqn8zVo0kJUWGp4gO7w6FgsTu1cOOmjV2hXFIiQDy_swbVFB-hgTTi0P8o9d5vAuQR8AYg0f2-tZ8XR2fkHP4S_0Zwc2AtcINy17tNQjZEtNZLwjOX8JeCG-ATcz0Jh_hBDri9_EMo-4inn6kcIDzpCicDJo_TFIrFLURjP7sqF0nygHgwQ6ZRiDGasT49fe7TOYBsGslSKJxsE9rmuuIWTlOhDwUhvv0ivvKGvTIIqH44%3D&Signature=msmzYUo5eSQvMIChXE12Q0HSgQw%3D",
        },
        {
          id: "Basic Springboot",
          src: require("../../assets/img/data.png"),
          sdesc: "Data Security Application",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/prisma-cloud-for-alibaba-cloud-datasheet.pdf?AccessKeyId=0QUCYGDO1B00ZP8WTLJW&Expires=1643090832&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00irekuV3NGBWpby9e40r0oVKyykmJUg55nR4rxziSQQMNeeWC5zoLQiomJ4OAjKlFdIsioAMdfESEw4zWPm6zwe4OMYzMk3M4H2d27eMrkWDO7BpBFaB7y2xV8Kfpov6ALyPMJ962wTCJohN9bRqH5TL8hyj9rcgNe1-9q5wqsNd5yO4TbSdgCzze5lJBf0-gKixzqcs9xnlOFfrucB4STdnHl_IqcxIuNn6Fup0dm3GPTg59DPuc9A4pFVv-nQhNjZp3cp2D6g_OO2dFAW36wOSELq6s92g5dCJ55kT6yfnCHGhrTlABwYo19nupFdbsAkr44MNdYwroB56alaCh7k2XdRIFJgdpE83FGhAa5g6oTPWXtXoZ-q7xBLZskLvLL4A4fCxBpMx9FkNXA3sEQi9YjIwmgZsYjf_q_lMCL8AsYgr7EmuSLuv3WDCr2Bs5AqKi0vnOLSUSay0E6SeCZDX3049K0lvgJcm2Bk_b01LeoRhlUvaQQswI5Tu5HjsOmZacYq__xreex9zJa2gPwbqbJ7_sSaVASNsZFlCxR3LpnDPRi4qctVxHNZQI1BNBNPkAg3Kpjr5TTAZi5vnCgx4ugF9tN9S9ebLlFxrBUYim4uP6iWB0xIHrGhgkuX01SmCYGmXxtjfF5Tv0uxmXtefU7yz_xuNDDIpmPnAskOK0WS1KzSkGnz167URuTMblo0eOGFmKdpRJxxsH1E5uxKA0-hDGqOGMAKcLP4IJkpTvgO4u96ASul__KejGoHH1Hil7uqCeWpVwzh4Mt24b3gg%3D&Signature=dV7WZzNWTGL2/uxgbLfKcpW06ro%3D",
        },
      ],
    };
  },
  // 注册组件
  components: {
    Pagination,
  },
  /**
   * 数据发生改变
   */

  /**
   * 创建完毕
   */
  created() {},

  /**
   * 里面的方法只有被调用才会执行
   */
  methods: {
    // 获取公司列表
  },
  // 分页插件事件
};
</script>

<style scoped>
.time {
  font-size: 13px;
  color: #999;
}

.bottom {
  margin-top: 13px;
  line-height: 12px;
}

.button {
  padding: 0;
  float: right;
}

.image {
  width: 100%;
  display: block;
  height: 150px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}

.clearfix:after {
  clear: both;
}
.card {
  height: 30%;
  width: 30%;
  margin-left: 3%;
}
</style>

 
 