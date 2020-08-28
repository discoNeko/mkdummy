<template>
  <div class="hello">
    <div v-html="parsedMock"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    schema: String,
    i: Number,
  },
  computed: {
    // @todo add sanitize
    parsedMock () {
      const b = this.schema
        .replace(/\t/g, ': \'')
        .replace(/\n/g, '\',<br>  ')
      const c = b
        .replace(/'String'/g, '\'hoge' + this.i + '\'')
        .replace(/'Number'/g, this.i)
        .replace(/'Boolean'/g, 'true')
        .replace(/'Timestamp'/g, 1234567890 + this.i)
      const d = c
        .replace(/'Array \[ String \]'/g, '[ \'hoge\' ]')
        .replace(/'Array \[ Number \]'/g, '[ 1234 ]')
        .replace(/'Array \[ Boolean \]'/g, '[ true ]')
      return '{<br>' + d + '},'
    },
  },
}
</script>
