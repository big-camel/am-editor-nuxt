<template>
  <div>
    <am-toolbar v-if="engine" :engine="engine" :items="items" />
    <div ref="container"></div>
  </div>
</template>

<script>
let Component = {
  data: function () {
    return {
      engine: null,
      items: []
    };
  },
}
if (!process.client) {

} else {
  const Engine = require('@aomao/engine').default
  const Heading = require('@aomao/plugin-heading').default
  const AmToolbar = require('am-editor-toolbar-vue2')
  const { ToolbarPlugin, ToolbarComponent } = AmToolbar
  const Codeblock = require('am-editor-codeblock-vue2')
  const { CodeBlockComponent } = Codeblock
  const Bold = require('@aomao/plugin-bold').default

  Component = {
    name: "HelloWorld",
    components: {
      AmToolbar: AmToolbar.default,
    },
    data: function () {
      return {
        engine: null,
        items: [['collapse'],['heading','bold']]
      };
    },
    props: {
      msg: String,
    },
    mounted() {
      const engine = new Engine(
        this.$refs.container,
        {
          cards:[
            ToolbarComponent,
            CodeBlockComponent
          ],
          plugins: [
            Heading,
            ToolbarPlugin,
            Codeblock.default,
            Bold
          ]
        },
      );
      this.engine = engine;
    }
  };
}
export default Component
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
