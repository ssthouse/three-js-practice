<template>
  <div class="hello" id="webglContiner">
  </div>
</template>

<script>
import * as Three from 'three'
import Stats from 'stats-js'

export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      Three,
      Stats,
      scene: null,
      camera: null,
      render: null,
      cube: null
    }
  },
  methods: {
    init() {
      this.scene = new this.Three.Scene()
      this.camera = new this.Three.PerspectiveCamera(
        45,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      )
      this.renderer = new this.Three.WebGLRenderer()
      this.renderer.setClearColor(0xeeeeee, 1.0)
      this.renderer.setSize(window.innerWidth, window.innerHeight)
      this.renderer.shadowMap.enabled = true

      const axes = new this.Three.AxesHelper(20)
      this.scene.add(axes)

      const spotLight = new this.Three.SpotLight(0xffffff)
      spotLight.position.set(-40, 60, -10)
      this.scene.add(spotLight)

      const planeGeometry = new this.Three.PlaneGeometry(60, 20)
      const planeMaterial = new this.Three.MeshLambertMaterial({
        color: 0xffffff
      })
      const plane = new this.Three.Mesh(planeGeometry, planeMaterial)

      plane.rotation.x = -0.5 * Math.PI
      plane.position.x = 15
      plane.position.y = 0
      plane.position.z = 0
      plane.receiveShadow = true
      this.scene.add(plane)

      const cubeGeometry = new this.Three.BoxGeometry(4, 4, 4)
      const cubeMaterial = new this.Three.MeshLambertMaterial({
        color: 0xff0000ff
      })
      this.cube = new this.Three.Mesh(cubeGeometry, cubeMaterial)
      this.cube.position.y = 2
      this.cube.castShadow = true
      this.scene.add(this.cube)

      const sphereGeometry = new this.Three.SphereGeometry(4, 20, 20)
      const sphereMaterial = new this.Three.MeshLambertMaterial({
        color: 0x7777ffff
      })
      const sphere = new this.Three.Mesh(sphereGeometry, sphereMaterial)
      sphere.position.x = 10
      sphere.position.y = 4
      sphere.castShadow = true
      this.scene.add(sphere)

      this.camera.position.x = -30
      this.camera.position.y = 40
      this.camera.position.z = 30
      this.camera.lookAt(this.scene.position)

      document
        .getElementById('webglContiner')
        .appendChild(this.renderer.domElement)
      this.renderer.render(this.scene, this.camera)
    },
    showFps() {
      this.stats = new this.Stats()
      this.stats.domElement.style.position = 'absolute'
      this.stats.domElement.style.left = '0px'
      this.stats.domElement.style.top = '0px'
      document.body.appendChild(this.stats.domElement)
    },
    renderScene() {
      this.stats.update()
      requestAnimationFrame(this.renderScene)
      this.cube.rotation.x += 0.1
      this.cube.rotation.y += 0.1
      this.renderer.render(this.scene, this.camera)
    }
  },
  created() {
    const self = this
    window.onload = function() {
      self.init()
      self.showFps()
      self.renderScene()
    }
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
