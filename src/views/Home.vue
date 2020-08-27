<template>
  <div class="home">
    <textarea class="home__input" v-model="schema" />
    <div class="home__output" v-html="parsedText" />
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      schema: '',
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
    // @todo add sanitize
    parsedText () {
      const b = this.schema.replace(/\t/g, ': \'').replace(/\n/g, '\',<br>  ')
      const c = b.replace(/'String'/g, '\'hoge\'').replace(/'Number'/g, '1234').replace(/'Boolean'/g, 'true').replace(/'Timestamp'/g, '1234567890')
      const d = c.replace(/'Array \[ String \]'/g, '[ \'hoge\' ]').replace(/'Array \[ Number \]'/g, '[ 1234 ]')
      return 'const json = {<br>' + d + '}'
    },
  },
}
</script>

<style scoped lang="scss">
.home {
  &__input {
    width: 300px;
    height: 250px;
  }
}
</style>
