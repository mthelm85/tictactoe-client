<template lang="html">
  <div class="container">
    <div class="row d-flex justify-content-center">
      <div class="col" style="max-width: 300px;">
        <div class="row mt-3">
          <div class="col-4 square sq0 d-flex justify-content-center align-items-center display-4">
            X
          </div>
          <div class="col-4 square sq1 d-flex justify-content-center align-items-center display-4">
            O
          </div>
          <div class="col-4 square sq2 d-flex justify-content-center align-items-center display-4">
            X
          </div>
        </div>
        <div class="row">
          <div class="col-4 square sq3 d-flex justify-content-center align-items-center display-4">
          O
          </div>
          <div class="col-4 square sq4 d-flex justify-content-center align-items-center display-4">
            X
          </div>
          <div class="col-4 square sq5 d-flex justify-content-center align-items-center display-4">
            O
          </div>
        </div>
        <div class="row">
          <div class="col-4 square sq6 d-flex justify-content-center align-items-center display-4">
            X
          </div>
          <div class="col-4 square sq7 d-flex justify-content-center align-items-center display-4">
            O
          </div>
          <div class="col-4 square sq8 d-flex justify-content-center align-items-center display-4">
            X
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="css">
.square {
  max-width: 100px;
  height: 100px;
}
.square:hover {
  background-color: gray;
  cursor: pointer;
}
.sq0, .sq1, .sq3, .sq4 {
  border-right: solid black;
  border-bottom: solid black;
}
.sq2, .sq5 {
  border-bottom: solid black;
}
.sq6, .sq7 {
  border-right: solid black;
}
</style>
