<template>
  <div class="home">
    <van-image :src="headerImg"></van-image>
    <van-row type="flex" justify="center">
      <van-col>
        <div class="header">
          <p>{{ title }}</p>
          <span>[{{ status }}]</span>
        </div>
      </van-col>
    </van-row>
    <van-row type="flex" justify="center">
      <van-col>
        <div class="list">
          <div class="icon"><van-icon name="location-o" size="17" /></div>
          <p>报名地址：</p>
          <p>{{ position }}</p>
        </div>
        <div class="list">
          <div class="icon"><van-icon name="phone-o" size="17" /></div>
          <p>联系电话：</p>
          <p>{{ telNum }}</p>
        </div>
      </van-col>
    </van-row>
    <van-divider style="margin: 15px 0 10px 0;" />
    <van-row>
      <van-col :span="6">
        <van-image :src="logoImg"> </van-image>
      </van-col>
      <van-col :span="18">
        <div class="jjTitle">
          <p>{{ companyTitle }}</p>
          <span>公司简介</span>
        </div></van-col
      >
      <van-col :span="22" offset="1">
        <div class="jjMain">
          {{ jjMain }}
        </div>
      </van-col>
    </van-row>
    <van-tabbar :safe-area-inset-bottom="true" style="height: 45px;">
      <van-button type="primary" @click="ljbm">初审登记</van-button>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      headerImg: require("@/assets/images/header.png"),
      title: "福建省三钢（集团）有限责任公司招工报名初审登记",
      status: "进行中",
      startTime: "2019-10-10 10:40",
      endTime: "2019-10-11 23:59",
      trueNum: "450",
      allNum: "1000",
      position: "福建省三明市梅列区三钢集团",
      telNum: "0598-8205039、8206415",
      logoImg: require("@/assets/images/logo.png"),
      companyTitle: "福建省三钢（集团）有限责任公司招工报名初审登记",
      jjMain:
        " 福建省三钢（集团）有限责任公司（以下简称三钢集团）前身为福建省三明钢铁厂，建于1958年。2000年3月，经福建省人民政府批准改制设立福建省三钢（集团）有限责任公司，控股股东为福建省冶金（控股）有限责任公司，占三钢集团总股本的94.4906%。目前，三钢集团已形成年产钢1200万吨和以钢铁业为主、多元产业并举的跨行业、跨地区、跨所有制的大型企业集团，旗下拥有三明本部、泉州闽光、罗源闽光、漳州闽光四个钢铁生产基地。截至2019年12月，三钢集团有职工1.59万人，总资产436.09亿元，全资及控股子公司16家（其中福建三钢闽光股份有限公司为上市公司），紧密型企业2家。三钢集团自1988年以来连年进入中国500强企业行列，在“2019中国企业500强”中位居第311位，在“2019中国制造业企业500强”中位居第142位。三钢集团先后获得全国五一劳动奖状、全国文明单位、全国先进基层党组织、全国模范劳动关系和谐企业、全国质量管理先进企业、第一批国家级知识产权优势企业、中国钢铁工业科技工作先进单位、全国钢铁工业先进集体、首届“福建省政府质量奖”、福建省企（事）业信息化应用先进单位、福建省企业文化建设示范单位、福建省用户满意企业、福建省工商信用优异企业（AAA级）等荣誉称号。"
    };
  },
  methods: {
    ljbm() {
      this.$router.push("/Main");
    }
  }
};
</script>

<style lang="scss" scoped>
.home {
  .van-image {
    width: 100%;
  }
  .van-row {
    width: 90%;
    margin: auto;
    .van-col {
      .header {
        p {
          font-size: 16px;
          color: #000000;
          margin: 10px 0;
          font-weight: 600;
        }
        span {
          float: left;
          color: #18b0f8;
          margin-bottom: 5px;
        }
      }
      .list {
        color: #858484;
        display: flex;
        display: -webkit-flex;
        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: flex-start;
        align-items: flex-start;
        .icon {
          float: left;
          margin-right: 3px;
        }
        p {
          font-size: 12px;
          word-break: break-all;
          float: left;
          min-width: 60px;
        }
      }
      .van-image {
        width: 67px;
        height: 67px;
        float: right;
      }
      .jjTitle {
        float: left;
        p {
          font-size: 15px;
          color: #000000;
          margin-top: 10px;
          margin-bottom: 3px;
        }
        span {
          font-size: 12px;
          color: #fff;
          background-color: #18b0f8;
          padding: 2px 5px;
          border-radius: 5px;
        }
      }
      .jjMain {
        font-size: 12px;
        color: #858484;
        line-height: 22px;
        padding-bottom: 50px;
        text-align: justify;
        padding-top: 10px;
      }
    }
  }
  .van-button {
    width: 100%;
    height: 100%;
  }
}
</style>
