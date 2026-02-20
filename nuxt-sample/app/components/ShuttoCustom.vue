<!--
  多言語コンポーネント
  shutto翻訳を使用
-->
<script>
import SlideUpDown from "vue-slide-up-down";
export default {
  components: {
    SlideUpDown,
  },
  data() {
    return {
      isOpen: false,
    };
  },
  computed: {
    localButtonClass() {
      return {
        "shutto-custom__button": true,
        "shutto-custom__button--open": this.isOpen,
      };
    },
  },
  mounted() {
    this.$nextTick(() => {
      setTimeout(() => {
        this.insertShuttoTranslation();
      }, 500);
    });
  },
  methods: {
    /**
     * shutto翻訳タグを挿入する
     * すでに存在してる場合は追加しない
     * 注意: tagNameは常に大文字で返るため、'SCRIPT'と大文字で比較する
     * ローカル環境は除外
     */
    insertShuttoTranslation() {
      const targetTag = document.getElementById("shutto-translation");
      if (targetTag && targetTag.tagName === "SCRIPT") {
        return;
      }

      // なければheadタグの末尾に追加
      const shuttoTag = document.createElement("script");
      shuttoTag.src =
        "https://sandbox-d.ea-shutto-translation.net/trans.js?id=80215";
      shuttoTag.id = "shutto-translation";
      document.head.appendChild(shuttoTag);
    },
    /**
     * 多言語のプルダウンを開閉する
     */
    toggleShuttoTranslation() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>

<template lang="pug">
test
#shutto-custom.shutto-custom
  button(@click='toggleShuttoTranslation' :class='localButtonClass')
    i.shutto-custom__button-icon.fa-solid.fa-globe
    span.shutto-custom__button-text LANG
    span.shutto-custom__button-arrow
      i.fa-solid.fa-chevron-down
  .shutto-custom__content
    .shutto-custom__wrapper(v-show='isOpen')
      .shutto-custom__inner(data-stt-langbar)
        .shutto-custom__item
          button(data-stt-changelang='ja' data-stt-ignore @click='toggleShuttoTranslation') JP
        .shutto-custom__item
          button(data-stt-changelang='en' data-stt-ignore @click='toggleShuttoTranslation') EN
        .shutto-custom__item
          button(data-stt-changelang='id' data-stt-ignore @click='toggleShuttoTranslation') ID
        .shutto-custom__item
          button(data-stt-changelang='ko' data-stt-ignore @click='toggleShuttoTranslation') KO
        .shutto-custom__item
          button(data-stt-changelang='zh-CN' data-stt-ignore @click='toggleShuttoTranslation') CN
        .shutto-custom__item
          button(data-stt-changelang='zh-TW' data-stt-ignore @click='toggleShuttoTranslation') TW
</template>
