<template>
  <section>
    <div id="contact"></div>
      <h2>Contact<span>お問い合わせ</span></h2>
      <p class="lead">もし私に興味を持っていただけましたら、こちらのフォームからご連絡いただけますと幸いです。</p>
      <p class="lead_note">*は必須項目です。<br />※送信システムは未実装です。送信後はコンソールログに送信内容が表示されます。</p>

      <form @submit.prevent="openModal">
        <div class="form_item">
          <label for="name">お名前</label>
          <input v-model="form.name" type="text" id="name" placeholder="例：山田 太郎">
          <p class="form_note">例：山田　太郎</p>
        </div>
        <div class="form_item">
          <label for="email">メールアドレス</label>
          <input v-model="form.email" type="email" id="email" placeholder="例：example@example.com">
          <p class="form_note">例：example@example.com</p>
        </div>
        <div class="form_item">
          <label for="message">お問い合わせ内容</label>
          <textarea v-model="form.message" ref="textareaRef" @input="autoResize" id="message" row="5"></textarea>
        </div>
        <button type="submit">確認画面</button>
      </form>

      <div v-if="isModalOpen" class="form_check" @click.self="closeModal">
        <div class="form_check_item">

          <template v-if="formStep === 'confirm'">
            <p class="form_check_title">送信内容の確認</p>
            <p class="lead">内容をご確認の上、送信ボタンを押してください。</p>
            <p class="lead_note">※送信システムは未実装です。送信後はコンソールログに送信内容が表示されます。</p>
            <div class="form_check_detail">
              <p><span>お名前：</span>{{ confirmData.name }}</p>
              <p><span>メールアドレス：</span>{{ confirmData.email }}</p>
              <p><span>お問い合わせ内容：</span>{{ confirmData.message }}</p>
            </div>
            <button @click="sendForm">送信</button>
            <button @click="closeModal">キャンセル</button>
          </template>

          <template v-else-if="formStep === 'done'">
            <p class="form_check_title">送信完了</p>
            <p class="lead">お問い合わせありがとうございました。</p>
            <p class="lead_note">※送信システムは未実装です。送信後はコンソールログに送信内容が表示されます。</p>
            <button @click="closeModal">閉じる</button>
          </template>

        </div>
      </div>
  </section>
</template>

<script setup>
import { nextTick, reactive, ref } from 'vue'
//　入力フォームの値
const form = reactive({
  name: '',
  email: '',
  message: '',
})
//確認モーダル表示用
const confirmData = reactive({
  name: '',
  email: '',
  message: '',
})
//モーダル表示
const isModalOpen = ref(false)
const formStep = ref('confirm')

const openModal = () => {
  formStep.value='confirm'//確認画面表示
  confirmData.name = form.name
  confirmData.email = form.email
  confirmData.message = form.message
  isModalOpen.value = true
  document.body.style.overflow = 'hidden'
  nextTick(autoResize) //開いた直後に高さ調整
}
const closeModal = () => {
  isModalOpen.value = false
  document.body.style.overflow = ''
}
// 送信処理
const sendForm = () => {
  console.log(
    `お問い合わせ受付内容:`,
    `お名前:${confirmData.name}`,
    `メールアドレス:${confirmData.email}`,
    `お問い合わせ内容:${confirmData.message}`,)
    formStep.value='done' //完了画面切り替え

  form.name = ''
  form.email = ''
  form.message = ''
}
// textarea　オートリサイズ処理
const textareaRef = ref(null) //DOM要素の取得を参照するref
const autoResize = () => {
  nextTick(() => { //DOM更新後に実行
    const el = textareaRef.value
    if (!el) return
    el.style.height = 'auto'
    el.style.height = el.scrollHeight + 'px'
  })
}
</script>

<style scoped>
#contact {
  scroll-margin-top: var(--pagelink);
}

form {
  margin-top: var(--width_margin_sp);
}

.form_item {
  margin-top: var(--width_margin_sp);
}

.form_item:first-child {
  margin-top: 0;
}

.form_item label {
  display: block;
  font-size: var(--txt_m_sp);
  font-weight: var(--txt_bold);
}

.form_item label::after {
  content: "*";
  font-size: var(--txt_min_sp);
  color: var(--red);
  margin-left: 0.5rem;
}

.form_item input {
  width: 100%;
  background-color: #fff;
  border: 1px solid var(--lightgray);
  border-radius: var(--form_radius);
  padding: var(--form_padding);
  margin-top: var(--form-margin_top);
}

.form_item textarea {
  width: 100%;
  min-height: 20vw;
  background-color: #fff;
  border: 1px solid var(--lightgray);
  border-radius: var(--form_radius);
  padding: var(--form_padding);
  margin-top: var(--form-margin_top);
  resize: none;
}

.form_item input:focus,
.form_item textarea:focus {
  outline: none;
  border-color: var(--green);
}

.form_item p.form_note {
  font-size: var(--txt_min_sp);
  padding: 1vw 0 0 0.5rem;
}

form button {
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

.form_check {
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

.form_check .form_check_item {
  width: 90%;
  max-height: 80vh;
  background-color: #fff;
  padding: 5vw;
  border-radius: var(--form_radius);
  overflow-y: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
}

.form_check .form_check_item .form_check_title {
  font-size: 1.2rem;
  color: var(--green);
  font-weight: var(--txt_bold);
  text-align: center;
}

.form_check .form_check_item .form_check_detail {
  margin-top: 5vw;
}

.form_check .form_check_item .form_check_detail p {
  font-size: var(--txt_m_sp);
  margin-top: 3vw;
}

.form_check .form_check_item .form_check_detail p span {
  display: block;
  font-size: var(--txt_m_sp);
  color: var(--green);
  font-weight: var(--txt_bold);
}

.form_check .form_check_item button {
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

.form_check .form_check_item button:last-child {
  background-color: var(--gray);
  width: 30vw;
}

@media (min-width: 1024px) {
  #contact {
    scroll-margin-top: var(--pagelink_pc);
  }

  form {
    margin-top: var(--width_margin_pc);
  }

  .form_item {
    margin-top: var(--width_margin_pc);
  }

  .form_item label {
    font-size: var(--txt_m_pc);
  }

  .form_item label::after {
    content: "*";
    font-size: var(--txt_min_pc);
  }

  .form_item textarea {
    min-height: 100px;
  }

  .form_item p.form_note {
    font-size: var(--txt_min_pc);
  }

  form button {
    width: 300px;
    font-size: var(--txt_m_pc);
    padding: 0.5rem 0;
    margin: var(--width_margin_pc) auto 0;
  }

  .form_check .form_check_item {
    width: var(--width_modal_pc);
    padding: var(--padding_modal_tb_pc) var(--padding_modal_lr_pc);
  }

  .form_check .form_check_item .form_check_title {
    font-size: 2rem;
  }

  .form_check .form_check_item .form_check_detail {
    margin-top: 20px;
  }

  .form_check .form_check_item .form_check_detail p {
    font-size: var(--txt_m_pc);
    margin-top: 10px;
  }

  .form_check .form_check_item .form_check_detail p span {
    font-size: var(--txt_m_pc);
  }

  .form_check .form_check_item button {
    width: 300px;
    font-size: var(--txt_m_pc);
    padding: 0.5rem 0;
    margin: var(--width_margin_pc) auto 0;
  }

  .form_check .form_check_item button:last-child {
    width: 200px;
    margin: 30px auto 0;
  }
}
</style>