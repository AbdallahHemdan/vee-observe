<template>
  <div>
    <slot />
  </div>
</template>

<script>
export default {
  name: 'VeeObserve',
  data () {
    return {
      observer: null,
    }
  },

  props: {
    root: {
      type: HTMLElement,
      default: null,
    },
    rootMargin: {
      type: String,
      default: '0px',
    },
    threshold: {
      type: Number,
      default: 0,
    },
    once: {
      type: Boolean,
      default: false,
    },
  },

  methods: {
    unobserve () {
      if (this.observer) {
        this.observer.unobserve(this.$el);
      }
    },
  },

  mounted () {
    if ('IntersectionObserver' in window) {
      const options = {
        root: this.root,
        rootMargin: this.rootMargin,
        threshold: this.threshold,
      }

      this.observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting && this.once) {
            this.$emit('on-change', entry);
            this.unobserve();
          } else {
            this.$emit('on-change', entry, this.unobserve);
          }
        })
      }, options);

      this.observer.observe(this.$el);
    }
  },

  beforeDestroy () {
    if (this.observer) {
      this.unobserve();
      this.observer = null;
    }
  },
}
</script>