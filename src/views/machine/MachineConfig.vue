/**
 * 支付管理 支付配置信息
 */
<template>
  <div>
    <!-- 面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Cloud Materials</el-breadcrumb-item>
    </el-breadcrumb>
    <!--列表-->
    <el-carousel :interval="4000" type="card" height="270px" class="carousel">
      <el-carousel-item v-for="item in imgLIst" :key="item.id">
        <img class="carousel_image_type" :src="item.src" />
        <!-- <p
          style="
            position: absolute;
            bottom: 0px;
            left: 0;
            background-color: white;
            opacity: 0.9;
            display: none;
            text-align: left;
            border-radius: 4px;
          "
          :class="item.id"
        >
          {{ item.desc }}
          <el-button
            style="line-height: 0"
            type="primary"
            @click.native="fadeInOrFadeOut(item.id)"
            >收起</el-button
          >
        </p> -->
        <p style="position: absolute; bottom: 0px; left: 10" :class="item.id">
          <el-link :underline="false" :href="item.href">{{
            item.sdesc
          }}</el-link>
        </p>
      </el-carousel-item>
    </el-carousel>
    <el-table :data="tableData" stripe style="width: 100%" @row-click="openLink">
      <el-table-column prop="date" label="Name" width="180"> </el-table-column>
      <el-table-column prop="name" label="Link" width="180"> 
        <img src="../../assets/img/link.svg" width="25px" height="25px"/>
      </el-table-column>
      <el-table-column prop="address" label="Description" > </el-table-column>
    </el-table>
  </div>
</template>

<script>
import {
  MachineConfigList,
  MachineConfigSave,
  MachineConfigDelete,
} from "../../api/payMG";
import Pagination from "../../components/Pagination";
export default {
  data() {
    return {
      imgLIst: [
        {
          id: "carousel-item-1",
          src: require("../../assets/img/GettyImages-1023021802.jpg"),
          sdesc: "Alicloud ACF阿里云白皮书",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/%E9%98%BF%E9%87%8C%E4%BA%91%E7%99%BD%E7%9A%AE%E4%B9%A6.pdf?AccessKeyId=TWCW69YWIL3RR5A4M8P7&Expires=1644912598&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00iqKJq9vnBuxTcnUTZuvdYhHcIY7QjElZCl7k6rMO8VK3c4GQ7WrmVkHrYFvZJkU8mTHwcswqgAu2Y_HN707u9pS-Bn-5FlIPpst1RBfv0EEjAanl63lopdWNbP-p1kud-RvrTHahS7j_KftOsdW7DImPQNguLPEQuLZi-LmUZtFYxnOnUOyRcXOiyMWFIBRZtvYHwSySXJ47F4Ha91JrL01oc05dJVewTIN_E_kNrpKXlmKCMdsvt8kddwYuFNqWPeGxl7F09UgPmVv2unkxO2lL9gI2SBd5pFPDlrA7UaD0AqFcwGLB-_wGOKXIwtW1g56q3NY_I2wa5pzRLq4JCtaS4nJ9EkNjMLq21CVzWFy4WIT9gLaM5fIoKkr1ZO8gdtRNM9wUzYSXwZ-yI_-GXU0Y7mzCzBPkhCNQnF1WL7iERuEQgEe0V2QokbSDmyhh31dryXAQsKrF4qFtNr5Ejq3ddfiGdiEuCcrygte7LZSejw7d0EY0NppMTA0mJTEwlcy_XZmyqDiqAjrkL6u-PbuLW0kCiTFBkah0hmA1aDPSle1srRZEkMnv2N8cKQQL4QOmftpsXQfCcWIHrXAZ2AP-GB25fjo3pBZ3yicLH9xw_fpcJZH4EL-Ycn70K4LWkQypTXoCxek4bJCFXje0P6QlqQyK0aW9x1P6ErkJQ91UdY7PZ3ihwu_Z4CbH2yjkdDd00dcGwIGCgC_DAgY6z9TIskTKzlYYY8QycW21AYVHkPDshg6Uhr3TZBya1OX1mZuapRB7HsI4_I-Xra6-cDs%3D&Signature=G8DG7TDie3t7SuUed%2B5jIJEEu6A%3D",
        },
        {
          id: "carousel-item-2",
          src: require("../../assets/img/GettyImages-1138192105.jpg"),
          sdesc: "Gartner魔力象限",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/2022-gartner-top-strategic-technology-trends-ebook-cn.pdf?AccessKeyId=LRKSDIEEK8CQZ1ST22N0&Expires=1643090277&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00igGI6PXn-M4ffEBtUQ9LLRdb1yMgvWJrWWD0IhIVZg0oswNptEQv18x2mnxi7f1-2PZFTQ9XJJf8dEJ2LQsbGZ3EqwKdZahuQvN4O7iICgqBBd6i_aXFKOP-ZTb7Z_kpYHLCjCGWEh58RXyeeOatPDv-qLk3eTHasu2vU7CztjmeuX6WHvzXyxckzNn5g_0LuyOKVW1KClIQwQ9Qtss_p-6rTJgmGoo7j2Xuch7bQ0wrxRjDmuCGv9tChAGcLwkN1zexpRbBK7PmZTT4qbBbpsil_HTROqX0-vKSZAn7bsNr_6-KCc9MrluTAykcKR_zAyNcbg3GNrl4q9qNBx60772IHPplnktPMS17Ito99skmnPjJw-tOYlMbBpqu0kXLMXpWVgFjk7PCU5SxUZLssHqHh9Es5HHjW_9UjQyxmjCFH0Dwvgjq5x9NCGmPn184gk-pvcZThkQPz7unwckM0WuGX9RJ_pm9HWKyxh2-PvIqgaH-Jyg1Nj2zQOwH1pr3ldDXh1x1qj17iRXbi3eV3FjeQpYhWLKUvEsCDHibmUqn8zVo0kJUWGp4gO7w6FgsTu1cOOmjV2hXFIiQDy_swbVFB-hgTTi0P8o9d5vAuQR8AYg0f2-tZ8XR2fkHP4S_0Zwc2AtcINy17tNQjZEtNZLwjOX8JeCG-ATcz0Jh_hBDri9_EMo-4inn6kcIDzpCicDJo_TFIrFLURjP7sqF0nygHgwQ6ZRiDGasT49fe7TOYBsGslSKJxsE9rmuuIWTlOhDwUhvv0ivvKGvTIIqH44%3D&Signature=msmzYUo5eSQvMIChXE12Q0HSgQw%3D",
        },
        {
          id: "carousel-item-3",
          src: require("../../assets/img/GettyImages-1025651972.jpg"),
          sdesc: "云安全Prisma",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/prisma-cloud-for-alibaba-cloud-datasheet.pdf?AccessKeyId=0QUCYGDO1B00ZP8WTLJW&Expires=1643090832&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00irekuV3NGBWpby9e40r0oVKyykmJUg55nR4rxziSQQMNeeWC5zoLQiomJ4OAjKlFdIsioAMdfESEw4zWPm6zwe4OMYzMk3M4H2d27eMrkWDO7BpBFaB7y2xV8Kfpov6ALyPMJ962wTCJohN9bRqH5TL8hyj9rcgNe1-9q5wqsNd5yO4TbSdgCzze5lJBf0-gKixzqcs9xnlOFfrucB4STdnHl_IqcxIuNn6Fup0dm3GPTg59DPuc9A4pFVv-nQhNjZp3cp2D6g_OO2dFAW36wOSELq6s92g5dCJ55kT6yfnCHGhrTlABwYo19nupFdbsAkr44MNdYwroB56alaCh7k2XdRIFJgdpE83FGhAa5g6oTPWXtXoZ-q7xBLZskLvLL4A4fCxBpMx9FkNXA3sEQi9YjIwmgZsYjf_q_lMCL8AsYgr7EmuSLuv3WDCr2Bs5AqKi0vnOLSUSay0E6SeCZDX3049K0lvgJcm2Bk_b01LeoRhlUvaQQswI5Tu5HjsOmZacYq__xreex9zJa2gPwbqbJ7_sSaVASNsZFlCxR3LpnDPRi4qctVxHNZQI1BNBNPkAg3Kpjr5TTAZi5vnCgx4ugF9tN9S9ebLlFxrBUYim4uP6iWB0xIHrGhgkuX01SmCYGmXxtjfF5Tv0uxmXtefU7yz_xuNDDIpmPnAskOK0WS1KzSkGnz167URuTMblo0eOGFmKdpRJxxsH1E5uxKA0-hDGqOGMAKcLP4IJkpTvgO4u96ASul__KejGoHH1Hil7uqCeWpVwzh4Mt24b3gg%3D&Signature=dV7WZzNWTGL2/uxgbLfKcpW06ro%3D",
        },
        {
          id: "carousel-item-4",
          src: require("../../assets/img/GettyImages-1032655290.jpg"),
          sdesc: "NGC云管平台",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/NGC%20Features%20Overview%20.pdf?AccessKeyId=I8TSU4WX896BH2HBGTOW&Expires=1643090396&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00itVDItksioY_AL5iAZF3tpe8SaeuTL85JUayrHR2I4uZ_aHNDvcf28nXoj4vX4L4DjqhzKU4MH5iP5CcQtD7PNc8ZnJUaIZqTYgXfxFGmac9bZVvkaLO0pZuFCCBrCfQWyjIWFJN-Ts74vanSLSPxBiXqsRfvc3zZ4Oqwdcr6aumtMMFzJ1mkyvk13tuHhdMhRgwkDaIDxBo1kenc1U06wUmfO7_HZM8EC7G08JQy3oLOimCACiFCFDdLMjC8TLpxRJnHJ7eqPWiXa_SpLjL137qYfWbtAz29gLP4ou-HvhzDQr9cc9RCC_btQbvr5mCMkKNet8sQVbrZD7SNYHoMKvg6_SzoEuJSFkDFzkE8gX9ldR2w8CXQ3fXZ6ZrJ6ceimev2HMtfEXd-KMXBVN-zliPXAJ3eOE9I0BkcLPlvojDmQ4xQJM3Ow3MuyOvB_HeU2Qpq9Ms56ZNhkk_7mHSv_c48eWEHhRdeGiwvw1FHPNYd-_N7QulRenVK6Y84N6CdEYlz-KuW6DddtGEncK1pLEOSvvCX2LJuKb9BRtWSzbUQBEtw6gHe7I6VfAyKv4trjmmLNtcM_CBOT3asYLq813c7jBPy2LKWSZ5Q40RFlNMERhbjEzbhNdWLbGiNC8iv7tVCW7DvipeVybQ0bCXBb2Dye6v7ijam6_F_TANHFq9oyZcXM_D9TV1r_HVfCab2yrjGc7GJAb3tgZApshbXxRlcSshAkk9qokQmpebRJJJDyE8nHa1dpOjYsrWpxb4FRkqyOwhWXYC9jucNy60x4U%3D&Signature=g6jTKmnvYG9l5o1Rc1c6xnSXyX0%3D",
        },
        {
          id: "carousel-item-5",
          src: require("../../assets/img/GettyImages-1032866658.jpg"),
          sdesc: "NGC微服务",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/NGC%20Platform%20-%20ServiceNow%20APIs%20%28Microservices%29.pdf?AccessKeyId=OFP3EA9MNLXOVH5D77HM&Expires=1643090465&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00ipZSKKdUT-HEbdWvlPjfITAocHq65Q3Z-ciw46TWOpy2U8bUJlkVYFhRxJDUEnHi13uZlp_h3xPFOtz8PllpGxlHMieNUIg-K6P2IkSKQLQy10wHqwpFW3Pbuz0abvSJmidgO3B41T3yFGoJ5IRq1wHkLy6TqYWpFIM98-E3Ik2-kJHIqUXZO2I8nzXA6tkMSZfLXo70MHo2ZoOuUbBfYhqE6SYO6G9Fo9fJ-vMembJgAyDXHWu_lZJ4Hp7C4mVw4vHN7MrP_ZYCvHUA6nMv5zvG_rbx-61CLeeLNseV3o-PK1dP4yucDOPm191_u66JXQqNk3CF0ZSJhqVOSWhONpNF73qeOy66WOmE4EYFmHs10VaxxQeJxEJQoKmivnzm9crLLGwNGBqOX0kTwyoW-dYEHLcWKIt0nnuYV1Ab0x-IiFRBo75lrqYAvc-lQrdP3xQsKiALVLMvb2jvfG1yqr1xZPU5LiQOHCOiMLv2o2_27icPKXqq87kSXzcbB1ij-pctWXOe_rdyB4rKWDMAux6EieITNsFDf8DASf52Xr2t_r4LUQNo7c3q_H7nygjr-tuFjAnQlyagYsGNz8YGDzKvgflbCdy3zoOjZZ-8Yq5CrQ3y88pMlnxed_B_UWY2eXpWAcRdXl21G6CA0KIxNZqPqeJp7jZJ4JmdDfeQ42xq1frk7rR-ze8u5d6cAvDJ2Oed9JOqXS-F_oOZXd2nNtoJ8_gH6eKLjlMCq3SPX1unllFA28cASDI59ikjJq4Mjp46l-NkXEslrblhMDIryfI%3D&Signature=8j0KXb/UYjgJ9zC/%2BIOWLLu8V/M%3D",
        },
        {
          id: "carousel-item-6",
          src: require("../../assets/img/GettyImages-1048702210.jpg"),
          sdesc: "NGC 工具链",
          href: "https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/NextGen%20Cloud%20Tooling%20Highlights.pdf?AccessKeyId=ZHCZTSA9RMMBY2TCEJCD&Expires=1643090487&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00inSlMwDvMHTcCr9T1iDjIMCCMrV_MtbxGMAausZOHVVrduhVOykDE0SbNgw-FMVOsgF2fmF9aoD2PxGEIsH_ObcrAedPg93MsebQmN8zRvl_g6SnYHaYDNk1AxM5stNEYELXEOMXDyuNqAMKNEKTuyjxoVW0TRfLJ2ojaZnuBqsVfZ7G6UIetcEns8qQa8ge5yw7dW6JRYaXhpjF5mY6ngXE-7cuiHyhzI1uPMNt6BPklpyOoJU00wAFYmtt2L-dM4tGrkCisVIuYZoLAaYsK3uQr9MHA8mhSfrXhM7p9roRSSIEYuyWe8_ZpGvdMcqmnyxbPBTCyHV1wr6f12fP1uOh-3m3szwul7jpC931JMkjqPHkV1uhoZolSCzn4VQoW_fcokZpgMBmOEmSGjks-xF7_Ro41WgqNxGCuPF9qOWoa4SbYTovs77eS6G3GEZejAZcQ-1w0ncvcbh5_g3wDNAqk5nM3DZn7yi9L67FYdoY8nn6YMczR0pn7dkCqT5nWuZFUAh0zYYoGU3qT0T1lsAcH0tjY4aaYfS5DCD6xc0gJQDZbBRfZmd8DBJp3U-oIO4_4MCsyR_z_vLDaB8pSEz0TigP435oAoJRxxvNTDMSrQFYJDGMY8GcuZStzrC-PMqdQ3xdcQ992Hg0vbTESCXaixK1UcTDAgRmVOWo0ngFepOFZO-odWx3a_R0MrcceSe46Rqa75byyg3B6kY4UnmRH-V8yCDglfMR9mL2Wxh1SQ6a9j5ZWstYneVPbvZog7Caw3fUpO-pM5_6dlXHPr0%3D&Signature=i7bpC6iNIByXsBaULaNLH6Vou4c%3D",
        },
      ],
      tableData: [{
          date: 'Azure Function',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
          link: 'https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/AKS%20Best%20Practices%20Deepdive%20for%20BMW.pdf?AccessKeyId=HZT3CL9ER9LKKVRN3JIL&Expires=1645144770&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00ja_Gs3ruiOc9RL6WN3WlCd1TpcjMjxJpPNE5e2kzbGf8o1ekMrIVbj2y-soqxs7o2djfYQQSoe0jq7BoZdRGmCaMPUvOCA9piafq8vqe-7UkmdNO6iQ3y9XOk_Os07pi_2eABEI8gU5MDk4cH6vpm49wP9R16O34DspG_T5g-OsH4P8Ma1sSg7RN66xT_MDcyEzgppmPFl5la1pqxFXjz5kXiNJGPy0zhtr4yrJxsmgr-V191MYxZ7SFoeyRbO5pjib3af_id5ZlibY7xJ3y_b0tDl9OwETA-gRWxuuRrLc1YVUMm_e_1rGM7-ZABNFGcB83rnL_pk-EfVha724CJksDfEFQL2T465xk_hF63JfIMYK7EXnHVweVP2530adn0sTqRuAB28OJrvITUyyl__CwbSmK2dSueDcra2c_dh22AlJahGAj-iHPeph1_7KNx2e965-HoVYfmlaLsBR67FFwJUcQzyItjG9dmblQpT_21YN25AoU3YudJlQFDAKP7XVlzMRou_wjseTxkbVs1wKTU2qVd4mGgtIY6FgAUKU2r3kJq4K1MPQwT6VpHbMPbaLyL_i1-OMEFtgPVSVTbaMg67snVSYH0FIbGG-2sRkvDGPBjOkZepuKMv4et4ktuxCDsC5hH-XKsyC6EYd11TOy-iwXvKHQn8iEh_7-rKXxDh60gn2SVptKWj5ZiCMLpr8RVfbRAZIavF6FUzHPsTAmnMHRh195flqdgWmD76xa4VlcIJG5T-0kiPjKlP8TKjcsp2E_CTHGwwjuIVA5HME%3D&Signature=QKx2RocBhzgAqWs10xwKMUfUVnA%3D'
        }, {
          date: 'HW CCE',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
          link: 'https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/NextGen%20Cloud%20Tooling%20Highlights.pdf?AccessKeyId=QWROPPH7MFDQGBY3QR49&Expires=1645144801&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00jRUaC4A1gvl8Z8PfikVT-6az2Te51Yl7pDbDIRtXIZIXYbnOhQMXz-LdEjQb085S797v-EbPyJbekKE3j_OHObXujKTRI_aAUjZnOQxZYMyhrjcej_RXnTjrd4p-syJai8rZnbM947fhyWcW-vAD8INZFd0UeyJKukck8uYxPvGPYN2ftE3UgMp9-q7SX5u5FqJl171b3z8dUN2C-5bUTYQkhr6FPPTYyp-rKNNkF2S7GxJSFMd0KMxOl-6Mq_WMVCqPA9UEakpwoU3-oecs06K9GSOU4Oj_uFl42C7ku7dVerIFW8Ow1pSwvOT_FW9G0Ew9DIC8mj22xzK26aLYeZXcBlnZ7QhKfbO3qlPThiyiMLE4aZL0ll7Tym89JsfPZ_S2uLqPTZyf0Py3nl4SoH-zG3hpXid_f6MhH5YOUHiZ91R7uNfbDrS1hT6tTCY2jCt7W0JBJLCpZDdQXQChj8ZkGeG6Ym-pa2ggBMp7AoVuL66x1FHu7M1SWldjlIu3lDWd5EF-_U25d6moM9YX5k_mT5xuobjLr_MxC5fjIfQjBzv1sO0jb8zHlQEtmobDab5pTUIl_PFwq8DW_9NEGMGjos8FOJlDV8rAoZJpXGNzrW_0E_rAsnHbtz5-G03UdHdx4F2Y9sIaTvD1Q0gwx7ykiSWhfge_Oah-9yhN4SfvyVA5o6TghAfu7cv-Xq8YRCkQmuewML9HZdaUV8en_9w3Ud2f2dxoSLDhxqnvNwI4LXkugUEpgQreBrzlTR3YnFNZXleb2VluFsza6YdqjJA%3D&Signature=MtDF2EuKcZ9B90pwESyepWKRBYo%3D'
        }, {
          date: '阿里白皮书',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
          link: 'https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/AKS%20Best%20Practices%20Deepdive%20for%20BMW.pdf?AccessKeyId=HZT3CL9ER9LKKVRN3JIL&Expires=1645144770&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00ja_Gs3ruiOc9RL6WN3WlCd1TpcjMjxJpPNE5e2kzbGf8o1ekMrIVbj2y-soqxs7o2djfYQQSoe0jq7BoZdRGmCaMPUvOCA9piafq8vqe-7UkmdNO6iQ3y9XOk_Os07pi_2eABEI8gU5MDk4cH6vpm49wP9R16O34DspG_T5g-OsH4P8Ma1sSg7RN66xT_MDcyEzgppmPFl5la1pqxFXjz5kXiNJGPy0zhtr4yrJxsmgr-V191MYxZ7SFoeyRbO5pjib3af_id5ZlibY7xJ3y_b0tDl9OwETA-gRWxuuRrLc1YVUMm_e_1rGM7-ZABNFGcB83rnL_pk-EfVha724CJksDfEFQL2T465xk_hF63JfIMYK7EXnHVweVP2530adn0sTqRuAB28OJrvITUyyl__CwbSmK2dSueDcra2c_dh22AlJahGAj-iHPeph1_7KNx2e965-HoVYfmlaLsBR67FFwJUcQzyItjG9dmblQpT_21YN25AoU3YudJlQFDAKP7XVlzMRou_wjseTxkbVs1wKTU2qVd4mGgtIY6FgAUKU2r3kJq4K1MPQwT6VpHbMPbaLyL_i1-OMEFtgPVSVTbaMg67snVSYH0FIbGG-2sRkvDGPBjOkZepuKMv4et4ktuxCDsC5hH-XKsyC6EYd11TOy-iwXvKHQn8iEh_7-rKXxDh60gn2SVptKWj5ZiCMLpr8RVfbRAZIavF6FUzHPsTAmnMHRh195flqdgWmD76xa4VlcIJG5T-0kiPjKlP8TKjcsp2E_CTHGwwjuIVA5HME%3D&Signature=QKx2RocBhzgAqWs10xwKMUfUVnA%3D'
        }, {
          date: '腾讯Cloud',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
          link: 'https://portal-doc.obs.cn-east-3.myhuaweicloud.com:443/AKS%20Best%20Practices%20Deepdive%20for%20BMW.pdf?AccessKeyId=HZT3CL9ER9LKKVRN3JIL&Expires=1645144770&response-content-disposition=inline&x-obs-security-token=gQpjbi1ub3J0aC00ja_Gs3ruiOc9RL6WN3WlCd1TpcjMjxJpPNE5e2kzbGf8o1ekMrIVbj2y-soqxs7o2djfYQQSoe0jq7BoZdRGmCaMPUvOCA9piafq8vqe-7UkmdNO6iQ3y9XOk_Os07pi_2eABEI8gU5MDk4cH6vpm49wP9R16O34DspG_T5g-OsH4P8Ma1sSg7RN66xT_MDcyEzgppmPFl5la1pqxFXjz5kXiNJGPy0zhtr4yrJxsmgr-V191MYxZ7SFoeyRbO5pjib3af_id5ZlibY7xJ3y_b0tDl9OwETA-gRWxuuRrLc1YVUMm_e_1rGM7-ZABNFGcB83rnL_pk-EfVha724CJksDfEFQL2T465xk_hF63JfIMYK7EXnHVweVP2530adn0sTqRuAB28OJrvITUyyl__CwbSmK2dSueDcra2c_dh22AlJahGAj-iHPeph1_7KNx2e965-HoVYfmlaLsBR67FFwJUcQzyItjG9dmblQpT_21YN25AoU3YudJlQFDAKP7XVlzMRou_wjseTxkbVs1wKTU2qVd4mGgtIY6FgAUKU2r3kJq4K1MPQwT6VpHbMPbaLyL_i1-OMEFtgPVSVTbaMg67snVSYH0FIbGG-2sRkvDGPBjOkZepuKMv4et4ktuxCDsC5hH-XKsyC6EYd11TOy-iwXvKHQn8iEh_7-rKXxDh60gn2SVptKWj5ZiCMLpr8RVfbRAZIavF6FUzHPsTAmnMHRh195flqdgWmD76xa4VlcIJG5T-0kiPjKlP8TKjcsp2E_CTHGwwjuIVA5HME%3D&Signature=QKx2RocBhzgAqWs10xwKMUfUVnA%3D'
        }],
        
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
    fadeInOrFadeOut(className) {
      $("." + className).fadeToggle();
    },
    openLink(row, event, column){
      console.log(row.link);
      window.location.href=row.link
    },
  },
};
</script>

<style scoped>
.carousel {
  margin-top: 30px;
}
.carousel_image_type {
  width: 100%;
  height: 100%;
}
.el-link.el-link--default {
  color: #fff;
  font-size: 26px;
  margin-left: 15px;
}
</style>

 
 