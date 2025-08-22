<template>
  <section>
    <div id="about"></div>
    <h2>About<span>自己紹介</span></h2>

    <p class="lead">
      ポートフォリオを閲覧頂きありがとうございます。みやもとと申します。<br /><br />
      本サイトでは私の紹介や、プログラミングの勉強のために制作したサイトやアプリの紹介を行います。<br /><br />
      前職では<span class="bold">総合広告代理店にて7年間、Webディレクターとして勤務</span>し、自治体、観光協会、JA、民間企業の<span
        class="bold">公式サイトやイベントLP制作・更新業務を担当</span>しました。<br /><br />またWeb制作の他に、Web広告の提案・出稿、冊子制作、イベント運営など幅広い業務に携わってきました。<br /><br />
      ディレクションをする中でプログラミングに興味を持ち、入社3年目からHTML・CSSを学び、マークアップを担当するようになりました。<br /><br />ディレクション業務と並行してマークアップを経験する中で、Webエンジニアになりたいという思いが強くなり、2025年6月に退職し、転職活動を開始しました。<br /><br />
      現在はHTML・CSSを復習しながら、JavaScriptやVue.jsを勉強中です。
    </p>

    <h3>Point</h3>
    <div class="skill_wrap">
      <div class="skill_box">
        <dl>
          <dt><span class="bold">目標達成を意識した制作姿勢</span></dt>
          <dd>
            これまで総合広告代理店のWebディレクターとして、Web制作をクライアントの目標達成の手段の一つとして考え、進行してきました。今後も広い視点でクライアントの目標達成を意識し、開発者として目的に合った提案や改善に努めていきたいと考えています。
          </dd>
        </dl>
      </div>
      <div class="skill_box">
        <dl>
          <dt><span class="bold">顧客とのコミュニケーション経験</span></dt>
          <dd>
            前職では営業に同行し、顧客への提案や要望のヒアリングをしていました。その経験を活かし、Webエンジニアとしても相手の意図を丁寧に理解し、制作チームや顧客とのコミュニケーションを大切にしながら開発に取り組みたいと考えています。
          </dd>
        </dl>
      </div>
      <div class="skill_box">
        <dl>
          <dt><span class="bold">設計～運用を意識したプログラミング</span></dt>
          <dd>
            前職で培った企画・設計・制作進行・運用までを意識する視点を活かしつつ、現在は実装スキルを勉強中です。今後、使いやすさや運用性を考慮した開発ができるよう成長していきたいです。
          </dd>
        </dl>
      </div>
      <div class="skill_box">
        <dl>
          <dt><span class="bold">学習意欲と興味のある分野への取り組み</span></dt>
          <dd>
            興味を持った分野には積極的に取り組む姿勢を大切にしています。現在はフロントエンド開発を中心に学習していますが、今後も興味を持った分野を深めながら、実務に生かせるスキルを身につけていきたいと思います。
          </dd>
        </dl>
      </div>
    </div>
  </section>
</template>

<script setup></script>

<style scoped>
/* カスタム変数 */
.skill_wrap {
  --box_p_jyoge: 4vw;
  --box_p_jyoge_pc: 2vw;
}

#about {
  scroll-margin-top: var(--pagelink);
}

.skill_wrap {
  display: block;
}

.skill_wrap .skill_box {
  position: relative;
  width: 100%;
  padding: var(--box_p_jyoge) 1rem;
}

.skill_wrap .skill_box::after {
  content: "";
  display: block;
  width: 100%;
  height: 1px;
  background-color: var(--gray);
  margin: var(--box_p_jyoge) auto 0;
}

.skill_wrap .skill_box dl dt {
  font-size: var(--txt_m_sp);
  font-weight: var(--txt_bold);
  color: var(--green);
  line-height: var(--line_h);
}

.skill_wrap .skill_box dl dd {
  font-size: 0.9rem;
  padding-top: 0.3rem;
}

/* PC版　*/
@media (min-width: 1024px) {
  #about {
    scroll-margin-top: var(--pagelink_pc);
  }

  .skill_wrap {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin: var(--width_margin_pc) 0 0;
  }

  .skill_wrap .skill_box {
    position: relative;
    width: 50%;
    padding-top: var(--box_p_jyoge_pc);
    padding-right: 0.5rem;
    padding-bottom: var(--box_p_jyoge_pc);
    padding-left: 0.5rem;
  }

  .skill_wrap .skill_box::before {
    content: "";
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    right: 0;
    display: block;
    width: 1px;
    height: 80%;
    background-color: var(--gray);
  }

  .skill_wrap .skill_box::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0.5rem;
    display: block;
    width: 95%;
    height: 1px;
    background-color: var(--gray);
  }

  .skill_wrap .skill_box:nth-child(2n)::before,
  .skill_wrap .skill_box:nth-last-child(2)::after,
  .skill_wrap .skill_box:last-child::after {
    opacity: 0;
  }

  .skill_wrap .skill_box:nth-child(2n):after {
    left: auto;
    right: 0.5rem;
  }

  .skill_wrap .skill_box:nth-child(2n) {
    padding-top: var(--box_p_jyoge_pc);
    padding-right: 0.5rem;
    padding-bottom: var(--box_p_jyoge_pc);
    padding-left: 1.5rem;
  }

  .skill_wrap .skill_box dl dt {
    font-size: var(--txt_m_pc);
  }

  .skill_wrap .skill_box dl dd {
    font-size: var(--txt_min_pc);
    padding-top: 0.2rem;
  }
}
</style>