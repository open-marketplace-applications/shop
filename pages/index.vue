<template>
  <div class="container">
    <div>
      <h1 class="title">{{ shopName }}</h1>
      <h2 class="subtitle">
        {{ shopDescription }}
      </h2>
      <div class="contain">
        <storefront />
      </div>
    </div>
  </div>
</template>

<script>
import Storefront from '@/components/shop/Storefront.vue'
export default {
  components: {
    Storefront
  },
  data() {
    return {}
  },
  computed: {
    shopName() {
      return process.env.shopName
    },
    shopDescription() {
      return process.env.shopDescription
    }
  },
  beforeMount() {
    console.log('shops page created')
    console.log(this.$store.state.products)
    this.connect_pegasus()
  },
  methods: {
    connect_pegasus() {
      console.log('connect_pegasus')
      if (process.client) {
        setTimeout(async function() {
          if (window.iota) {
            console.log('window.iota', window.iota)
            try {
              const isConnected = await window.iota.connect()
              console.log('isConnected', isConnected)
            } catch (err) {
              console.log('err', err)
            }
          }
        }, 3000)
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
</style>
