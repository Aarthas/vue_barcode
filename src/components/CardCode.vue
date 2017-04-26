<template>
  <div class="container">

    <!--<x-header>This is the page title.</x-header>-->
    <div style="height: 30px"></div>

    <div style="width:100%;color: #333333;font-size: 1.2rem;text-align: center">{{cardNumFormat}}</div>
    <div style="height: 10px"></div>

    <div style="display: flex;flex-direction: column;justify-content: center;align-items:center;background-color: #f1f1f1;
    padding-top: 30px;padding-bottom:20px;margin-left:20px;margin-right:20px;border-radius: 30px;">

      <barcode height="90px" width="290px" bg-color="#f1f1f1" :value=cardNum></barcode>
      <div style="height: 30px"></div>
      <qrcode size=80       bg-color="#f1f1f1" :value=cardNum level="H"></qrcode>
    </div>

    <div style="display: flex;flex-direction: row;justify-content: center">
      <span
        style="color: #333333;font-size: 16px; padding-top: 20px;padding-bottom: 20px;padding-left: 15px;padding-right: 15px;"
        @click="onRefresh">每分钟自动更新</span>
    </div>

    <div style="display: flex;flex-direction: column;justify-content: center;align-items: center;margin-top: 20px">
      <span style="color: #333333;font-size: 14px;padding-left: 15px;padding-right: 15px;">如有二维码显示问题</span>
      <span style="color: #333333;font-size: 14px;padding-left: 15px;padding-right: 15px;">您可以拨打xxxx联系我们</span>
    </div>

  </div>

</template>


<script>
  import {Group, XInput, XButton, Loading, Qrcode} from 'vux'
  import {XHeader} from 'vux'
  import {BarCode} from '../components/barcode/BarCode.vue'


  var barcode = require("../components/barcode/barcode.js");
  var page;
  var st;
  export default {

    components: {
      Group,
      XInput,
      XHeader,
      XButton,
      Loading,
      Qrcode,
      BarCode
    },
    data () {
      return {

        cardNum: "123124321117",

      };
    },
    computed: {
      cardNumFormat(){
        return barcode.formatBarCode(page.cardNum, " ");
      }
    },
    created () {
      page = this;
      console.log("created")
    },

    mounted(){
      console.log("mounted")

    },
    activated () {
      console.log("activated")
      page.onload();
    },

    deactivated(){
      console.log("deactivated")
      clearTimeout(st);
    },


    methods: {
      onRefresh(){
        page.onload();
      },
      onload(){
        console.log("onload   page.cardNum=" + page.cardNum)


        page.cardNum = ( parseInt(page.cardNum,10) + 1) + "";

        clearTimeout(st);
        st = setTimeout(function () {
            page.onload();
            clearTimeout(st);
          },
          10 * 1000
          /*
           4000
           baseBean.getData().interval * 1000
           */
        );

      }


    }
  }


</script>


<style>


</style>
