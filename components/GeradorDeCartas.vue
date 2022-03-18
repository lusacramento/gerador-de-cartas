<template>
  <div id="gerador-de-cartas">
    <h1>Gerador de Cartas</h1>
    <div class="container">
      <div class="row">
        <div v-for="card in deck" :key="card.id" class="col">
          <div class="card">
            <div id="id-card">Id:{{ card.id }}<br /></div>
            <div id="value-card">Value: {{ card.value }}</div>
            <div id="width-card">width: {{ card.width }}</div>
            <div id="future-card">isFutureCard: {{ card.isFutureCard }}</div>
            <div id="future-card">isCurrentCard: {{ card.isCurrentCard }}</div>
            <div id="future-card">isPastCard: {{ card.isPastCard }}</div>
            <div id="fragments-card">
              <div v-for="fragment in card.fragments" :key="fragment.position">
                Posição: {{ fragment.position }} || isHighlight:
                {{ fragment.isHighlight }} || Fragmento:
                <strong>{{ fragment.fragment }}</strong>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GeradorDeCartas',
  props: {
    deck: {
      type: Array,
      default() {
        return []
      },
    },
  },
}
</script>

<style>
.card {
  width: 370px;
  height: 250px;
  border: solid 3px red;
  padding: 5px;
  margin: 5px;
}
</style>
