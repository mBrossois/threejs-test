<script>
import * as THREE from "three";
import {GLTFLoader} from "three/examples/jsm/loaders/GLTFLoader";

export default {
  name: 'LoadModalScene',
  scene: null,
  camera: null,
  renderer: null,
  gltfScene: null,
  methods: {
    rotateScene(){
      this.gltfScene.rotation.y += 0.002
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.renderer.render(this.scene, this.camera);
      this.rotateScene();
    },
    setScene() {
      this.scene = new THREE.Scene();

      this.camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
      this.camera.position.set( 0, 0, 20 );
      this.camera.lookAt( 0, 0, 0 );

      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(this.renderer.domElement);

      const ambientLight = new THREE.AmbientLight(0xBBBBBB);
      this.scene.add(ambientLight);
      const loader = new GLTFLoader();

      loader.load('sakura_cherry_blossom/scene.gltf',  (gltf) => {
        this.gltfScene = gltf.scene;
        this.scene.add(this.gltfScene);
        this.animate()

      }, undefined, function (error) {

        console.error(error);

      });

    }
  },
  mounted() {
    this.setScene();
  }
}

</script>
