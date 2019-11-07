<template>
<div>
  作者 1 <br>
  <Editor
    ref="editor1"
    @receiveSteps="receiveSteps"
  />
  作者 2 <br>
  <Editor
    ref="editor2"
    @receiveSteps="receiveSteps"
  />
</div>
</template>

<script>
import Editor from '@/components/Editor.vue'
export default {
  name: 'Notebook',
  components: { Editor },
  data() {
    return {
      authority: {
        steps: [],
        stepClientIDs: []
      }
    }
  },
  methods: {
    receiveSteps(version, steps, clientID) {
      if (version != this.authority.steps.length) return
      steps.forEach(step => {
        this.authority.steps.push(step)
        this.authority.stepClientIDs.push(clientID)
      })
      this.$refs.editor1.updateDoc()
      this.$refs.editor2.updateDoc()
    },
    stepsSince(version) {
      return {
        steps: this.authority.steps.slice(version),
        clientIDs: this.authority.stepClientIDs.slice(version)
      }
    }
  }
}
</script>
