<template>
  <div class="number-scroll">
    <div
      v-for="(char, charIndex) in chars"
      :key="`num-${charIndex}`"
      class="number-scroll__item"
      :style="{
        width: size - 4 + 'px',
        height: size + 2 + 'px',
        'font-size': size + 'px',
      }"
    >
      <div
        class="number-scroll__item-anim"
        :style="{
          top: char.top * -1 + 'px',
          transition: `top ${char.countNumbers * speed}s ease-out`,
        }"
      >
        <template v-if="char.isNumber">
          <span v-for="num in char.countNumbers" :key="`numItem${num}`">{{
            num - 1
          }}</span>
        </template>

        <span>{{ char.value }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    number: {
      type: String,
      required: true,
    },
    size: {
      type: Number,
      default: 24,
    },
    speed: {
      type: Number,
      default: 0.2,
    },
    delay: {
      type: Number,
      default: 200,
    },
  },
  data() {
    return {
      chars: [],
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    async init() {
      for (const char of this.number) {
        const isNumber = this.checkNumber(char);
        const value = isNumber ? Number(char) : char;
        let top;

        if (isNumber) {
          top = char === "0" ? this.size * 1.2 * 10 : 0;
        } else {
          top = this.size * 1.2;
        }

        this.chars.push({
          value,
          isNumber,
          top,
          countNumbers: this.getCountNumbers({ value, isNumber }),
        });
      }

      await new Promise((resolve) => setTimeout(resolve, this.delay));

      this.chars.forEach((char) => {
        char.top = char.isNumber ? this.size * 1.2 * char.value : 0;
      });
    },

    checkNumber(number) {
      return /^\d$/.test(number);
    },

    getCountNumbers(char) {
      return char.isNumber ? char.value || 10 : 1;
    },
  },
};
</script>

<style lang="scss" scoped>
.number-scroll {
  display: flex;
  justify-content: center;
  margin-bottom: rem(10);
  &__item {
    position: relative;
    overflow: hidden;
    &-anim {
      left: 0;
      right: 0;
      position: absolute;
      display: flex;
      flex-direction: column;
      align-items: center;
      span {
        line-height: 1.2;
      }
    }
  }
}
</style>
