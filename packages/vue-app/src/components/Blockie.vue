<template>
  <div class="flex">
    <img :src="blockieSrc" :class="`w-${size} h-${size}`"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator'
import * as blockies from 'blockies-ts'

@Component
export default class Blockie extends Vue {
  @Prop({ required: true }) readonly address: string | undefined

  @Prop({ default: '10' }) readonly size: string | undefined

  copying = false

  get blockieSrc(): string {
    return blockies.create({ seed: this.address }).toDataURL()
  }

  async copy() {
    this.copying = true
    setTimeout(() => { this.copying = false }, 1000)
  }
}
</script>
