<template>
    <canvas id="canvas" width="600" height="400"></canvas>
</template>

<script lanbg="ts">
import { Component, Vue } from 'vue-property-decorator';
import * as THREE from "three";
@Component
export default class Three extends Vue {
    scene = new THREE.Scene();
    renderer = null;
    camera = new THREE.PerspectiveCamera(75, 600 / 400, 0.1, 1000);
    light = new THREE.DirectionalLight(0xffffff);
    geometry = new THREE.BoxGeometry(1, 1, 1);
    material = new THREE.MeshNormalMaterial();
    cube = new THREE.Mesh(this.geometry, this.material);

    mounted() {
        const $canvas = document.getElementById("canvas");
        // canvasを後付けで設定する方法あったら教えてほしいー
        this.renderer = new THREE.WebGLRenderer({
            antialias: true,
            canvas: $canvas
        });
        this.camera.position.set(0, 0, 2);
        this.light.position.set(0, 0, 10);
        this.scene.add(this.cube);
        this.scene.add(this.light);

        this.animate();
    }

    animate() {
      requestAnimationFrame(this.animate);

      this.cube.rotation.x += 0.02;
      this.cube.rotation.y += 0.02;

      this.renderer.render(this.scene, this.camera);
    }
}
</script>

<style>

</style>