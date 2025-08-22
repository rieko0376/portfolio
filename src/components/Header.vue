<template>
  <header>
    <div id="headarea">

      <div id="h_logo">
        <a href="#">
          <p>Miyamoto</p>
        </a>
      </div>

      <div id="hamburger">
        <button @click="toggleMenu" :class="{ open: isOpen }">
          <span class="ham"></span>
          <span class="ham"></span>
          <span class="ham"></span>
          <p>Menu</p>
        </button>
      </div>

      <div id="global_nav" :class="{ open: isOpen }">
        <nav>
          <ul>
            <li><a href="#mainvisual" @click="pageLink">TOP</a></li>
            <li><a href="#about" @click="pageLink">About<span>自己紹介</span></a></li>
            <li><a href="#works" @click="pageLink">Works<span>制作物紹介</span></a></li>
            <li><a href="#vision" @click="pageLink">Vision<span>今後の展望</span></a></li>
            <li><a href="#contact" @click="pageLink">Contact<span>お問い合わせ</span></a></li>
          </ul>
        </nav>
      </div>

    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue';
//メニュー開閉
const isOpen = ref(false);
const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};
//メニュー　スムーズスクロール
const closeMenu = () => {
  isOpen.value = false;
}
const pageLink = (e) => {
  e.preventDefault()
  const link = e.currentTarget
  const href = link.getAttribute('href')
  if (!href || href === '#') { return; }
  const target = document.querySelector(href)
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' })
  }
  closeMenu()
}
</script>

<style scoped>
#headarea {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  height: var(--height_menu);
  background-color: #fff;
  padding: 0 5.3vw;
  border-bottom: 1px solid var(--green);
}

#headarea #h_logo p {
  font-size: 1.5rem;
  color: var(--green);
}

#headarea #hamburger {
  width: 30px;
  height: 35px;
}

#headarea #hamburger button {
  position: relative;
  top: 3px;
  width: 100%;
  height: 100%;
  cursor: pointer;
}

#headarea #hamburger button span.ham {
  display: block;
  position: absolute;
  left: 50%;
  width: 80%;
  height: 2px;
  background-color: var(--green);
  transform: translateX(-50%);
  transition: all 0.3s ease;
}

#headarea #hamburger button span.ham:first-child {
  top: 0;
}

#headarea #hamburger button span.ham:nth-child(2) {
  top: 6px;
}

#headarea #hamburger button span.ham:nth-child(3) {
  top: 12px;
}

#headarea #hamburger button p {
  font-size: var(--txt_min_sp);
  color: var(--green);
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}

#headarea #global_nav {
  position: fixed;
  top: var(--height_menu);
  right: 0;
  width: 80%;
  height: 100vh;
  background-color: var(--green);
  padding: 10vw 8vw;
  transform: translateX(100%);
  opacity: 0;
  pointer-events: none;
  transition: all 0.3s ease;
  z-index: 1;
}

/* メニュー表示時 */
#headarea #hamburger button.open span.ham:first-child {
  transform: translate(-50%,-50%) rotate(45deg);
  top: 1.6vw;
}

#headarea #hamburger button.open span.ham:nth-child(2) {
  opacity: 0;
}

#headarea #hamburger button.open span.ham:nth-child(3) {
  transform: translate(-50%,-50%) rotate(-45deg);
  top: 1.6vw;
}

#headarea #global_nav.open {
  transform: translateX(0);
  opacity: 1;
  pointer-events: auto;
}

#headarea #global_nav ul li {
  font-size: 1.3rem;
  color: #fff;
  line-height: 1.5;
  margin: 0 0 5vw;
  padding: 0 0 1vw;
  border-bottom: 1px solid #fff;
}

#headarea #global_nav ul li a {
  display: block;
  width: 100%;
}

#headarea #global_nav ul li span {
  font-size: 0.8rem;
  margin-left: 1.5rem;
}

/* PC版　*/
@media (min-width: 1024px) {
  #headarea {
    height: var(--height_menu_pc);
  }

  #headarea #hamburger {
    width: 60px;
    height: 50px;
  }

  #headarea #h_logo p {
    font-size: 2rem;
  }

  #headarea #hamburger button {
    top: 3px;
  }

  #headarea #hamburger button span.ham:first-child {
    top: 0;
  }

  #headarea #hamburger button span.ham:nth-child(2) {
    top: 10px;
  }

  #headarea #hamburger button span.ham:nth-child(3) {
    top: 20px;
  }

  #headarea #hamburger button p {
    font-size: var(--txt_min_pc);
  }

  #headarea #global_nav {
    top: var(--height_menu_pc);
    width: 40%;
    padding: 5vw 8vw;
  }

  /* PCメニュー表示時 */
  #headarea #hamburger button.open span.ham:first-child {
    top: 10px;
  }

  #headarea #hamburger button.open span.ham:nth-child(3) {
    top: 10px;
  }

  #headarea #global_nav ul li {
    font-size: 1.6rem;
    margin: 0 0 2vw;
    padding: 0 0 0.3vw;
  }

  #headarea #global_nav ul li span {
    font-size: 1rem;
    margin-left: 1.5rem;
  }
}
</style>