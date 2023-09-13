<template>
  <div>
    <DinoSVG />
  </div>
</template>

<script>
import { random } from '@/utils'
import { character } from '../character.mixin'
import DinoSVG from './DinoSVG.vue'
import { LOOP, LOOP_EASE_IN_OUT } from '../../../constants'

const SONGS = [
  // Lil Tjay - Calling My Phone
  'https://open.spotify.com/track/3J8EOeKLTLXORtWPpOU5bE?si=766cdc56a9db459f',
  // Lil Tjay - F.N
  'https://open.spotify.com/track/0RLLvYBopDwooCyvnTwgYu?si=55766e3a0421434c',
  // KR$NA - No Cap
  'https://open.spotify.com/track/1XdUEm2MwB6ysy6E80ltMg?si=fea1827b6ef14d85',
  // Russ - Bornfire
  'https://open.spotify.com/track/0MROyfaRrhcwpwEA8eBqdA?si=dccab3679e334e21',
  //KR$NA - Still Standing
  'https://open.spotify.com/track/2JQI6C3UCEIr7SF23ar3qy?si=14e22f0e869b4fec',
  // KR$NA - NGL
  'https://open.spotify.com/track/58h9f4lWnyLPIwqucWydxj?si=493779f0c6f945ea',
  // KR$NA - Hola Amigo
  'https://open.spotify.com/track/19pHSvXUwErAXFktkvYMk9?si=c268593180d24795',
]

export default {
  name: 'DinoCharacter',
  components: { DinoSVG },
  mixins: [character],
  data() {
    return {
      rhythm: 0.3,
      song: random(1, 4),
    }
  },
  methods: {
    init() {
      const head = document.querySelector('.dino-head')
      const leftArm = document.querySelector('.dino-l-arm')
      const rightArm = document.querySelector('.dino-r-arm')
      const leftLeg = document.querySelector('.dino-l-leg')
      const rightLeg = document.querySelector('.dino-r-leg')
      const tail = document.querySelector('.dino-tail')
      const eye = document.querySelector('.dino-eye')
      const headphone = document.querySelector('.dino-headphone')
      const bright = document.querySelector('.dino-bright')
      const teeth1 = document.querySelector('#dino .teeth1')
      const teeth2 = document.querySelector('#dino .teeth2')
      const mouthChillout = document.querySelector('#dino .mouth-chillout')
      const mouthFuckYeah = document.querySelector('#dino .mouth-fuck-yeah')
      let rotationZ = this.rhythm * 32

      // dance to the song rythm
      switch (this.song) {
        case 1:
          // Pink Floyd - Dogs
          bright.style.display = 'none'
          teeth1.style.display = 'none'
          teeth2.style.display = 'none'
          mouthChillout.style.display = 'none'
          mouthFuckYeah.style.display = ''
          break
        case 2:
          // The Doors - Spanish Caravan
          rotationZ = this.rhythm * 8
          this.rhythm = 1
          bright.style.display = 'none'
          teeth1.style.display = 'none'
          teeth2.style.display = 'none'
          mouthChillout.style.display = 'none'
          mouthFuckYeah.style.display = ''
          break
        case 3:
          // BadBadNotGood - Speaking Gently
          this.rhythm = 0.2
          break
      }

      // add song link
      document.querySelector('.dino-head').addEventListener('click', () => {
        window.open(SONGS[this.song - 1])
      })

      this.loop
        .addLabel('start', 0)
        .to(
          leftLeg,
          this.rhythm,
          {
            skewX: -20,
            transformOrigin: '50% 100%',
            ...LOOP,
          },
          'start'
        )
        .to(
          rightLeg,
          this.rhythm,
          {
            skewX: 20,
            transformOrigin: '50% 100%',
            ...LOOP,
          },
          'start'
        )
        .to(
          headphone,
          this.rhythm / 2,
          {
            scale: 1.1,
            transformOrigin: '20% 20%',
            ...LOOP,
          },
          'start'
        )
        .to(
          [leftArm, rightArm],
          this.rhythm,
          {
            yPercent: 20,
            ...LOOP_EASE_IN_OUT,
          },
          'start'
        )
        .to(
          tail,
          this.rhythm,
          {
            transformOrigin: '25% 50%',
            rotationZ: 20,
            ...LOOP_EASE_IN_OUT,
          },
          'start'
        )
        .to(
          head,
          this.rhythm,
          {
            transformOrigin: '85% 100%',
            rotationZ,
            ...LOOP_EASE_IN_OUT,
          },
          'start'
        )

      if (this.song > 2) {
        this.loop
          .fromTo(
            eye,
            0.01,
            {
              scaleY: 0.1,
              transformOrigin: '50% 50%',
            },
            {
              scaleY: 1,
              transformOrigin: '50% 50%',
              repeatDelay: 3,
              ...LOOP,
            },
            'start'
          )
          .fromTo(
            bright,
            0.01,
            {
              autoAlpha: 0,
            },
            {
              autoAlpha: 1,
              repeatDelay: 3,
              ...LOOP,
            },
            'start'
          )
      } else {
        this.loop.set(
          eye,
          {
            scaleY: 0.1,
            transformOrigin: '50% 50%',
          },
          'start'
        )
      }
    },
  },
}
</script>
