<template>
  <div class="main">
    <div class="header">
      <van-image :src="headerImg"></van-image>
      <div class="header-black"></div>
    </div>
    <div class="main-list">
      <div class="main-title">
        <h1>{{ company }}</h1>
        <h2>{{ title }}</h2>
        <span>{{ date }}</span>
      </div>
      <div class="main-container">
        <van-row>
          <van-col :span="24" class="container-title">
            <h1>{{ titleSecd }}</h1>
            <p>
              {{ secdMain }}
            </p>
          </van-col>
          <van-col :span="24">
            <van-cell-group>
              <van-field
                :required="false"
                label="姓名"
                placeholder="请填写报名编号"
              />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
              <van-field required label="姓名" placeholder="请填写报名编号" />
            </van-cell-group>
          </van-col>
        </van-row>
      </div>
      <van-button :loading="false" type="info" loading-text="提交中..."
        >点击提交</van-button
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Main",
  //创建前设置
  beforeCreate() {
    document
      .querySelector("body")
      .setAttribute("style", "background-color:#f2f2f3");
  },
  //销毁前清除
  beforeDestroy() {
    document.querySelector("body").removeAttribute("style");
  },
  data() {
    return {
      headerImg: require("@/assets/images/main-header.png"),
      company: "三明钢铁集团",
      title: "福州大学第一场招聘",
      date: "2020-20-20",
      titleSecd: "应聘须知",
      secdMain:
        "应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知"
    };
  }
};
</script>

<style lang="scss" scoped>
.main {
  height: 100%;
  position: relative;
  .header {
    .van-image {
      position: absolute;
      z-index: 100;
      width: 100%;
      height: 30%;
    }
    .header-black {
      position: absolute;
      z-index: 101;
      width: 100%;
      height: 30%;
      background-color: #000000;
      opacity: 0.6;
    }
  }
  .main-list {
    position: absolute;
    z-index: 102;
    width: 90%;
    height: 100%;
    left: 5%;
    .main-title {
      width: 100%;
      color: #fff;
      height: 20%;
      h1 {
        font-size: 5vmin;
        padding-top: 9%;
      }
      h2 {
        font-size: 8vmin;
        margin-bottom: 1vmin;
      }
      span {
        float: right;
        font-weight: bold;
      }
    }
    .main-container {
      clear: both;
      background-color: #fff;
      min-height: 80%;
      border-radius: 10px 10px 0 0;
      .van-row {
        .van-col {
          padding: 10px;
        }
        .container-title {
          h1 {
            padding: 2vmin 0 2vmin 0;
            font-size: 6vmin;
          }
        }
      }
    }
    .van-button {
      width: 100%;
      margin: 3vmin 0 6vmin 0;
    }
  }
}
</style>
