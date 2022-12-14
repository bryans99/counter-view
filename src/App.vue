/*
 * The MIT License (MIT)
 *
 * Copyright (c) 2022 Looker Data Sciences, Inc.
 *
 * Permission is hereby granted, free of charge, to any person obtaining a copy
 * of this software and associated documentation files (the "Software"), to deal
 * in the Software without restriction, including without limitation the rights
 * to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 * copies of the Software, and to permit persons to whom the Software is
 * furnished to do so, subject to the following conditions:
 *
 * The above copyright notice and this permission notice shall be included in
 * all copies or substantial portions of the Software.
 *
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 * FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 * AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 * LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
 * THE SOFTWARE.
 */

<template>
  <div class="webpage">
    <h1>Looker Counter Extension (Vue)</h1>
    <h2>Welcome {{ displayName }}</h2>
    <h3>This number will increase by one upon every click:</h3>
    <Button></Button>
    <h3>We hope you had fun with this Looker extension.</h3>
    <img
      width="200"
      src="./looker-logo.svg"
    />
  </div>
</template>

<script>
import { defineAsyncComponent } from 'vue'
import { me } from '@looker/sdk'
import { } from '@looker/extension-sdk'

const Button = defineAsyncComponent(() => import('./Button.vue'))

export default {
  props: {
    extensionSdk: Object,
    sdk: Object,
  },
  data() {
    return {
      displayName: null,
    };
  },
  components: {
    Button,
  },
  async created() {
    try {
      const result = await (await this.sdk.ok(me(this.sdk)))
      this.displayName = result.display_name
    } catch(error) {
      console.error(error) 
      this.displayName = 'Unknown'
    }
  },
};
</script>

<style>
body {
  font-family: -apple-system, system-ui, BlinkMacSystemFont;
  text-align: center;
  font-variant-numeric: tabular-nums;
}
.webpage {
  padding: 100px 0;
}
</style>
