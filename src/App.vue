<script setup lang="ts">
import { reactive } from 'vue'
type typeOfFeatures = {
  Sex: '男性' | '女性' | '性別は？'
  Pclass: string | '階級は？'
  Age: number | '年齢は？'
  Parch: number | '親・子の同伴者数は？'
  SibSp: number | '兄弟姉妹の同伴者数は？'
}

const features = reactive<typeOfFeatures>({
  Sex: '性別は？',
  Pclass: '階級は？',
  Age: '年齢は？',
  Parch: '親・子の同伴者数は？',
  SibSp: '兄弟姉妹の同伴者数は？',
})

const displayOutput = (): void => {
  alert(`
    性別: ${features.Sex}
    階級: ${features.Pclass}
    年齢: ${features.Age}
    親・子の同伴者数: ${features.Parch}
    兄弟姉妹の同伴者数: ${features.SibSp}
  `)
}
</script>

<template>
  <p class="bg-blue-200 text-2xl p-4 mt-4">Hello World</p>
  <div class="container mx-auto mt-4">
    <select v-model="features.Sex" class="select select-primary mb-4">
      <option disabled selected>性別は？</option>
      <option>男性</option>
      <option>女性</option>
    </select>
    <br />
    <select v-model="features.Pclass" class="select select-primary mb-4">
      <option disabled selected>階級は？</option>
      <option>上層クラス（お金持ち）</option>
      <option>中級クラス（一般階級）</option>
      <option>下層クラス（労働階級）</option>
    </select>
    <br />
    <select v-model="features.Age" class="select select-primary mb-4">
      <option disabled selected>年齢は？</option>
      // eslint-disable-next-line vue/require-v-for-key
      <option v-for="i in [...Array(121).keys()]">
        {{ i }}
      </option>
    </select>
    歳
    <br />
    <select v-model="features.Parch" class="select select-primary mb-4">
      <option disabled selected>親・子の同伴者数は？</option>
      // eslint-disable-next-line vue/require-v-for-key
      <option v-for="i in [...Array(11).keys()]">
        {{ i }}
      </option>
    </select>
    人
    <br />
    <select v-model="features.SibSp" class="select select-primary mb-4">
      <option disabled selected>兄弟姉妹の同伴者数は？</option>
      // eslint-disable-next-line vue/require-v-for-key
      <option v-for="i in [...Array(11).keys()]">{{ i }}</option>
    </select>
    人
    <br />
    <button class="btn btn-primary" @click="displayOutput()">結果を出力</button>
  </div>
</template>
