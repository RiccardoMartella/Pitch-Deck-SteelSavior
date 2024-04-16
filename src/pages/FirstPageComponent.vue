<template>
  <div class="min-vh-100">
    <div class="logo-container d-flex justify-content-center">
      <img src="/src/assets/logoSteelSaviorimg.png" alt="Logo">
    </div>
    <div ref="container" class="mecha-container" style="height:500px;"></div>
  </div>
</template>

<script>
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader'
import Stats from 'three/examples/jsm/libs/stats.module'

const scene = new THREE.Scene()
scene.add(new THREE.AxesHelper(5))

const light = new THREE.PointLight(0xffffff, 50)
light.position.set(0.8, 1.4, 1.0)
scene.add(light)

const ambientLight = new THREE.AmbientLight()
scene.add(ambientLight)

const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
)
camera.position.set(0.8, 1.4, 1.0)

const renderer = new THREE.WebGLRenderer()
renderer.setSize(window.innerWidth, window.innerHeight)
document.body.appendChild(renderer.domElement)

const controls = new OrbitControls(camera, renderer.domElement)
controls.enableDamping = true
controls.target.set(0, 0, 0)

// Carica il modello FBX mecha
const fbxLoader = new FBXLoader()
fbxLoader.load(
    '/src/assets/mecha.fbx', 
    (object) => {
        scene.add(object)
    },
    (xhr) => {
        console.log((xhr.loaded / xhr.total) * 100 + '% loaded')
    },
    (error) => {
        console.log(error)
    }
)

window.addEventListener('resize', onWindowResize, false)
function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight
    camera.updateProjectionMatrix()
    renderer.setSize(window.innerWidth, window.innerHeight)
    render()
}

const stats = new Stats()
document.body.appendChild(stats.dom)

function animate() {
    requestAnimationFrame(animate)

    controls.update()

    render()

    stats.update()
}

function render() {
    renderer.render(scene, camera)
}

animate()

</script>

<style scoped>
img{
  width: 80%;
}

.logo-container {
  position: relative;
  animation: fallAndBounce 1s ease forwards;
}

.mecha-container {
  position: relative;
}

@keyframes fallAndBounce {
  0% {
    top: -650px;
  }
  50% {
    top: 50vh; 
    transform: translateY(-50%);
  }
  100% {
    top: 0; 
  }
}
</style>
