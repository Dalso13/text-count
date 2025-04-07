<script>
export default {
  data() {
    return {
      textData: "",
      emptyOkText: 0,
      emptyNoText: 0,
      emptyOkByte: 0,
      emptyNoByte: 0,
    }
  },
  created() {
    this.$watch('textData', (newValue, oldValue) => {
      this.emptyOkText = newValue.length
      this.emptyNoText = newValue.trim().length

      this.emptyOkByte = newValue.split("").reduce((acc, cur) => (cur.charCodeAt() > 127 ? (acc += 2) : (acc += 1)), 0);
      this.emptyNoByte = newValue.trim().split("").reduce((acc, cur) => (cur.charCodeAt() > 127 ? (acc += 2) : (acc += 1)), 0);
    },
      {
        flush: true
      });
  },
  methods: {
    allCopy() {
      navigator.clipboard.writeText(this.textData).then((_) => {
        alert(
          "입력하신 내용이 복사되었습니다.\n\nCtrl + v 키를 사용하여, 붙여 넣기를 사용하실 수 있습니다."
        );
      })
    },
    allClear() {
      this.textData = ""
    }
  }
}


</script>
<template>
  <div class="saramin">
    <h1>글자수세기</h1>
    <div class="box">
      <div class="string-length">
        <textarea v-model="textData" placeholder="내용을 입력해주세요"></textarea>
      </div>
      <div class="str-info">
        <p>공백 포함 <span>{{ emptyOkText }}</span> 자 | <span>{{ emptyOkByte }}</span> byte</p>
        <p>공백 제외 <span>{{ emptyNoText }}</span> 자 | <span>{{ emptyNoByte }}</span> byte</p>
      </div>
      <div class="btn-area">
        <button @click="allCopy">전체복사</button>
        <button @click="allClear">초기화</button>
      </div>
    </div>
  </div>
</template>
<style>
.saramin {
  width: 564px;
  margin: 100px auto;
}

.saramin .box {
  border-top: 1px solid #676767;
  border-left: 1px solid #ddd;
  border-right: 1px solid #ddd;
  border-block: 1px solid #ddd;
}

.saramin h1 {
  font-size: 32px;
  margin-bottom: 20px;
  line-height: 1;
  font-weight: normal;
}

.saramin .string-length {
  padding: 30px;
}

.saramin .string-length textarea {
  width: 100%;
  height: 400px;
  border: none;
  outline: none;
}

.saramin .str-info {
  border-top: 1px solid #ebebeb;
  padding: 0 22px;
  font-size: 14px;
  margin: 0px 8px;
}

.saramin .str-info span {
  font-size: 15px;
  color: #ff662f;
  font-weight: bold;
}

.saramin .btn-area {
  background-color: #fbfbfb;
  padding: 35px 0;
  text-align: center;
}

.saramin .btn-area button {
  background: transparent;
  border: 1px solid #d9d9d9;
  width: 160px;
  height: 40px;
  margin: 0 2px;
  cursor: pointer;
}

.saramin .btn-area button:nth-child(1) {
  background-color: #9c9c9c;
  color: white;
}
</style>