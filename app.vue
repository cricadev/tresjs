<script setup lang="ts">
import { OrbitControls } from '@tresjs/cientos';

const gl = {
  clearColor: '#82DBC5',
  shadows: true,
  alpha: false,

};

const boxRef = shallowRef()
const { onLoop, pause, resume } = useRenderLoop()
onLoop(({ delta, elapsed }) => {
  if (boxRef.value) {
    boxRef.value.rotation.x += delta

  }
})
const handlePauseGame = () => {
  pause()
  document.getElementById('appear').style.display = 'flex'

}
const handleResumeGame = () => {
  resume()
  document.getElementById('appear').style.display = 'none'
}

</script>

<template>
  <div class="">
    <TresCanvas v-bind="gl" window-size>
      <TresPerspectiveCamera :position="[9, 9, 9]" />
      <OrbitControls :make-default="true" />
      <!-- <TransformControls :object="boxRef" /> -->
      <!-- <PointerLockControls make-default  />
      <KeyboardControls /> -->
      <TresGroup :position="[2, 0, 0]">
        <TresMesh ref="boxRef" cast-shadow>
          <TresBoxGeometry :args="[1, 1, 1]" />
          <TresMeshToonMaterial color="#4F4F4F" />
        </TresMesh>
      </TresGroup>
      <TresMesh @click="pause()" cast-shadow :position="[15, 0, 0]">
        <TresBoxGeometry :args="[3, 3, 3]" />
        <TresMeshToonMaterial color="#f0f" />
      </TresMesh>
      <TresMesh @click="resume()" cast-shadow :position="[-15, 0, 0]">
        <TresBoxGeometry :args="[3, 3, 3]" />
        <TresMeshToonMaterial color="#f0f" />
      </TresMesh>
      <TresDirectionalLight :position="[0, 2, 4]" :intensity="1.2" cast-shadow />
    </TresCanvas>
    <div class="text-white bg-black absolute top-0" @click="handlePauseGame()">

      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
        class="w-12 h-12">
        <path stroke-linecap="round" stroke-linejoin="round"
          d="M14.25 9v6m-4.5 0V9M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
      </svg>

    </div>
    <div id="appear" class="bg-black hidden h-screen w-screen absolute z-10 flex justify-center items-center">
      <div class="flex flex-col items-center">
        <h1 class="text-white">Hello World</h1>
        <svg @click="handleResumeGame()" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
          stroke-width="1.5" stroke="#fff" class="w-12 h-12">
          <path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
          <path stroke-linecap="round" stroke-linejoin="round"
            d="M15.91 11.672a.375.375 0 0 1 0 .656l-5.603 3.113a.375.375 0 0 1-.557-.328V8.887c0-.286.307-.466.557-.327l5.603 3.112Z" />
        </svg>
      </div>

    </div>
  </div>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}

#app {
  height: 100%;
  width: 100%;
  background-color: #000;
}
</style>