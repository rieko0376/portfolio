<template>
  <section>
    <div id="vision"></div>
      <h2>Vision<span>今後の展望</span></h2>
      <p class="lead">
        これまでのWebディレクターの経験を活かしながら、フロントエンドのスキルを学習し、Webエンジニアとして実務に対応できる力を身につけたいと考えています。<br /><br />
        将来的にはユーザーにとって使いやすく、クライアントの目標達成に繋がるWebサイトやアプリを開発できるエンジニアを目指しています。
      </p>
  </section>
</template>

<script setup></script>

<style scoped>
#vision {
  scroll-margin-top: var(--pagelink);
}

@media (min-width: 1024px) {
  #vision {
    scroll-margin-top: var(--pagelink_pc);
  }
}
</style>