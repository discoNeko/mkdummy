<template>
  <div class="home">
    <textarea class="home__input" v-model="schema" />
    <div class="home__amount">
      <div @click="decreaseAmount">減らす</div>
      <input v-model="amount" type="number" min=1 max=100 />
      <div @click="increaseAmount">増やす</div>
    </div>
    <div @click="copy">クリップボードにコピー</div>
    <div class="home__output" id="mock">
      <div>const mock = [</div>
      <div v-for="i in amount" :key="i">
        <mock :schema="schema" :i="i" />
      </div>
      <div>]</div>
    </div>
  </div>
</template>

<script>
import Mock from '@/components/mock.vue'

export default {
  name: 'Home',
  components: { Mock },
  data () {
    return {
      schema: '',
      amount: 1,
    }
  },
  mounted () {
    /* eslint-disable no-tabs */
    this.schema =
      'name	String\n' +
      'age	Number\n' +
      'isAdmin	Boolean\n' +
      'likes	Array [ String ]\n' +
      'followers	Array [ Number ]\n'+
      'createdAt	Timestamp\n'
  },
  computed: {
  },
  methods: {
    decreaseAmount () {
      if (this.amount > 1) this.amount--
    },
    increaseAmount () {
      if (this.amount < 99) this.amount++
    },
    async copy () {
      const mock = document.getElementById('mock')
      await navigator.clipboard.writeText(mock.innerText)
    },
  },
}
</script>

<style scoped lang="scss">
/* @see https://www.w3schools.com/howto/howto_css_hide_arrow_number.asp */

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}

.home {
  &__input {
    width: 300px;
    height: 250px;
  }
  &__amount {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
