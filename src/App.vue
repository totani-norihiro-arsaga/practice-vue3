<script setup>
import {reactive, ref, computed} from "vue";

let message = 'hello world';
const html = "<h2>v-html属性</h2>"
const link = 'https://google.com';
let isActive = ref(true);
const error = '何か変です。';
const languages = ['Javascript', 'TypeScript', 'Vue.js'];
const user = {
  name: '太郎',
  age: 54,
  job: 'carpenter',
  hobby: 'drinking coffee',
}

const myName = reactive({
  firstName:'とんかつ',
  lastName:'DJ',
})

const companies = [
    {name:'TOYOTA',founder: '豊田さん', country: 'jp', industry: 'mobirity',},
    {name:'Google', founder: 'rary page', country: 'us', industry: 'information technology',},
    {name: 'FaceBook', founder: 'mark', country: 'us', industry: 'information technology',},
    {name: 'ArsagaPartners', founder: 'taimei', country: 'jp', industry: 'information technology',},
    {name:'ITOKI', founder: 'kijuurou', country: 'jp', industry: 'manufacturing industry',}
];

let count = ref(0);
let inputMessage = reactive({
  message: 'v-modelとreactive',
})
const upperCase = () => {
  message = message.toUpperCase();
}
upperCase();

const clickButton = () => {
  isActive.value = !isActive.value;
  console.log(isActive);
}

const submit = (v) => {
  v.preventDefault();
  console.log(v);
}

const japaneseCompanies = computed(()=>companies.filter((company) => company.country === 'jp'));

const cFullName = computed(() => {
  console.log('コンピューテッド');
  return Math.random()+`${myName.firstName}${myName.lastName}`
});
const fullName = () => {
  console.log('ファンクション');
  return Math.random()+`${myName.firstName}${myName.lastName}`;
}

</script>

<template>
  <h1>Vue3 入門</h1>
  {{ message.length > 10 ? 'long' : 'short' }}
  <p v-text="message"></p>
  <div v-html="html"></div>
  <a :href="link">go Google</a>
  <p :class="isActive ? 'active underLine' : 'blue'">v-bindでクラスを付ける(リアクティブに変化)</p>
  <p v-if="error">{{ `v-ifで条件分岐:${error}` }}</p>
  <p v-else>エラーはございません。</p>
  <h3>リストレンダリング</h3>
  <ul v-for="language in languages " :key="languages">
    <li>{{ language }}</li>
  </ul>
  <h3>オブジェクトのリストレンダリング</h3>
  <ul v-for="(value, prop) in user " :key="value">
    <li>{{ prop }}:{{ value }}</li>
  </ul>
  <button class="h3" @click="clickButton">クリックイベント</button>
  <input class="h3" @click="submit" type="submit" value="prevent default">
  <input type="text" v-model="inputMessage.message">
  <p>{{ inputMessage.message }}</p>
  <h3>computedでフィルタリング</h3>
  <ul v-for="(value, prop) in japaneseCompanies " :key="value.name">
    <li>{{value.name}}</li>
  </ul>
  <h3>computedとfunction</h3>
  <div>{{cFullName}}</div>
  <div>{{cFullName}}</div>
  <div>{{cFullName}}</div>
  <div>{{fullName()}}</div>
  <div>{{fullName()}}</div>
  <div>{{fullName()}}</div>
  <input type="text" v-model="myName.firstName">
  <button @click="count++">{{count}}</button>
</template>

<style scoped>
.active {
  color: red;
  font-weight: 900;
}

.blue {
  color: blue;
  font-weight: 1000;
}

.underLine {
  text-decoration: underline;
}

ul {
  list-style: none;
  text-align: start;
}

.h3 {
  display: block;
  font-size: 1.17em;
  margin-block-start: 1em;
  margin-block-end: 1em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
  font-weight: bold;
}
</style>