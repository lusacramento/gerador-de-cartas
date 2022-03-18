<template>
  <div id="app">
    <div>{{ info2 }}</div>
    <div>{{ info3 }}</div>
    <div>{{ info }}</div>

    <!-- <div>{{ data }}}</div> -->

    <GeradorDeCartas :deck="deck" />
  </div>
</template>

<script>
import GeradorDeCartas from '@/components/GeradorDeCartas.vue'
export default {
  name: 'IndexPage',
  components: { GeradorDeCartas },
  async asyncData({ $http }) {
    const deck = await $http.$get('./json/deck.json')
    return {
      deck: deck.deck,
      data: {},
      info: '',
      info2: '',
      info3: '',
    }
  },
  data() {
    return {}
  },
  mounted() {
    this.data.deck = this.generateFragmentsData()
    this.info = this.data
  },
  methods: {
    generateFragmentsData() {
      const [min, max] = [1, 4]

      const digits = []
      // const fragments = {}
      for (let i0 = min; i0 <= max; i0++) {
        for (let i1 = min; i1 <= max; i1++) {
          for (let i2 = min; i2 <= max; i2++) {
            for (let i3 = min; i3 <= max; i3++) {
              if (
                i0 !== i1 &&
                i0 !== i2 &&
                i0 !== i3 &&
                i1 !== i2 &&
                i1 !== i3 &&
                i2 !== i3
              ) {
                const fragmentA = [0, i0, 0, i1]
                const fragmentB = [0, i2, 0, i3]
                digits.push({
                  card: [
                    {
                      id: `${i0}${i1}${i2}${i3}`,

                      fragments: [
                        {
                          fragA: this.injectFragmentsData(fragmentA),

                          fragB: this.injectFragmentsData(fragmentB),
                        },
                      ],
                    },
                  ],
                })
              }
            }
          }
        }
      }
      return digits
    },

    injectFragmentsData(data) {
      const fragments = {}
      fragments.value = `${data[0]}${data[1]}${data[2]}${data[3]}`
      fragments.width = data.length
      fragments.isfutureCard = true
      fragments.isCurrentCard = false
      fragments.isPastCard = false
      fragments.fragment = []
      for (const i in data) {
        fragments.fragment.push({
          position: i,
          isrHighLight: false,
          value: data[i],
        })
      }
      return fragments
    },
  },
  generateFragments(frags) {},

  generateCards() {},
}
</script>
