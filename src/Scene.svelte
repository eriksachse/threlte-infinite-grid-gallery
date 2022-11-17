<script>
  import { MeshStandardMaterial, SphereBufferGeometry } from "three";
  import {
    Canvas,
    Mesh,
    AmbientLight,
    SpotLight,
    DirectionalLight,
  } from "@threlte/core";
  import Camera from "./Camera.svelte";
  import Element from "./Element.svelte";
  import Environment from "./Environment.svelte";

  let dragged = { x: 0, y: 0 };
  let pointer = { down: false };
  let pointerstart = { x: 0, y: 0 };

  let positions = [
    { x: -1.2, y: -0.99 },
    { x: 0.05, y: -1.0 },
    { x: 1, y: -0.95 },
    { x: -0.95, y: -0.05 },
    { x: 0, y: 0 },
    { x: 0.97, y: -0.1 },
    { x: -1, y: 0.9 },
    { x: 0.05, y: 1.1 },
    { x: 1.04, y: 1.05 },
  ];

  function pointerdown(e) {
    pointer.down = true;
    pointerstart.x = e.clientX + dragged.x;
    pointerstart.y = e.clientY + dragged.y;
    document.body.style.cursor = "grabbing";
  }
  function pointermove(e) {
    if (pointer.down) {
      dragged.x = pointerstart.x - e.clientX;
      dragged.y = pointerstart.y - e.clientY;
    }
  }
  function pointerup(e) {
    document.body.style.cursor = "grab";
    pointer.down = false;
  }
</script>

<svelte:window
  on:pointerup={pointerup}
  on:pointermove={pointermove}
  on:pointerdown={pointerdown}
/>
<div>
  <Canvas
    ><Environment />
    <Camera dragged={dragged} />
    {#each positions as _, i}
      <Element i={i + 1} _={_} dragged={dragged} />
    {/each}
  </Canvas>
</div>

<style>
  div {
    height: 100vh;
    width: 100vw;
    overflow: hidden;
  }
</style>
