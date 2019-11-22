<template>
  <div class="todo">
    <div class="title">
      <div class="header">{{ msg }}</div>

      <div :class="{ CloseBtn: show, insertbtn: true }" :target="content" @click.stop="showBox">+</div>
    </div>
    <div class="content">
      <ul>
        <li
          v-for="(item, index) in list"
          @dblclick="change"
          :class="{ cross: item.flag }"
          :key="index"
        >
          <input type="checkbox" :value="index" v-model="item.flag" />
          <label class="date">{{ item.date }}</label>
          <label class="todocontent">{{ item.content }}</label>
        </li>
      </ul>
    </div>
    <transition name="slide-fade">
      <div class="Insert" v-if="show">
        <label>内容:</label>
        <input type="text" @keyup.enter="Insert" v-model="dcontent" />
        <label>日期:</label>
        <Datepicker v-model="date"></Datepicker>
      </div>
    </transition>
  </div>
</template>

<script>
import Datepicker from "vuejs-datepicker";
export default {
  name: "HelloWorld",
  data: () => {
    return {
      date: new Date().toLocaleString(),
      list: [],
      show: false,
      Name: "",
      tag: "",
      dcontent: ""
    };
  },
  watch: {
    list: {
      handler() {
        window.console.log(JSON.stringify(this.list));
        localStorage.setItem(this.tag, JSON.stringify(this.list));
      },
      deep: true
    }
  },
  methods: {
    showBox: function(e) {
      window.console.log(e.toElement.attributes.target.nodeValue);
      this.show = !this.show;
    },
    change: function() {
      window.console.log("li被双击！");
    },
    Insert: function() {
      var data = "";
      var newStr = "";
      try {
        data = localStorage.getItem(this.tag);
        data = data.slice(0, data.length - 1);
        newStr =
          data +
          ',"' +
          new Date().toLocaleString() +
          '":{"date":"' +
          this.date.toLocaleDateString() +
          '","content":"' +
          this.dcontent +
          '","flag":false}}';
      } catch (e) {
        window.console.log(e);
        data = '{"';
        newStr =
          data +
          new Date().toLocaleString() +
          '":{"date":"' +
          this.date.toLocaleDateString() +
          '","content":"' +
          this.dcontent +
          '","flag":false}}';
      }
      localStorage.setItem(this.tag, newStr);
      window.console.log(localStorage.getItem(this.tag));
      this.list = JSON.parse(localStorage.getItem(this.tag));
      window.console.log(this.list);
      this.show = !this.show;
      this.dcontent = "";
    }
  },
  mounted: function() {
    this.Name = this._props.msg;
    this.tag = this._props.content;
    var cd = localStorage.getItem(this._props.content);
    if (cd !== null) {
      var json = JSON.parse(cd);
      this.list = json;
      window.console.log(json);
    } else {
      window.console.log("没有" + this._props.content + "值");
    }
  },
  props: {
    msg: String,
    content: String
  },
  components: {
    Datepicker
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.3s ease;
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
.Insert {
  position: absolute;
  top: 25px;
  width: 100%;
  background: white;
  text-align: left;
  padding-left: 40px;
}
.Insert label {
  width: 40px;
  float: left;
  margin-left: -40px;
}
.cross {
  text-decoration-line: line-through;
}
.Insert input[type="text"] {
  box-sizing: border-box;
  width: 100%;
  display: block;
}
.todo {
  flex: 1;
  flex: 0 0 50%;
  height: 50%;
  border: 1px solid black;
  box-sizing: border-box;
  overflow: hidden;
  position: relative;
}
.todo .title {
  background: pink;
  height: 25px;
  line-height: 25px;
  width: 100%;
}
.todo .title .header {
  float: left;
}
.CloseBtn {
  transform: rotateZ(45deg);
}
.todo .title .insertbtn {
  float: right;
  width: 25px;
  height: 25px;
  user-select: none;
  cursor: pointer;
  transition: all 0.3s;
}
.todo .content {
  background: gray;
  height: 100%;
}
.todo .content ul li {
  text-align: left;
  user-select: none;
}
.todo .content ul li .date {
  color: aqua;
  margin: 0px 10px;
}
.todo .content ul li .todocontent {
  color: white;
}
</style>
