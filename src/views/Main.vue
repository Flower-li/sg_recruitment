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
            <van-form @submit="onSubmit">
              <div v-for="item in mainData" :key="item.id">
                <van-cell-group>
                  <van-field
                    :required="item.require"
                    colon
                    center
                    :type="item.type"
                    :label="item.name"
                    :placeholder="'请填写' + item.name"
                    v-model="item.value"
                    input-align="right"
                    :rules="item.rule"
                    v-if="item.type == 'text' || item.type == 'number'"
                  />
                  <van-field
                    :required="item.require"
                    readonly
                    clickable
                    colon
                    :label="item.name"
                    v-model="item.value"
                    placeholder="点击选择时间"
                    input-align="right"
                    :rules="item.rule"
                    @click="showDate(item.dateType, item.id)"
                    v-if="item.type == 'date'"
                  />
                  <div class="select own-div" v-if="item.type == 'select'">
                    <p>{{ item.name }}</p>
                    <van-dropdown-menu :overlay="false">
                      <van-dropdown-item
                        v-model="item.value"
                        :options="item.selectData"
                      />
                    </van-dropdown-menu>
                  </div>
                  <div class="upload own-div" v-if="item.type == 'uploadImg'">
                    <p>图片上传：</p>
                    <van-uploader
                      v-model="item.fileList"
                      multiple
                      :max-count="item.maxCount"
                    />
                  </div>
                  <div class="add-line own-div" v-if="item.type == 'dateList'">
                    <p>{{ item.name }}</p>
                    <van-swipe-cell v-for="data in item.data" :key="data.id">
                      <van-field
                        readonly
                        clickable
                        colon
                        label="开始时间"
                        placeholder="点击选择时间"
                        input-align="right"
                        v-model="data.startDate.value"
                        @click="
                          showDate(data.startDate.dateType, data.startDate.id)
                        "
                      />
                      <van-field
                        readonly
                        clickable
                        colon
                        label="结束时间"
                        placeholder="点击选择时间"
                        input-align="right"
                        v-model="data.endDate.value"
                        @click="
                          showDate(data.endDate.dateType, data.endDate.id)
                        "
                      />
                      <van-field
                        v-model="data.text"
                        rows="2"
                        autosize
                        colon
                        type="textarea"
                        input-align="left"
                        maxlength="50"
                        placeholder="请输入信息"
                        show-word-limit
                      />
                      <template #right>
                        <van-button
                          square
                          text="删除"
                          type="danger"
                          class="delete-button"
                          @click="deleteLine(item.id, data.id)"
                        />
                      </template>
                    </van-swipe-cell>
                    <van-button
                      class="add-button"
                      @click="
                        addLine(
                          item.id,
                          item.data[item.data.length - 1].id,
                          item.data[item.data.length - 1].startDate.dateType,
                          item.data[item.data.length - 1].endDate.dateType
                        )
                      "
                      >+添加一行</van-button
                    >
                  </div>
                  <van-field
                    v-model="item.value"
                    :required="item.require"
                    rows="2"
                    autosize
                    colon
                    :label="item.name"
                    type="textarea"
                    input-align="right"
                    :maxlength="item.maxLength"
                    placeholder="请输入留言"
                    show-word-limit
                    v-if="item.type == 'textArea'"
                  />
                </van-cell-group>
              </div>
              <van-button
                :loading="isSending"
                type="info"
                loading-text="提交中..."
                native-type="submit"
                >点击提交</van-button
              >
            </van-form>
            <van-popup v-model="showPicker" position="bottom">
              <van-datetime-picker
                :type="dateType"
                title="选择时间"
                :min-date="minDate"
                :max-date="maxDate"
                @confirm="onConfirm"
                @cancel="showPicker = false"
                :formatter="formatter"
              />
            </van-popup>
          </van-col>
        </van-row>
      </div>
    </div>
  </div>
</template>

<script>
import { Toast } from "vant";
export default {
  name: "Main",
  beforeCreate() {
    document
      .querySelector("body")
      .setAttribute("style", "background-color:#f2f2f3");
  },
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
        "应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知应聘须知",
      isSending: false,
      //idCard: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/,
      //phone:/^1[3456789]\d{9}$/,
      value: "",
      dateId: "",
      dateType: "",
      showPicker: false,
      minDate: new Date(1950, 0, 1),
      maxDate: new Date(2030, 12, 31),
      currentDate: new Date(),
      mainData: []
    };
  },
  mounted() {
    this.$axios
      .post("http://mock-api.com/wjzpZenX.mock/main", {})
      .then((res) => {
        console.log(res);
        this.mainData = res.data;
      });
  },
  methods: {
    onSubmit() {
      this.isSending = true;
      setInterval(() => {
        this.isSending = false;
      }, 2000);
      console.log("上传内容", this.mainData);
    },
    formatter(type, val) {
      if (type === "year") {
        return `${val}年`;
      } else if (type === "month") {
        return `${val}月`;
      } else if (type === "day") {
        return `${val}日`;
      }
      return val;
    },
    showDate(value, id) {
      console.log(value, id);
      this.showPicker = true;
      this.dateId = id;
      this.dateType = value;
    },
    trunData(d) {
      return d < 10 ? "0" + d : d;
    },
    onConfirm(value) {
      if (this.dateType == "date") {
        this.value =
          value.getFullYear() +
          "-" +
          this.trunData(value.getMonth() + 1) +
          "-" +
          this.trunData(value.getDate());
      } else {
        this.value =
          value.getFullYear() + "-" + this.trunData(value.getMonth() + 1);
      }
      for (let item of this.mainData) {
        if (item.id == this.dateId) {
          item.value = this.value;
        } else {
          if (item.data) {
            let dateList = item.data;
            for (let item2 of dateList) {
              if (item2.startDate.id == this.dateId) {
                item2.startDate.value = this.value;
              }
              if (item2.endDate.id == this.dateId) {
                item2.endDate.value = this.value;
              }
            }
          }
        }
      }
      this.showPicker = false;
    },
    addLine(dataId, dataChildenMaxId, startDateType, endDateType) {
      console.log(dataId, dataChildenMaxId);
      let idNew = Number(dataChildenMaxId) + 1;
      for (let item of this.mainData) {
        if (item.id == dataId) {
          item.data.push({
            id: String(idNew),
            startDate: {
              id: idNew + "001",
              value: "",
              dateType: startDateType
            },
            endDate: {
              id: idNew + "002",
              value: "",
              dateType: endDateType
            },
            text: ""
          });
        }
      }
    },
    deleteLine(dateListId, lineId) {
      console.log(dateListId, lineId);
      for (let item of this.mainData) {
        if (item.id == dateListId) {
          let item2 = item.data;
          console.log(item2.length);
          if (item2.length > 1) {
            item2.splice(
              item2.findIndex((a) => a.id === lineId),
              1
            );
          } else {
            Toast("唯一行不允许删除！");
          }
        }
      }
    }
  }
};
</script>

<style lang="scss">
.select {
  .van-dropdown-menu__bar {
    background-color: #e9e8e8 !important;
    box-shadow: unset !important ;
    text-align: center;
  }
  .van-dropdown-menu__title::after {
    border-color: transparent transparent black black !important;
  }
  .van-popup--top {
    top: 0;
    left: 5%;
    width: 90%;
  }
  .van-cell__title {
    text-align: center;
  }
  .van-cell__value {
    display: none;
  }
}
.main {
  .main-container {
    .van-field__error-message {
      text-align: right !important;
    }
  }
}
</style>

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
          .own-div {
            font-size: 14px;
            line-height: 24px;
            padding: 10px 16px;
            color: #646566;
            // border-bottom: 1px solid #ebedf0;
            p {
              padding-bottom: 15px;
            }
          }
          .add-line {
            .add-button {
              background-color: #e9e8e8;
              margin: 3vmin 0 3vmin 0;
            }
            .delete-button {
              height: 100%;
            }
          }
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
