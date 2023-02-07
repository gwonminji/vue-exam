<template>
  <div>
    <h1>click toggle</h1>
    <div class="bar" :class="isVisible ? 'is-visible' : ''">box</div>
    <button type="button" @click="toggle">click</button>

    <h1>click style</h1>
    <div class="box">
      <span class="line" :class="{ 'blue': isBlue, 'red': isRed }">line</span>
    </div>
    <button type="button" @click="lineBlue">blue로 변경</button>
    <button type="button" @click="lineRed">red로 변경</button>

    <h1>click v-if v-else</h1>
    <div v-if="isShow">이거</div>
    <div v-else>이거 말고</div>
    <button type="button" @click="isShow = !isShow">click</button>

    <h1>v-for 리스트 출력</h1>
    <ul>
      <li v-for="(v, idx) in items" :key="idx">{{ v.level }}</li>
    </ul>

    <h1>v-for 오브젝트 출력</h1>
    <dl>
      <dd v-for="(v, idx) in person" :key="idx">
        <span>{{ v.name }}</span>
        <span>{{ v.birth }}</span>
        <span>{{ v.blood }}</span>  
      </dd>
    </dl>

    <h1>input text 입력</h1>
    <div>
      <input type="text" v-model="message" placeholder="메시지를 입력하세요.">
    </div>
    <p>입력값 : {{ message }}</p>

    <h1>textarea 입력</h1>
    <span> 여러 줄 메시지 : {{ msgs }}</span>
    <textarea v-model="msgs" placeholder="여러 줄 입력"></textarea>

    <h1>v-model 체크박스</h1>
    <div>
      <input type="checkbox" id="cb" v-model="checked">
      <label for="cb">{{ checked }}</label>
    </div>

    <h1>v-model 체크박스 배열</h1>
    <div>체크된 이름 : {{ checkedName }}</div>
    <input type="checkbox" id="jack" value="jack" v-model="checkedName">
    <label for="jack">jack</label>
    <input type="checkbox" id="john" value="john" v-model="checkedName">
    <label for="john">john</label>
    <input type="checkbox" id="mike" value="mike" v-model="checkedName">
    <label for="mike">mike</label>

    <h1>v-model select option</h1>
    <div>
      <!--
        v-model 표현식의 초기값이 옵션과 일치하지 않으면 select 엘리먼트가 '선택되지 않은' 상태로 렌더링 됨
        ios에서는 이 경우 변경 이벤트를 발생시키지 않기 때문에 사용자가 첫 번째 항목을 선택할 수 없게 됨
        비활성화된 옵션에 빈 값을 제공하는 것이 좋음
      -->
      <select name="" id="" v-model="select">
        <option disabled value="">선택하세요.</option>
        <option value="option0">option0</option>
        <option value="option1">option1</option>
        <option value="option2">option2</option>
      </select>
    </div>
    <div>선택한 select : {{ select }}</div>

    <h1>v-model select option 다중선택</h1>
    <div>
      <select v-model="select2" multiple>
        <option value="가">가</option>
        <option value="나">나</option>
        <option value="다">다</option>
      </select>
    </div>
    <div>선택한 select : {{ select2 }}</div>

    <h1>이벤트 핸들링</h1>
    <button type="button" @click="cnt++">{{ cnt }}</button>
    <button type="button" @click="openAlert">alert 띄우기</button>

    <h1>watch</h1>
    <div> watch text : {{ watchText }}</div>
    <button type="button" @click="changeText">changeText</button>


  </div>
</template>

<script>
import { ref, watch } from 'vue'
export default {
  name: 'HelloWorld',

  setup() {
    const isVisible = ref(false);
    const isBlue = ref(false);
    const isRed = ref(false);
    const isShow = ref(false);
    const items = ref([{level: 'A'}, {level: 'B'}, {level: 'C'}, {level: 'D'}, {level: 'E'}]);
    const person = ref([{name: 'gmj', birth: '1124', blood: 'O'}]);

    const toggle = () => {
      isVisible.value = !isVisible.value;
    }

    const lineBlue = () => {
      isBlue.value = true;
      isRed.value = false;
    }

    const lineRed = () => {
      isRed.value = true;
      isBlue.value = false;
    }

    const openAlert = () => {
      alert();
    }

    const message = ref('');
    const msgs = ref('');
    const checked = ref(false);
    const checkedName = ref([]);

    const select = ref('');
    const select2 = ref([]);
    const cnt = ref(0);

    const watchText = ref('텍스트 바뀌기 전');
    watch(
      watchText,
      (cur, prev) => {
        console.log("초기 텍스트 ==> ", prev);
        console.log("바뀐 텍스트 ==> ", cur);
      },{
        immediate: true
      }
    )
    const changeText = () => {
      watchText.value = '텍스트 바꿈'
    }

    return{
      isVisible,
      toggle,
      isBlue,
      isRed,
      lineBlue,
      lineRed,
      isShow,
      items,
      person,
      openAlert,
      message,
      msgs,
      checked,
      checkedName,
      select,
      select2,
      cnt,
      watchText,
      changeText
    }
  }
}
</script>
<style>
.bar{
  display: none;
}
.is-visible{
  display: block;
}

.line{
  display: inline-block;
}
.blue{
  background: blue;
  color: #fff;
}
.red{
  background: red;
  color: #fff;
}
</style>