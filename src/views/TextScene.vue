<script>
import * as THREE from "three";
import {FontLoader} from "three/examples/jsm/loaders/FontLoader";

export default {
  name: 'TextScene',
  scene: null,
  camera: null,
  renderer: null,
  methods: {
    setScene() {
      this.scene = new THREE.Scene();

      this.camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 500 );
      this.camera.position.set( 0, 0, 100 );
      this.camera.lookAt( 0, 0, 0 );

      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(this.renderer.domElement);

      const loader = new FontLoader();

      loader.load( 'fonts/helvetiker_regular.typeface.json', ( font ) => {
        console.log(font)

        const geometry = new THREE.TextGeometry( 'Hello three.js!', {
          font: font,
          size: 80,
          height: 5,
          curveSegments: 12,
          bevelEnabled: true,
          bevelThickness: 10,
          bevelSize: 8,
          bevelOffset: 0,
          bevelSegments: 5
        } );

        this.scene.add( geometry );

      } );


    }
  },
  mounted() {
    this.setScene();
    this.renderer.render( this.scene, this.camera );
  }
}

</script>
