<script>
  import { PerspectiveCamera, PointLight, useFrame } from "@threlte/core";
  import { Environment } from "@threlte/extras";
  import { get } from "svelte/store";
  export let dragged;
  let position = { x: 0, y: 0 };
  useFrame(({ camera }) => {
    get(camera).position.y +=
      (-dragged.y / 100 - get(camera).position.y) * 0.05;
    get(camera).position.x += (dragged.x / 100 - get(camera).position.x) * 0.05;
    position.x += (dragged.x / 100 - position.x) * 0.05;
    position.y += (-dragged.y / 100 - position.y) * 0.05;
  });
</script>

<PerspectiveCamera position={{ z: 100 }} fov={2} />
<PointLight position={{ x: position.x, y: position.y }} />

<Environment
  path="/"
  files="shanghai_riverside_1k.hdr"
  isBackground={false}
  format="hdr"
/>
