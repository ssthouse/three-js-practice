<template>
  <div class="hello" id="webglContiner">
  </div>
</template>

<script>
import * as Three from 'three'

export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      Three
    }
  },
  methods: {
    init() {
      const scene = new this.Three.Scene()
      const camera = new this.Three.PerspectiveCamera(
        45,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      )
      const renderer = new this.Three.WebGLRenderer()
      renderer.setClearColor(0xeeeeee)
      renderer.setSize(window.innerWidth, window.innerHeight)

      const axes = new this.Three.AxesHelper(20)
      scene.add(axes)

      const planeGeometry = new this.Three.PlaneGeometry(60, 20, 1, 1)
      const planeMaterial = new this.Three.MeshBasicMaterial({
        color: 0xcccccc
      })
      const plane = new this.Three.Mesh(planeGeometry, planeMaterial)

      plane.rotation.x = -0.5 * Math.PI
      plane.position.x = 15
      plane.position.y = 0
      plane.position.z = 0
      scene.add(plane)

      const cubeGeometry = new this.Three.BoxGeometry(4, 4, 4)
      const cubeMaterial = new this.Three.MeshBasicMaterial({
        color: 0xff0000,
        wireframe: true
      })
      const cube = new this.Three.Mesh(cubeGeometry, cubeMaterial)
      cube.position.y = 2
      scene.add(cube)

      const sphereGeometry = new this.Three.SphereGeometry(4, 20, 20)
      const sphereMaterial = new this.Three.MeshBasicMaterial({
        color: 0x7777ff,
        wireframe: true
      })
      const sphere = new this.Three.Mesh(sphereGeometry, sphereMaterial)
      sphere.position.y = 10
      scene.add(sphere)

      camera.position.x = -30
      camera.position.y = 40
      camera.position.z = 30
      camera.lookAt(scene.position)

      document.getElementById('webglContiner').appendChild(renderer.domElement)
      renderer.render(scene, camera)
    }
  },
  created() {
    window.onload = this.init
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  height: 100%;
}
h1,
h2 {
  font-weight: normal;
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
