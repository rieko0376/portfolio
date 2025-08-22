<template>
  <section>
    <div id="works"></div>
    <h2>Works<span>制作物紹介</span></h2>
    <ul class="works_wrap">
      <li class="works_box" v-for="(work, index) in works" :key="index" @click="openModal(work)">
        <div class="work_card">
          <div class="works_img">
            <img :src="work.imgUrl" :alt="work.title" />
            <p>more</p>
          </div>
          <dl>
            <dt>{{ work.title }}</dt>
            <dd>{{ work.desc }}</dd>
          </dl>
        </div>
      </li>
    </ul>

    <div v-if="selectedWork" class="works_d_wrap" @click.self="closeModal">
      <div class="works_d_box">
        <button class="works_close" @click="closeModal">
          <span class="close"></span>
          <span class="close"></span>
        </button>
        <p class="works_d_title">{{ selectedWork.title }}</p>
        <div class="works_d_pc">
          <div class="works_d_img">
            <img :src="selectedWork.imgUrl" :alt="selectedWork.title" />
          </div>
          <div class="works_d_txt">
            <p class="works_d_desc">{{ selectedWork.desc }}</p>
            <a v-if="selectedWork?.link1" :href="selectedWork.link1" class="works_button" target="_blank">{{ selectedWork.linkTxt1 }}</a>
            <a v-if="selectedWork?.link2" :href="selectedWork.link2" class="works_button" target="_blank">{{ selectedWork.linkTxt2 }}</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import imgDummy from '../assets/images/dummy_img.png';

const works = ref([
  {
    title: 'ポートフォリオサイト',
    desc: '本サイトはVue.jsの勉強のために制作しました。WFをFigmaで制作し、GitHub Pagesで公開しました。今後も機能の拡張をする予定のため、シンプルなデザインで制作しています。',
    imgUrl: imgDummy,
    link1: '#',
    linkTxt1:'実際のサイト',
    link2: '',
    linkTxt2:'',
  },
  {
    title: '【制作予定】Todoリストor計算ツール',
    desc: 'ゲーム内の作業を整理するTodoリスト、またはコーディング時のちょっとした計算（vwやline-height等）ができるツールを制作予定です。',
    imgUrl: imgDummy,
    link1: '',
    linkTxt1:'',
    link2: '',
    linkTxt2:'',
  },
]);

const selectedWork = ref(null);

const openModal = (work) => {
  selectedWork.value = work;
  document.body.style.overflow = "hidden";
}

const closeModal = () => {
  selectedWork.value = false
  document.body.style.overflow = ''
}
</script>

<style scoped>
/* カスタム変数 */
.works_wrap,
.works_d_wrap {
  --card_radius: 10px;
}

#works {
  scroll-margin-top: var(--pagelink);
}

.works_wrap {
  margin-top: var(--width_margin_sp);
}

.works_wrap .works_box {
  width: 85%;
  height: var(--height_work_card);
  background-color: #fff;
  margin: 0 auto var(--width_margin_sp);
  border-radius: var(--card_radius);
  border: 1px solid var(--lightgray);
  overflow: hidden;
  cursor: pointer;
}

.work_card a {
  display: block;
  width: 100%;
  height: var(--height_work_card);
}

.work_card .works_img {
  position: relative;
  height: 32vw;
  overflow: hidden;
}

.work_card .works_img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.work_card .works_img p {
  position: absolute;
  bottom: -0.5vw;
  right: 0;
  width: 18.6vw;
  height: 6.6vw;
  background-color: #fff;
  color: var(--green);
  font-size: var(--txt_m_sp);
  padding-left: 2vw;
  border-radius: 10px 0 0 0;
}

.work_card .works_img p::after {
  content: ">";
  position: absolute;
  bottom: 0;
  right: 2vw;
}

.work_card dl {
  padding: 3vw 1rem;
}

.work_card dl dt {
  font-size: var(--txt_m_sp);
  font-weight: var(--txt_bold);
}

.work_card dl dd {
  font-size: var(--txt_min_sp);
  margin-top: 0.5rem;
  max-height: 10vw;
  overflow: hidden;
}

/* 詳細モーダル */
.works_d_wrap {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
}

.works_d_wrap .works_d_box {
  position: relative;
  width: 90%;
  max-height: 80vh;
  background-color: #fff;
  padding: 5vw;
  border-radius: var(--card_radius);
  overflow-y: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
}

.works_d_wrap .works_d_box .works_close {
  position: absolute;
  top: 2vw;
  right: 2vw;
  width: 30px;
  height: 30px;
  cursor: pointer;
}

.works_d_wrap .works_d_box .works_close .close {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 30px;
  height: 2px;
  background-color: var(--gray);
  transform: translate(-50%, -50%) rotate(45deg);
}

.works_d_wrap .works_d_box .works_close .close:last-child {
  transform: translate(-50%, -50%) rotate(-45deg);
}

.works_d_wrap .works_d_box .works_d_title {
  font-size: 1.2rem;
  color: var(--green);
  font-weight: var(--txt_bold);
  line-height: var(--line_h);
}

.works_d_wrap .works_d_box .works_d_pc {
  display: block;
}

.works_d_wrap .works_d_box .works_d_pc .works_d_img {
  position: relative;
  width: 100%;
  height: 32vw;
  margin-top: 0.5rem;
  overflow: hidden;
}

.works_d_wrap .works_d_box .works_d_pc .works_d_img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.works_d_wrap .works_d_box .works_d_pc .works_d_txt .works_d_desc {
  font-size: var(--txt_min_sp);
  line-height: var(--line_h);
  margin-top: 0.5rem;
}

.works_d_wrap .works_d_box .works_d_pc .works_d_txt a.works_button {
  display: block;
  width: 35vw;
  background-color: var(--green);
  font-size: var(--txt_m_sp);
  color: #fff;
  padding: 0.3rem 0;
  text-align: center;
  margin: var(--width_margin_sp) auto 0;
  border-radius: var(--form_radius);
}

@media (min-width: 1024px) {
  #works {
    scroll-margin-top: var(--pagelink_pc);
  }

  .works_wrap {
    margin-top: var(--width_margin_pc);
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: var(--card_gap_pc) 20px;
  }

  .works_wrap .works_box {
    flex: 0 0 calc((100% - (var(--card_gap_pc) * 2)) / 3);
    height: var(--height_work_card_pc);
    margin: 0;
  }

  .work_card a {
    height: var(--height_work_card_pc);
  }

  .work_card .works_img {
    height: 150px;
  }

  .work_card .works_img p {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 100px;
    height: 30px;
    background-color: #fff;
    font-size: var(--txt_m_pc);
    padding-left: 20px;
  }

  .work_card .works_img p::after {
    content: ">";
    position: absolute;
    bottom: 0;
    right: 10px;
  }

  .work_card dl {
    padding: 10px 1rem;
  }

  .work_card dl dt {
    font-size: var(--txt_m_pc);
  }

  .work_card dl dd {
    font-size: var(--txt_min_pc);
    max-height: 50px;
  }

  /* 詳細モーダル */
  .works_d_wrap .works_d_box {
    position: relative;
    width: var(--width_modal_pc);
    padding: var(--padding_modal_tb_pc) var(--padding_modal_lr_pc);
  }

  .works_d_wrap .works_d_box .works_close {
    position: absolute;
    top: var(--padding_modal_tb_pc);
    right: var(--padding_modal_lr_pc);
  }

  .works_d_wrap .works_d_box .works_d_title {
    font-size: 1.3rem;
  }

  .works_d_wrap .works_d_box .works_d_pc {
    display: flex;
    justify-content: space-between;
    margin-top: 1vw;
  }

  .works_d_wrap .works_d_box .works_d_pc .works_d_img {
    width: 300px;
    height: 200px;
    margin-top: 0;
  }

  .works_d_wrap .works_d_box .works_d_pc .works_d_txt{
    width: 300px;
  }

  .works_d_wrap .works_d_box .works_d_pc .works_d_txt .works_d_desc {
    font-size: var(--txt_min_pc);
    margin-top: 0;
  }

  .works_d_wrap .works_d_box .works_d_pc .works_d_txt a.works_button {
    width: 300px;
    font-size: var(--txt_m_pc);
    padding: 0.5rem 0;
    margin: 3vw auto 0;
  }
}
</style>