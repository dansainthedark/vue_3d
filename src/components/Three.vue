<template>
    <canvas id="canvas" width=width height=height></canvas>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import * as THREE from "three";
import _ from "lodash";
@Component
export default class Three extends Vue {
    // @Prop({ default:0 })
    // postNumber!: number;
    
    scene = new THREE.Scene();
    width = window.innerWidth;
    height = window.innerHeight;
    renderer: THREE.WebGLRenderer | null = null;       
    camera = new THREE.PerspectiveCamera(75, this.width / this.height, 0.1, 1000);
    light = new THREE.DirectionalLight(0xffffff);
    geometry = new THREE.BoxGeometry(1, 1, 1);
    textureCube: THREE.Texture | null = null;
    material = new THREE.MeshBasicMaterial( { color: 0xffffff, envMap: this.textureCube } );
    cube = new THREE.Mesh(this.geometry, this.material);
    


    mounted() {
        this.width = window.innerWidth;
        this.height = window.innerHeight;
        const $canvas = document.getElementById("canvas");
        this.renderer = new THREE.WebGLRenderer({ antialias: true, canvas: $canvas });
        this.camera.position.set(0, 0, 2);
        this.light.position.set(0, 0, 10);

        
        this.scene.add(this.cube);
        this.scene.add(this.light);
        this.animate();
        this.createCubeMap("town");
        window.addEventListener('resize', _.debounce(this.onWindowResize, 200, { maxWait: 800 }));

    }
    beforeDestroy () {
        window.removeEventListener('resize', this.onWindowResize);
    }

    animate() {
      requestAnimationFrame(this.animate);

      this.cube.rotation.x += 0.02;
      this.cube.rotation.y += 0.02;

      if(this.renderer !== null){
        this.renderer.render(this.scene, this.camera);
      }
    }

    createCubeMap(name: string){
        const path = "./assets/img/texture/" + name + "/";
        const format = ".png"
        const urls = [
			path + 'Right' + format, path + 'Left' + format,
			path + 'Top' + format, path + 'Front' + format,
			path + 'Bottom' + format, path + 'Back' + format
		];
        this.textureCube = new THREE.CubeTextureLoader().load( urls );
        this.scene.background = this.textureCube;
        console.log(urls);
    }
    onWindowResize(){
        this.width = window.innerWidth;
        this.height = window.innerHeight;
        this.camera.aspect = this.width / this.height;
		this.camera.updateProjectionMatrix();
        if(this.renderer !== null){
            this.renderer.setSize( window.innerWidth, window.innerHeight );
        }
    }
}
</script>

<style>
    canvas { 
        display: block; 
    }
    body {
        margin: 0;
        padding: 0;
        overflow: hidden;
    }
</style>