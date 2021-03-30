<template>
  <div class="landing-page">
    <section class="landing-hero pt-5">
      <div class="header__bg"></div>
      <div class="container mx-auto relative">
        <Navbar />
        <Nuxt />
      </div>
    </section>
    <div class="cta-clip -mt-20"></div>
    <CallToAction />
    <Footer />
  </div>
</template>

<script>
import Navbar from '~/components/Navbar'
import CallToAction from '~/components/CallToAction'
import Footer from '~/components/Footer'

export default {
  components: {
    Navbar,
    CallToAction,
    Footer,
  },
}
</script>
