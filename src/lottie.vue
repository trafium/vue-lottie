<template>
    <div :style="style" ref="lavContainer"></div>
</template>

<script>
  import lottie from 'lottie-web';

  export default {
    props: {
      options: {
        type: Object,
        required: true
      },
      height: Number,
      width: Number,
    },

    data () {
      return {
        style: {
          width: this.width ? `${this.width}px` : '100%',
          height: this.height ? `${this.height}px` : '100%',
          overflow: 'hidden',
          margin: '0 auto'
        }
      }
    },

    mounted () {
      const { loop, autoplay, animationData, rendererSettings, name } = this.options;

      this.anim = lottie.loadAnimation({
          container: this.$refs.lavContainer,
          renderer: 'svg',
          loop: loop !== false,
          autoplay: autoplay !== false,
          animationData: animationData,
          rendererSettings: rendererSettings,
          name: name
        }
      );

      this.$emit('animCreated', this.anim);

      this.anim.addEventListener('complete', () => this.$emit('complete', this.anim));
      this.anim.addEventListener('loopComplete', () => this.$emit('loopComplete', this.anim));
      this.anim.addEventListener('enterFrame', () => this.$emit('enterFrame', this.anim));
    }
  }
</script>
