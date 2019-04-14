<template>
  <div class="nav">
    <div class="nav__box">
      <div class="logo">
        <img src="@/assets/logo.svg" alt="">
        <h2>Vicinia</h2>
      </div>
      <div class="tabs">
        <ul>
          <li><div class="dot active"></div></li>
          <li><div class="dot"></div></li>
          <li><div class="dot"></div></li>
          <li><div class="dot"></div></li>
        </ul>
      </div>
      <div class="copyright">2019</div>
    </div>
  </div>
</template>

<style lang="scss">

.nav {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  z-index: 200;

  &__box {
    position: relative;
    width: 5vw;
    height: 100%;
    background: white;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
  }
}

.logo {
  width: 100%;
  text-align: center;

  & h2 {
    width: inherit;
    font-size: 14px;
  }
}

.tabs ul {
  list-style-type: none;
  padding: 0;
}

.tabs li:not(:last-child) {
  margin-bottom: 1rem;
}

.dot {
  border-radius: 50rem;
  height: .5rem;
  width: .5rem;
  border: 1.5px solid #1d2b3b;
  transition: all .2s ease-in-out;
}

.dot.active, .dot:hover {
  background: #1d2b3b;
  transform: scale(1.2);
  cursor: pointer;
}

</style>
