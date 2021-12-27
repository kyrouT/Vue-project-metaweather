<template>
  <div class="backModal">
      <div class="modal">
          <slot/>
          <button>Close</button>
      </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>

.backModal {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 99;
    background: rgba(0,0,0,0.5);
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
    background: whitesmoke;
    padding: 32px;
    height: 25%;
    display: flex;
    align-items: center;
    justify-content: center;
}


</style>