<script>

export default {
  data() {
    return {
      isClicked: false,
      isSmooth: true,
    }
  },
  methods: {
    dragging(value) {
      if (!this.isClicked) return;
      //stampa un "dragging" ogni pixel percorso su asse x (numero messaggi sulla destra della console)"
      console.log('dragging...')
      // al movimento del mouse scrolla a sx quanto il valore di "mosue-move" sull asse x
      //movementX è una proprieta onlyread di "mousemove"
      document.getElementById('carousel').scrollLeft -= value.movementX
    },
    // richiamo questa funzione con "@mouseup vedi template e fondopagina"
    mouseRelease() {
      this.isClicked = false;
      this.isSmooth = true;
    },
    Right() {
      document.getElementById('carousel').scrollLeft += 215
      console.log("scrollDX")
    },

    Left() {
    document.getElementById('carousel').scrollLeft -= 215
      console.log("scrollSX")
    },

  },
  created() {

  },
  mounted() {

  }
}
</script>


<template>

  <div class="container">
    <button @click="Left()">next</button>
    <!-- la documentazione su questi "@events" è in fondo alla pagina -->
    <div @mousemove="dragging"
         @mousedown="isClicked = !isClicked, isSmooth = !isSmooth" 
         @mouseup="mouseRelease()"
      id="carousel" :class="{ smooth: isSmooth }">
      <div id="element-container"><!--width 1750px(va in overflow)-->
        <div class="elemento">foto 1</div>
        <div class="elemento">foto 2</div>
        <div class="elemento">foto 3</div>
        <div class="elemento">foto 4</div>
        <div class="elemento">foto 5</div>
        <div class="elemento">foto 6</div>
        <div class="elemento">foto 7</div>
        <div class="elemento">foto 8</div>
      </div>
    </div>
    <button @click="Right()">next</button>
  </div>

</template>



<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 99vh;
}

#carousel {
  width: 1100px;
  height: 330px;
  border: 2px dashed green;
  display: flex;
  align-items: center;
  overflow-x: hidden;
}

/* classe per scrollare SMOOTH */
/* lo metto come classe separata perche non va daccordo col "drag-scroll" */
.smooth {
  scroll-behavior: smooth;
}

#element-container {
  display: flex;
  width: 1750px;
}

button {
  border: 2px dashed orange;
  background: rgba(255, 166, 0, 0.288);
  background: none;
  margin: 2rem;
  width: 80px;
  height: 80px;
  cursor: pointer;
}

.elemento {
  border: 2px dashed orange;
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 1rem;
  background: rgba(255, 166, 0, 0.288);
}
</style>



<!-- nel codice viene usato "@mousdown" e non "@click" lascio la documentazione di MDN -->


<!-- "movementX" sempre su mdn (anche qua le prime righe spiegano gia abbastanza) -->
<!-- https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/movementX -->

<!-- ._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.- -->

<!-- "mousedown" spieghato velocemente su MDN (le prime 2 righre dicono gia tutto) -->
<!-- https://developer.mozilla.org/en-US/docs/Web/API/Element/mousedown_event -->

<!-- ._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.- -->

<!-- per "mouseup" sempre su MDN ( <3 MDN ) -->
<!-- https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseup_event -->

<!-- ._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.-._.- -->

<!-- sono arrivato fin qui.
mancherebbe da far in modo che se si preme "...[ next-> ]" A FINE lista, si torna all inizio
e se si preme "[ <-prev ] ..." a INIZIO lista si va alla fine -->