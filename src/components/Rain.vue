<template>
  <div class="rain"></div>
</template>

<script>
export default {
  name: "Rain",
};
let nbDrop = 858;

function randRange(minNum, maxNum) {
  return Math.floor(Math.random() * (maxNum - minNum + 1)) + minNum;
}

function createRain() {
  for (let i = 0; i < nbDrop; i++) {
    let dropLeft = randRange(0, 1600);
    let dropTop = randRange(-1000, 1400);

    document
      .querySelector(".rain")
      .append(`<div class="drop" id="drop'${i}'"></div>`);
    document.querySelector("#drop" + i).css("left", dropLeft);
    document.querySelector("#drop" + i).css("top", dropTop);
  }
}

createRain();
</script>

<style>
html {
  height: 100%;
}
body {
  background: #0d343a;
  background: -webkit-gradient(
    linear,
    0% 0%,
    0% 100%,
    from(rgba(13, 52, 58, 1)),
    to(#000000)
  );
  background: -moz-linear-gradient(
    top,
    rgba(13, 52, 58, 1) 0%,
    rgba(0, 0, 0, 1) 100%
  );

  overflow: hidden;
}

.drop {
  background: -webkit-gradient(
    linear,
    0% 0%,
    0% 100%,
    from(rgba(13, 52, 58, 1)),
    to(rgba(255, 255, 255, 0.6))
  );
  background: -moz-linear-gradient(
    top,
    rgba(13, 52, 58, 1) 0%,
    rgba(255, 255, 255, 0.6) 100%
  );
  width: 1px;
  height: 89px;
  position: absolute;
  bottom: 200px;
  animation: fall 0.63s linear infinite;
}

@keyframes fall {
  to {
    margin-top: 900px;
  }
}
</style>
