<script>
import * as THREE from "three";

export default {
  name: 'LineScene',
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

      const material = new THREE.LineBasicMaterial( { color: 0x0000ff } );

      const points = [];
      points.push( new THREE.Vector3( - 10, 0, 0 ) );
      points.push( new THREE.Vector3( 0, 10, 0 ) );
      points.push( new THREE.Vector3( 10, 0, 0 ) );
      points.push( new THREE.Vector3( 10, 10, 0 ) );
      points.push( new THREE.Vector3( -10, -10, 0 ) );
      points.push( new THREE.Vector3( -15, 10, 0 ) );
      points.push( new THREE.Vector3( -10, 0, 0 ) );

      const geometry = new THREE.BufferGeometry().setFromPoints( points );

      const line = new THREE.Line( geometry, material );

      this.scene.add( line );

    }
  },
  mounted() {
    this.setScene();
    this.renderer.render( this.scene, this.camera );
  }
}

</script>
