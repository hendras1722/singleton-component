## VUE 3 Singleton Component

Vue 3 Singleton Component for not attach components to html or templates

\*\* only runs on the client-side

## Installation

```
npm i vue3-singleton-component
```

## Usage

#### Vue 3

component Modal

```vue3Component (modal.vue)
<template>
  <div v-if="Open" style="position: absolute; float: left; left: 50%; top: 50%; transform: translate(-50%, -50%); z-index: 9999">
      Hello world
  </div>
</template>

<script setup lang="ts">
const Open = ref(false)

function Open(){
 Open = true
}

function Close(){
 Open = false
}


defineExpose({
  Open,
  Close
})
</script>
```

utils (useSingleTon.ts)

```utils
import {useSingleton} from 'vue3-singleton-component'

export async function handleOpenModal(){
  const modal = await useSingleton(Modal)
  modal.Open()
}
```

Pages

```vue3
<template>
  <button @click="handleOpenModal">Open Modal</button>
</template>

<script setup lang="ts">
import {handleOpenModal} from './utils/useSingleTon'
</script>
```

#### Nuxt

component

```Nuxt3Component
<template>
  <div v-if="Open" style="position: absolute; float: left; left: 50%; top: 50%; transform: translate(-50%, -50%); z-index: 9999">
      Hello world
  </div>
</template>

<script setup lang="ts">
const Open = ref(false)

function Open(){
 Open = true
}

function Close(){
 Open = false
}


defineExpose({
  Open,
  Close
})
</script>
```

Create Composable

```Composable
import { useSingleton, removeSingleton } from 'vue3-singleton-component'
import PComponent from '@/components/Modal.vue'

interface inCom {
  Open: Function
}

export async function useSingleTonCreate() {
  const inCom: any = await useSingleton(Modal)
  return toRaw(inCom)
}

export async function useSingletonDelete() {
  const inCom: any = await removeSingleton(Modal)
  return toRaw(inCom)
}
```

Pages

```vue3
<template>
  <button @click="handleOpenModal">Open Modal</button>
</template>

<script setup lang="ts">
const {useSingleTonCreate} = "vue3-singleton-component"

async function handleOpenModal(){
  const modal = await useSingleTonCreate()
  modal.Open()
}
</script>
```
