<template>
  <div>
    <div>
      <ul class="controls">
        <li class="controls--item">
          <a href="#"
             class="controls--link"
             @click.prevent="open">
            Send content
          </a>
        </li>
        <li class="controls--item">
          <a href="#"
             class="controls--link"
             @click.prevent="close">
            Clear content
          </a>
        </li>
        <li class="controls--item">
          <a href="#"
             class="controls--link"
             @click.prevent="checkTarget">
            has Target?
          </a>
        </li>
        <li class="controls--item">
          <a href="#"
             class="controls--link"
             @click.prevent="checkContent">
            has Content for Target?
          </a>
        </li>
        <li class="controls--item">
          <a href="#"
             class="controls--link"
             @click.prevent="getSource">
            Get the Source name
          </a>
        </li>
      </ul>
    </div>
    <div class="wrapper">
      <container type="destination">
        <portal-target name="programmatic-target"
                       ref="dest" />
      </container>
    </div>
  </div>
</template>

<script>
const { Wormhole } = process.env.NODE_ENV === 'production'
  ? require('../../../dist/portal-vue.js')
  : require('../../../src').default

export default {
  props: {

  },
  data() {
    return {

    }
  },
  methods: {
    open() {
      const passengers = [this.$createElement('p', 'Test-Text from the parent, sent with a button click')]
      Wormhole.open({
        to: 'programmatic-target',
        from: 'programmatic-source',
        passengers,
      })
    },
    close(force = false) {
      Wormhole.close({
        to: 'programmatic-target',
        from: force ? 'wrong-source' : 'programmatic-source',
      }, force)
    },
    checkTarget() {
      const res = Wormhole.hasTarget('programmatic-target')
      window.alert(`Does target content exist? \n${res}`)
    },
    checkContent() {
      const res = Wormhole.hasContentFor('programmatic-target')
      window.alert(`Does Wormhole have content for 'programmatic-target'? \n${res}`)
    },
    getSource() {
      const res = Wormhole.getSourceFor('programmatic-target')
      window.alert(`The source name is: ${res}`)
    },
  },
}
</script>

<style>

</style>
