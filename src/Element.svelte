<script>
  import { MeshStandardMaterial, SphereBufferGeometry } from "three";
  import { Mesh, useFrame } from "@threlte/core";  import { get } from "svelte/store";

  import { Text } from "@threlte/extras";
  export let i, _;
  let position = { x: _.x, y: _.y };
  let distance = { x: 0, y: 0 };
  let arrayLength = 3;
  let loop = { x: 0, y: 0 };
console.log(_)
  useFrame(({ camera }) => {
    distance.x = Math.round((-_.x + get(camera).position.x) / arrayLength);
    distance.y = Math.round((_.y - get(camera).position.y) / arrayLength);
    if (distance.x !== loop.x) {
      loop.x = distance.x;
      position.x = loop.x * arrayLength + _.x;
    }
    if (distance.y !== loop.y) {
      loop.y = distance.y;
      position.y = -loop.y * arrayLength + _.y;
    }
  });
</script>

<Mesh
  position={{ x: position.x, y: position.y, z: -1 }}
  castShadow
  geometry={new SphereBufferGeometry(0.4)}
  material={i === 1
    ? new MeshStandardMaterial({ color: "red" })
    : i === 4
    ? new MeshStandardMaterial({ color: "blue" })
    : i === 8
    ? new MeshStandardMaterial({ color: "green" })
    : new MeshStandardMaterial({ color: "#333333" })}
/>
<Text text={i} position={{ x: position.x, y: position.y }} color="black" />
