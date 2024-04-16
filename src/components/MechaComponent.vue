<script>
import * as THREE from 'three';
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader.js';

export default {
  mounted() {
    this.init();
  },
  methods: {
    init() {
      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      camera.position.z = 5;

      const renderer = new THREE.WebGLRenderer();
      renderer.setSize(window.innerWidth, window.innerHeight);
      this.$refs.container.appendChild(renderer.domElement);

      // Carica il modello 3D utilizzando FBXLoader
      const loader = new FBXLoader();
      loader.load('/src/assets/mecha.fbx', (model) => {
        scene.add(model);

        // Imposta l'animazione
        const animate = () => {
          requestAnimationFrame(animate);
          // Aggiorna l'animazione del modello qui
          renderer.render(scene, camera);
        };
        animate();
      });
    }
  }
}
</script>
