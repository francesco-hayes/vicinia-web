<template>
  <div class="home">
    <div id="screen">
      <div v-if="this.click == 0" class="container">
        <h3>click</h3>
      </div>
      <div id="box_00" class="box">
        <div class="left">
          <h2>Vicinia</h2>
        </div>
        <div class="right">
          <div class="card">
            <p>Discover the highest form of cummication based upon your geolocation.</p>
          </div>
        </div>
      </div>
      <div id="box_01" class="box">
        <div class="left">
          <h2>Scroll</h2>
        </div>
        <div class="right"></div>
      </div>
    </div>
    <div v-show="click == 2" class="cover">
      <div v-animate.fade="'slide-up'" class="block flex__center">
        <p>Working on creating a better future in communication to establish better relationships with those you're around in an innovative manner of the future.</p>
      </div>
      <div v-animate.fade="'slide-up'" class="block flex">
        <div class="left">
          <h2>It's Easy</h2>
        </div>
        <div class="right">
          <img src="@/assets/mobile_01.png" alt="" class="mobile-img">
        </div>
      </div>
      <div v-animate.fade="'slide-up'" class="block flex">
        <div class="left">
          <h2>To Begin Chatting</h2>
        </div>
        <div class="right right_short">
          <img src="" alt="" class="mobile-img">
        </div>
      </div>
      <div v-animate.fade="'slide-up'" class="block flex">
        <div class="left">
          <h2>Hook Up with Pokemon GO</h2>
        </div>
        <div class="right">
          <img src="@/assets/mobile_01.png" alt="" class="mobile-img">
        </div>
      </div>
      <div v-animate.fade="'slide-up'" class="block flex__center">
        <h2>Download the Free APK Below</h2>
        <a href="#">Download</a>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>

.mobile-img {
  -webkit-user-drag: none;
  width: 80%;
}

.block {
  padding: 2rem;
  margin: 0 auto;
  width: 80%;
  height: 100vh;

  & h2 {
    font-size: 2.5rem;
    letter-spacing: 2px;
    margin-bottom: 2rem;
    text-transform: uppercase;
  }
}

.flex {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.flex__center {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.block p {
  font-size: 3rem;
  font-weight: 600;
  letter-spacing: 5px;
}

.home {
  height: 100%;
}

.screen {
  height: inherit;
  position: relative;
  width: inherit;
}

.container {
  position: absolute;
  top: 80%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;

  & h3 {
    font-size: 1.2rem;
    text-align: center;
  }

  & img {
    width: 20rem;
    height: 20rem;
  }
}
.box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  z-index: 100;
  opacity: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;

  & h2 {
    font-size: 5rem;
    font-weight: 600;

  }

  & p {
    font-size: 1.2rem;
  }
}

.left {
  display: flex;
  align-items: center;
  justify-content: center;

  & h2 {
    font-size: 4rem;
    letter-spacing: 2px;
  }
}

.right {
  display: flex;
  align-items: center;
  justify-content: center;
}

.card {
  padding: 0 2rem;
}

.cover {
  width: 100%;
  height: 100%;
  background: #ebf0f4;
}

#elem {
  opacity: 0;
}

</style>


<script>
import * as THREE from 'three'
import {TweenMax, TimelineMax} from 'gsap'
// Scroll Library

// import { Float32Attribute, PointsMaterial, Points } from 'three';

export default {
  name: 'home',
  data () {
    return {
      camera: Function,
      scene: Function,
      renderer: Function,
      material: Function,
      particles: 5000,
      r: 1000,
      click: 0,
    }
  },
  mounted () {
    var positions = []

    this.init(positions);
    this.animate();
    document.getElementById('screen').addEventListener('click', this.onClick, false);
    
    var link = document.querySelectorAll('#link');
    for (let i =0; i < link.length; i ++) {
      link[i].addEventListener('click', ()=> {
        this.click = i;
        this.onClick();
      });
    }

  },
  methods: {

    init(positions) {

      var screen = document.querySelector('#screen');
      //
      this.camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 1, 10000 );
      this.camera.position.set(0,0,3000);
      this.scene = new THREE.Scene();
      this.scene.background = new THREE.Color( 0xebf0f4 );
      //this.scene.fog = new THREE.Fog( 0x050505, 2000, 3500 );
      

      var geometry = new THREE.BufferGeometry();
      var color = new THREE.Color();
      // particles spread in the sphere
      for ( var i = 0; i < this.particles; i++ ) {
        // positions
        var x = Math.random() * (this.r - (-this.r)) + (-this.r);

        var s = Math.sqrt((this.r*this.r)-(x*x));
        var y = Math.random() * (s - (-s)) + (-s);

        var t = Math.sqrt((this.r*this.r)-(y*y)-(x*x));
        var z = Math.random() * (t - (-t)) + (-t);

        positions.push( x, y, z );
      }
      geometry.addAttribute( 'position', new THREE.Float32BufferAttribute( positions, 3 ) );
      geometry.computeBoundingSphere();
      //
      this.material = new THREE.PointsMaterial( { size: 10, color: 0x0c57fb, } );
      this.points = new THREE.Points( geometry, this.material );
      this.scene.add( this.points );
      //
      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setPixelRatio( window.devicePixelRatio );
      this.renderer.setSize( window.innerWidth, window.innerHeight );
      
      screen.appendChild( this.renderer.domElement );

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
      this.points.rotation.x = time * 0.05;
      this.points.rotation.y = time * 0.15;
      this.renderer.render( this.scene, this.camera );
    },

    onClick(event){
      //event.preventDefault();

      var tm = TweenMax;
      var tl = new TimelineMax();
      var dot = document.querySelectorAll('.dot');
      var cover = document.querySelector('#box_00');
      var cover_01 = document.querySelector('#box_01');

      if (this.click == 4) {
        this.click = 0;
      }

      switch(this.click) {
        case 0:
          tl.to(this.camera.position, 1.5, {z: 5000, ease: Power2.easeOut}).to(this.camera.position, 1.5, {z: -5000, ease: Power2.easeOut}).to(cover, 1, {opacity: 1});
          dot[0].classList.remove('active');
          dot[1].className += ' active';
          this.click++;
          break;
        case 1: 
          tl.to(cover, 1, {opacity: 0}).to(this.camera.rotation, 1.5, {y: 4, ease: Power2.easeOut}).to(cover_01, 1, {opacity: 1});
          dot[1].classList.remove('active');
          dot[2].className += ' active';
          this.click++;
          break;
        case 2:
          dot[2].classList.remove('active');
          dot[3].className += ' active';
          this.click++;
          break;
        case 3:
          dot[0].className += ' active';
          dot[3].classList.remove('active');
          this.click++;
          break;
        default:
          dot[0].className += ' active';
          dot[3].classList.remove('active');
          this.click++;
          break;
      }

    }
  }
}
</script>
