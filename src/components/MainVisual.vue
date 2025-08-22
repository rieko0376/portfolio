<template>
  <section>
    <div id="mainvisual">
      <canvas ref="canvas"></canvas>
      <h1>Miyamoto’s <br />Portfolio</h1>
      <div id="scroll">
        <p>scroll</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

// canvas参照
const canvas = ref(null)
let ctx
let animationId

//波の設定
let t = 0
let waves = []

// メインビジュアルの高さ計算
const setVH = () => {
  const vh = window.innerHeight * 0.01
  document.documentElement.style.setProperty('--vh', `${vh}px`)
}

// 波の描画処理
function drawWave(wave, width, height) {
  //パスを開始（新しい図形）
  ctx.beginPath()
  //開始位置(x,y)
  ctx.moveTo(0, wave.offset)
  for (let x = 0; x <= width; x++) {
    const y =
      wave.amplitude * Math.sin((x / wave.wavelength) * 2 * Math.PI + t * wave.speed) + wave.offset
    //線を描く
    ctx.lineTo(x, y)
  }
  //波の下側を閉じて塗りつぶす
  ctx.lineTo(width, height)
  ctx.lineTo(0, height)
  // パスを閉じる
  ctx.closePath()
  // 塗りつぶしの色指定
  ctx.fillStyle = wave.color
  // 塗りつぶし
  ctx.fill()

  // 波の線を描く
  ctx.strokeStyle = wave.strokeColor
  // 線の太さ
  ctx.lineWidth = 0.8
  // 線を描画
  ctx.stroke()
}

function draw() {
  const c = canvas.value
  const width = c.width
  const height = c.height

  // 透明に戻す
  ctx.clearRect(0, 0, width, height)
  ctx.fillStyle = '#F4F8F6' //背景色
  // 四角形を塗りつぶし
  ctx.fillRect(0, 0, width, height)

  for (let wave of waves) {
    drawWave(wave, width, height)
  }

  // 時間
  t += 1
  //　次のフレームでもう一度draw関数を呼ぶ
  animationId = requestAnimationFrame(draw)
}

onMounted(() => {
  //#mainvisualの高さ--vhに代入
  setVH()
  window.addEventListener('resize', setVH)

  const c = canvas.value
  c.width = window.innerWidth
  c.height = window.innerHeight
  ctx = c.getContext('2d')

  // 中央に波を配置
  const center = c.height * 0.25

  // 波の設定（奥　→　手前）
  waves = [
    { amplitude: 15, wavelength: 600, speed: 0.008, offset: center -15, color: 'rgba(166, 207, 152, 0.35)', strokeColor: '#2E5939' },
    { amplitude: 13, wavelength: 450, speed: 0.006, offset: center, color: 'rgba(166, 207, 152, 0.45)', strokeColor: '#FFF' },
    { amplitude: 10, wavelength: 500, speed: 0.010, offset: center + 10, color: 'rgba(166, 207, 152, 0.55)', strokeColor: '#2E5939' }
  ]
  draw()
})

onBeforeUnmount(() => {
  //#mainvisualの高さ--vhの数値を削除
  window.removeEventListener('resize', setVH)
  cancelAnimationFrame(animationId)
})
</script>

<style scoped>
#mainvisual {
  position: relative;
  height: calc(var(--vh, 1vh) * 100 - var(--height_menu));
  background-color: var(--lightgreen);
  scroll-margin-top: var(--pagelink);
  overflow: hidden;
}

canvas {
  position: absolute;
  top: 0;
  left: 0;
}

#mainvisual h1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  font-size: 2rem;
  color: #fff;
  line-height: 1.5;
  letter-spacing: 0.2rem;
  text-align: center;
}

#mainvisual #scroll {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 5vw;
  height: 20vw;
}

#mainvisual #scroll::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 1px;
  height: 32px;
  background-color: #fff;
  border-radius: 1px;
  animation: drawline 2.5s ease-in-out infinite;
}

@keyframes drawline {
  0% {
    transform: scale(1, 0);
    transform-origin: 0 0;
  }

  30% {
    transform: scale(1, 1);
    transform-origin: 0 0;
  }

  70% {
    transform: scale(1, 1);
    transform-origin: 0 100%;
  }

  100% {
    transform: scale(1, 0);
    transform-origin: 0 100%;
  }
}

#mainvisual #scroll p {
  font-size: 1rem;
  color: #fff;
}

/* PC版　*/
@media (min-width: 1024px) {
  #mainvisual {
    height: calc(var(--vh, 1vh) * 100 - var(--height_menu_pc));
    scroll-margin-top: var(--pagelink_pc);
  }

  #mainvisual h1 {
    font-size: 4rem;
  }

  #mainvisual #scroll {
    position: absolute;
    bottom: 20px;
    height: 80px;
  }

  #mainvisual #scroll p {
    font-size: 1.2rem;
  }
}
</style>