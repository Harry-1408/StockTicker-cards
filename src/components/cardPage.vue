<template>
  <el-card class="box-card" @click="getCardData(item)">
          <div slot="header" class="clearfix">
            <img :src="item[1].url" alt="" @click="getCardData(item)">
            <span>{{item[0].companyName}}</span>
            <!-- <el-button style="float: right; padding: 3px 0" type="text">Operation button</el-button> -->
          </div>
          <div>
            <p> <b>MP</b> {{item[2].marketPercent}}</p>
            <p> <b>LSP</b> {{item[2].lastSalePrice}}</p>
            <p> <b>LSS</b> {{item[2].lastSaleSize}}</p>
          </div>
          <div>
            <p> <b>Last Sale Time</b> {{item[2].lastSaleTime | gettime() }}</p>
            <p> <b>Last Update</b> {{item[2].lastUpdated}}</p>
          </div>
          <div>
            <p> <b>Sector</b> :{{item[0].sector}}</p>
            <p> <b>Industry</b> {{item[0].industry}}</p>
            <p> <b>CEO</b> {{item[0].CEO}}</p>
            <p> <b>Website</b> {{item[0].website}}</p>
            <!-- <p> <b>Description</b> {{item[0].description}}</p> -->
          </div>
        </el-card>
</template>
<script>
export default {
  props: ['item'],
  mounted() {
    console.log(this.item)
  }
}
</script>

