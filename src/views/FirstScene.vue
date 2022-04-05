<script>
import * as THREE from 'three';

export default {
  cube: null,
  camera: null,
  scene: null,
  renderer: null,
  name: 'FirstScene',
  data() {
    return {
      name: '',
    }
  },
  methods: {
    rotateCube() {
      this.cube.rotation.x += 0.02;
      this.cube.rotation.y += 0.02;
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.rotateCube();
      this.renderer.render(this.scene, this.camera);
    },
    setScene() {
      this.renderer = new THREE.WebGLRenderer();
      this.scene = new THREE.Scene();
      this.camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

      this.renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(this.renderer.domElement);

      const geometry = new THREE.BoxGeometry();
      const material = new THREE.MeshBasicMaterial({color: 0x00ffff});
      this.cube = new THREE.Mesh(geometry, material);
      this.scene.add(this.cube);

      this.camera.position.z = 3;
    }
  },
  mounted() {
    this.setScene();
    this.animate();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
