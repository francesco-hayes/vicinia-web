<template>
  <div class="home">
    <div id="container">

    </div>
  </div>
</template>

<style lang="scss" scoped>

</style>


<script>
import * as THREE from 'three'
// import { Float32Attribute, PointsMaterial, Points } from 'three';

export default {
  name: 'home',
  data () {
    return {
      camera: Function,
      scene: Function,
      renderer: Function,
      particles: 100000,
    }
  },
  components: {
    
  },
  beforeMount () {
    var colors = []
    var positions = []

    this.init(colors, positions);
    this.animate();

    // var particlesData = [];
    // var particlePositions = new Float32Array( this.particleCount * 3);

    // this.init(particlesData, particlePositions);
    // this.animate(particlesData, particlePositions);
  },
  methods: {

    init(colors, positions) {
      //
      this.camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 5, 3500 );
      this.camera.position.set(0,0,3000);
      this.scene = new THREE.Scene();
      this.scene.background = new THREE.Color( 0x050505 );
      this.scene.fog = new THREE.Fog( 0x050505, 2000, 3500 );
      

      var geometry = new THREE.BufferGeometry();
      var color = new THREE.Color();
      var r = 1000, r2 = r / 2; // particles spread in the sphere
      for ( var i = 0; i < this.particles; i++ ) {
        // positions
        var x = Math.random() * (r - (-r)) + (-r);
        var y = Math.min((Math.random() * (r - 0) + 0), Math.sqrt((r*r)-(x*x)));
        var z = Math.min((Math.random() * (r - 0) + 0), Math.sqrt((r*r)-(y*y)-(x*x)));

        if (i % 2) {
          y = -y; 
        }
        if (i % 3) {
          z = -z;
        }

        positions.push( x, y, z );
        // colors
        var vx = ( x / r ) + 0.5;
        var vy = ( y / r ) + 0.5;
        var vz = ( z / r ) + 0.5;
        color.setRGB( vx, vy, vz );
        colors.push( color.r, color.g, color.b );
      }
      geometry.addAttribute( 'position', new THREE.Float32BufferAttribute( positions, 3 ) );
      geometry.addAttribute( 'color', new THREE.Float32BufferAttribute( colors, 3 ) );
      geometry.computeBoundingSphere();
      //
      var material = new THREE.PointsMaterial( { size: 15, vertexColors: THREE.VertexColors } );
      this.points = new THREE.Points( geometry, material );
      this.scene.add( this.points );
      //
      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setPixelRatio( window.devicePixelRatio );
      this.renderer.setSize( window.innerWidth, window.innerHeight );
      document.body.appendChild( this.renderer.domElement );

      //
      window.addEventListener( 'resize', this.onWindowResize, false );
    },
    
    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize( window.innerWidth, window.innerHeight );
    },

    animate() {
      requestAnimationFrame( this.animate );
      this.render();
    },

    render() {
      var time = Date.now() * 0.001;
      this.points.rotation.x = time * 0.25;
      this.points.rotation.y = time * 0.5;
      this.renderer.render( this.scene, this.camera );
    }
    
    // init(particlesData, particlePositions) {

    //   this.camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 1, 4000);
    //   this.camera.position.z = 1750;

    //   this.scene = new THREE.Scene();

    //   var group = new THREE.Group();
    //   this.scene.add( group );

    //   var helper = new THREE.BoxHelper( new THREE.Mesh( new THREE.BoxBufferGeometry( this.r, this.r, this.r ) ) );
    //   helper.material.color.setHex(0x080808);
    //   helper.material.blending = THREE.AdditiveBlending;
    //   helper.material.transparent = true;
    //   group.add(helper);

    //   var segments = this.particleCount * this.particleCount;

    //   this.positions = new Float32Array(segments * 3);
    //   this.colors = new Float32Array(segments * 3);

    //   var pMaterial = new THREE.PointsMaterial({
    //     color: 0x0c57fb,
    //     size: 3,
    //     blending: THREE.AdditiveBlending,
    //     transparent: true,
    //     sizeAttenuation: false
    //   });

    //   this.particles = new THREE.BufferGeometry();
    //   // particlePositions = new Float32Array( this.particleCount * 3);

    //   for (var i = 0; i < this.particleCount; i++) {
    //     var x = Math.random() * this.r - this.r / 2;
    //     var y = Math.random() * this.r - this.r / 2;
    //     var z = Math.random() * this.r - this.r / 2;

    //     particlePositions[i * 3] = x;
    //     particlePositions[i * 3 + 1] = y;
    //     particlePositions[i * 3 + 2] = z;

    //     particlesData.push({
    //       velocity: new THREE.Vector3( -1 + Math.random() * 2, -1 + Math.random() * 2, -1 + Math.random() * 2),
    //       numConnections: 0,
    //     });
    //   }

    //   this.particles.setDrawRange(0, this.particleCount);
    //   this.particles.addAttribute('position', new THREE.BufferAttribute(particlePositions, 3));

    //   // Create particle system
    //   this.pointCloud = new THREE.Points(particlePositions, pMaterial);
    //   group.add(this.pointCloud);

    //   var geometry = new THREE.BufferGeometry();
    //   geometry.addAttribute('position', new THREE.BufferAttribute(this.positions, 3));
    //   geometry.addAttribute('color', new THREE.BufferAttribute(this.colors, 3));

    //   geometry.computeBoundingSphere();
    //   geometry.setDrawRange(0, 0);

    //   var material = new THREE.LineBasicMaterial({
    //     vertexColors: THREE.VertexColors,
    //     blending: THREE.AdditiveBlending,
    //     transparent: true
    //   });

    //   this.linesMesh = new THREE.LineSegments(geometry, material);
    //   group.add(this.linesMesh);

    //   // Render the scene
    //   this.renderer = new THREE.WebGLRenderer({antialias: true});
    //   this.renderer.setPixelRatio(window.devicePixelRatio);
    //   this.renderer.setSize(window.innerWidth, window.innerHeight);

    //   this.renderer.gammaInput = true;
    //   this.renderer.gammaOutput = true;

    //   document.body.appendChild( this.renderer.domElement );

    //   //window.addEventListener('resize', this.onWindowResize, false);

    // },
    // animate(particlesData, particlePositions){
    //   var vertexpos = 0;
    //   var colorpos = 0;
    //   var numConnected = 0;

    //   var effectController = {
    //     showDots: true,
		// 		showLines: true,
		// 		minDistance: 150,
		// 		limitConnections: false,
		// 		maxConnections: 20,
		// 		particleCount: 500
    //   }

    //   for ( var i = 0; i < this.particleCount; i ++ )
    //     particlesData[ i ].numConnections = 0;

    //   for ( var i = 0; i < this.particleCount; i ++ ) {
    //     // get the particle
    //     var particleData = particlesData[ i ];
    //     particlePositions[ i * 3 ] += particleData.velocity.x;
    //     particlePositions[ i * 3 + 1 ] += particleData.velocity.y;
    //     particlePositions[ i * 3 + 2 ] += particleData.velocity.z;

    //     if ( particlePositions[ i * 3 + 1 ] < - this.rHalf || particlePositions[ i * 3 + 1 ] > this.rHalf )
    //       particleData.velocity.y = - particleData.velocity.y;

    //     if ( particlePositions[ i * 3 ] < - this.rHalf || particlePositions[ i * 3 ] > this.rHalf )
    //       particleData.velocity.x = - particleData.velocity.x;

    //     if ( particlePositions[ i * 3 + 2 ] < - this.rHalf || particlePositions[ i * 3 + 2 ] > this.rHalf )
    //       particleData.velocity.z = - particleData.velocity.z;

    //     if ( effectController.limitConnections && particleData.numConnections >= effectController.maxConnections )
    //       continue;
    //     // Check collision
    //     for ( var j = i + 1; j < this.particleCount; j ++ ) {
    //       var particleDataB = particlesData[ j ];
    //       if ( effectController.limitConnections && particleDataB.numConnections >= effectController.maxConnections )
    //         continue;
    //       var dx = particlePositions[ i * 3 ] - particlePositions[ j * 3 ];
    //       var dy = particlePositions[ i * 3 + 1 ] - particlePositions[ j * 3 + 1 ];
    //       var dz = particlePositions[ i * 3 + 2 ] - particlePositions[ j * 3 + 2 ];
    //       var dist = Math.sqrt( dx * dx + dy * dy + dz * dz );

    //       if ( dist < effectController.minDistance ) {
    //         particleData.numConnections ++;
    //         particleDataB.numConnections ++;
    //         var alpha = 1.0 - dist / effectController.minDistance;
    //         this.positions[ vertexpos ++ ] = particlePositions[ i * 3 ];
    //         this.positions[ vertexpos ++ ] = particlePositions[ i * 3 + 1 ];
    //         this.positions[ vertexpos ++ ] = particlePositions[ i * 3 + 2 ];
    //         this.positions[ vertexpos ++ ] = particlePositions[ j * 3 ];
    //         this.positions[ vertexpos ++ ] = particlePositions[ j * 3 + 1 ];
    //         this.positions[ vertexpos ++ ] = particlePositions[ j * 3 + 2 ];
    //         this.colors[ colorpos ++ ] = alpha;
    //         this.colors[ colorpos ++ ] = alpha;
    //         this.colors[ colorpos ++ ] = alpha;
    //         this.colors[ colorpos ++ ] = alpha;
    //         this.colors[ colorpos ++ ] = alpha;
    //         this.colors[ colorpos ++ ] = alpha;
    //         numConnected ++;
    //       }
    //     }
    //   }
    //   this.linesMesh.geometry.setDrawRange( 0, numConnected * 2 );
    //   //this.linesMesh.geometry.attributes.position.needsUpdate = true;
    //   this.linesMesh.geometry.attributes.color.needsUpdate = true;
    //   //this.pointCloud.geometry.attributes.position.needsUpdate = true;
    

    //   requestAnimationFrame(this.animate);
    //   this.render();
    // },
    // render() {
    //   this.renderer.render(this.scene, this.camera);
    // },
  }
}
</script>
