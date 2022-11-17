<script>
  import {
    CircleBufferGeometry,
    MeshBasicMaterial,
    MeshStandardMaterial,
    SphereBufferGeometry,
  } from "three";
  import { Mesh, useFrame } from "@threlte/core";
  import { get } from "svelte/store";

  import { Text } from "@threlte/extras";
  export let i, _;
  let position = { x: _.x, y: _.y };
  let distance = { x: 0, y: 0 };
  let arrayLength = 3;
  let loop = { x: 0, y: 0 };
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
    ? new MeshStandardMaterial({
        color: "#eb2d92",
        roughness: 0,
        envMapIntensity: 1,
        emissive: "#b80966",
      })
    : i === 4
    ? new MeshStandardMaterial({
        color: "#7cb2d6",
        roughness: 0,
        envMapIntensity: 0.2,
        emissive: "#213e52",
      })
    : i === 8
    ? new MeshStandardMaterial({
        color: "black",
        roughness: 0,
        envMapIntensity: 0.8,
        emissive: "#b80966",
      })
    : new MeshStandardMaterial({
        color: "#4d9ae3",
        roughness: 0,
        envMapIntensity: 0.6,
        emissive: "#b80966",
      })}
/>
<Mesh
  geometry={new CircleBufferGeometry(0.1, 24)}
  material={new MeshBasicMaterial({ color: "white" })}
  position={{ x: position.x, y: position.y, z: -0.01 }}
/>

<Text
  text={i}
  position={{ x: position.x - 0.02, y: position.y + 0.04 }}
  color="black"
/>
