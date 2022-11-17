<script>
  import { MeshStandardMaterial, SphereBufferGeometry } from "three";
  import {
    Canvas,
    Mesh,
    AmbientLight,
    SpotLight,
    DirectionalLight,
  } from "@threlte/core";
  import { Environment } from "@threlte/extras";
</script>

<AmbientLight intensity={0.25} />
<SpotLight
  intensity={1}
  angle={0.2}
  penumbra={1}
  position={[30, 30, 30]}
  castShadow
  shadow-mapSize={[512, 512]}
/>
<DirectionalLight intensity={5} position={[-10, -10, -10]} color="purple" />
