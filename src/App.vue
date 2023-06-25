<script setup lang="ts">
import { ref, reactive } from 'vue'
import axios from 'axios'
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

const survivalProbability = ref<number | undefined>()

const validateRequestValues = (): boolean => {
  if (features.Sex == '性別は？') {
    alert('性別を入力してください。')
    return false
  }
  if (features.Pclass == '階級は？') {
    alert('階級を入力してください。')
    return false
  }
  if (features.Age == '年齢は？') {
    alert('年齢を入力してください。')
    return false
  }
  if (features.Parch == '親・子の同伴者数は？') {
    alert('親子同伴者数を入力してください。')
    return false
  }
  if (features.SibSp == '兄弟姉妹の同伴者数は？') {
    alert('兄弟姉妹同伴者数を入力してください。')
    return false
  }
  return true
}

const displayOutput = (): void => {
  const endPoint = 'http://localhost:8080/api/titanic'
  const validationResult: boolean = validateRequestValues()
  if (validationResult === true) {
    axios
      .post(endPoint, features)
      .then((response) => {
        survivalProbability.value = (100 * response.data.survival_probability) as number
      })
      .catch(() => {
        alert('エラーが発生しました。')
      })
  }
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
    <template v-if="survivalProbability !== undefined">
      <div class="alert alert-error mt-4">あなたの生存確率は{{ Math.round(survivalProbability) }}%です。</div>
    </template>
  </div>
</template>
