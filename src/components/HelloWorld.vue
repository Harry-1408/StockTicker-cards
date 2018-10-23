<template>
  <div class="hello">
    <el-row :gutter="12">
      <el-col :span="8" v-for="item in cardData">
        <div  @click="getCardData(item)">
          <el-card class="box-card">
          <div slot="header" class="clearfix">
            <img :src="item[1].url" alt="">
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
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      symbols: ['AAPL','MSFT','IBN','V','HDB','PYPL','TSLA','FB','AXP','KO','BABA','VOD'],
      cardData: [],
      marketData:{
          "symbol": "AAPL",
          "marketPercent": 0.00901,
          "bidSize": 200,
          "bidPrice": 110.94,
          "askSize": 100,
          "askPrice": 111.82,
          "volume": 177265,
          "lastSalePrice": 111.76,
          "lastSaleSize": 5,
          "lastSaleTime": 1480446905681,
          "lastUpdated": 1480446910557,
          "sector": "softwareservices",
          "securityType": "commonstock"
        }
    }
  },
  async mounted() {
    let dataObj = []
    for (let index = 0; index < this.symbols.length; index++) {
      await axios.get('https://api.iextrading.com/1.0/stock/'+ this.symbols[index] +'/company')
      .then((res)=>{
        dataObj.push(res.data)
      })
      .catch((err)=>{
        console.log(err)
      })
      await axios.get('https://api.iextrading.com/1.0/stock/'+ this.symbols[index] +'/logo')
      .then((res)=>{
        dataObj.push(res.data)
      })
      .catch((err)=>{
        console.log(err)
      })
      dataObj.push(this.marketData)
      this.cardData.push(dataObj)
      dataObj = []
    }
  },
  methods: {
    getCardData(item) {
      this.$router.push({name:'cardPage', params: { item : item}})
    }
  },
  filters: {
    gettime(time) {
      // console.log('time', time)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
