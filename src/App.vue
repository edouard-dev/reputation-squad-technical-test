<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style>
body {
  margin: 0px;
}
p, h1, h2, h3 {
  font-family: Inter;
  font-weight: 500;
}


input[type=range] {
    height: 22px;
    -webkit-appearance: none;
    margin: 10px 0;
    width: 100%;
  }

  input[type=range]:focus {
    outline: none;
  }

  input[type=range]::-webkit-slider-runnable-track {
    width: 100%;
    height: 2px;
    cursor: pointer;
    box-shadow: 0px 0px 0px #000000;
    background: #DBE5FF;
    border-radius: 9px;
    border: 0px solid #010101;
  }

  input[type=range]::-webkit-slider-thumb {
    box-shadow: 0px 0px 0px #000031;
    border: 0px solid #00001E;
    height: 16px;
    width: 16px;
    border-radius: 50px;
    background: #5887FF;
    cursor: pointer;
    -webkit-appearance: none;
    margin-top: -7px;
  }

  input[type=range]:focus::-webkit-slider-runnable-track {
    background: #DBE5FF;
  }

  input[type=range]::-moz-range-track {
    width: 100%;
    height: 2px;
    cursor: pointer;
    box-shadow: 0px 0px 0px #000000;
    background: #DBE5FF;
    border-radius: 9px;
    border: 0px solid #010101;
  }

  input[type=range]::-moz-range-thumb {
    box-shadow: 0px 0px 0px #000031;
    border: 0px solid #00001E;
    height: 16px;
    width: 16px;
    border-radius: 50px;
    background: #5887FF;
    cursor: pointer;
  }

  input[type=range]::-ms-track {
    width: 100%;
    height: 2px;
    cursor: pointer;
    background: transparent;
    border-color: transparent;
    color: transparent;
  }

  input[type=range]::-ms-fill-lower {
    background: #DBE5FF;
    border: 0px solid #010101;
    border-radius: 18px;
    box-shadow: 0px 0px 0px #000000;
  }

  input[type=range]::-ms-fill-upper {
    background: #DBE5FF;
    border: 0px solid #010101;
    border-radius: 18px;
    box-shadow: 0px 0px 0px #000000;
  }

  input[type=range]::-ms-thumb {
    margin-top: 1px;
    box-shadow: 0px 0px 0px #000031;
    border: 0px solid #00001E;
    height: 16px;
    width: 16px;
    border-radius: 50px;
    background: #5887FF;
    cursor: pointer;
  }

  input[type=range]:focus::-ms-fill-lower {
    background: #DBE5FF;
  }

  input[type=range]:focus::-ms-fill-upper {
    background: #DBE5FF;
  }

</style>
