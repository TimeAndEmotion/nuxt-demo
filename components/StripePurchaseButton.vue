<template>
  <span>
    <stripe-checkout
      v-if="pk"
      ref="checkoutRef"
      class="inline-block"
      mode="payment"
      :pk="pk"
      :line-items="[{ price: priceId, quantity: 1 }]"
      :success-url="successURL"
      :cancel-url="cancelURL"
      @loading="$emit('loading')" />
    <span @click="enroll">
      <slot />
    </span>
  </span>
</template>
<script>
export default {
  props: {
    courseId: {
      type: String,
      required: true,
    },
    priceId: {
      type: String,
      default: null,
    },
    text: {
      type: String,
      default: 'Enroll now',
    },
  },
  data: () => {
    return {
      pk: process.env.STRIPE_PUBLISHABLE_KEY,
      loading: false,
    }
  },
  computed: {
    successURL() {
      return process.client
        ? `${window.location.origin}/courses/${this.courseId}?sale=true`
        : null
    },
    cancelURL() {
      return process.client
        ? `${window.location.origin}/courses/${this.courseId}?error=true`
        : null
    }
  },
  methods: {
    enroll() {
      if (this.pk) {
        this.$refs.checkoutRef.redirectToCheckout()
      } else {
        console.warn('Missing STRIPE_PUBLISHABLE_KEY env variable.')
      }
    },
  },
}
</script>
