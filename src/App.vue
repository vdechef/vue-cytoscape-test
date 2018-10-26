<template>
  <div id="holder">
    <cytoscape :config="config" :preConfig="preConfig" :afterCreated="afterCreated"/>
  </div>
</template>

<script>
/* eslint-disable */
const config = {
  elements: [
    { // node a
      data: { id: 'a' }
    }, { // node b
      data: { id: 'b' }
    }, { // edge ab
      data: { id: 'ab', source: 'a', target: 'b' }
    }
  ],
  style: [
    {
      selector: 'node',
      style: {
        'background-color': '#666',
        'label': 'data(id)'
      }
    }, {
      selector: 'edge',
      style: {
        'width': 3,
        'line-color': '#ccc',
        'target-arrow-color': '#ccc',
        'target-arrow-shape': 'triangle'
      }
    }
  ],
  layout: {
    name: 'grid',
    rows: 1
  }
}

export default {
  name: 'App',
  data () {
    return {
      config,
      i: 1
    }
  },
  methods: {
    preConfig (cytoscape) {
      console.log('calling pre-config')
	  // let's register a tap event, for instance
      const that = this
      this.$cytoscape.reset()
      this.$cytoscape.instance.then(cy => {
        cy.on('tap', event => {
          console.log('tapped by', that.i, 'time')
          that.i++
        })
      })
    },
    afterCreated (cy) {
      console.log('after created')
    }
  }
}
</script>

<style>
#holder {
  width: 100%;
  height: 400px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
