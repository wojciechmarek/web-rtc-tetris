<script lang="ts">
  import controllerImage from "@images/nintendo.webp";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  const handleKeyDownPress = (id: string) => {
    navigator.vibrate(50);
    dispatch("buttonPress", id);
  };
</script>

<div class="nintendo__container">
  <svg
    class="nintendo__mask"
    width="1235px"
    height="556px"
    viewBox="0 0 1235 556"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    version="1.1"
  >
    <g id="pad">
      <path
        id="container"
        d="M0 556 L1235 556 1235 0 0 0 Z"
        fill="transparent"
        stroke="none"
      />
      <g id="buttons">
        <path
          on:click={() => handleKeyDownPress("up")}
          role="button"
          id="up"
          d="M234.852 231.079 L306.705 231.079 306.705 159.227 234.852 159.227 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("right")}
          role="button"
          id="right"
          d="M306.705 303.929 L378.557 303.929 378.557 232.077 306.705 232.077 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("down")}
          role="button"
          id="down"
          d="M234.852 375.782 L306.705 375.782 306.705 303.929 234.852 303.929 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("left")}
          role="button"
          id="left"
          d="M163 302.931 L234.852 302.931 234.852 231.079 163 231.079 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("select")}
          role="button"
          id="select"
          d="M462.385 348.837 L564.175 348.837 564.175 267.005 462.385 267.005 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("start")}
          role="button"
          id="start"
          d="M594.114 348.837 L695.905 348.837 695.905 267.005 594.114 267.005 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("b")}
          role="button"
          id="b"
          d="M1026.226 357.818 C1026.226 330.261 1003.886 307.921 976.328 307.921 948.771 307.921 926.431 330.261 926.431 357.818 926.431 385.376 948.771 407.716 976.328 407.716 1003.886 407.716 1026.226 385.376 1026.226 357.818 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("a")}
          role="button"
          id="a"
          d="M1136 267.005 C1136 239.448 1113.66 217.108 1086.103 217.108 1058.545 217.108 1036.205 239.448 1036.205 267.005 1036.205 294.563 1058.545 316.903 1086.103 316.903 1113.66 316.903 1136 294.563 1136 267.005 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("x")}
          role="button"
          id="x"
          d="M1017.244 181.182 C1017.244 153.624 994.904 131.284 967.347 131.284 939.789 131.284 917.449 153.624 917.449 181.182 917.449 208.739 939.789 231.079 967.347 231.079 994.904 231.079 1017.244 208.739 1017.244 181.182 Z"
          fill="transparent"
          stroke="none"
        />
        <path
          on:click={() => handleKeyDownPress("y")}
          role="button"
          id="y"
          d="M912.459 268.003 C912.459 240.445 890.12 218.106 862.562 218.106 835.004 218.106 812.665 240.445 812.665 268.003 812.665 295.561 835.004 317.901 862.562 317.901 890.12 317.901 912.459 295.561 912.459 268.003 Z"
          fill="transparent"
          stroke="none"
        />
      </g>
    </g>
  </svg>
  <img src={controllerImage} alt="controller" class="nintendo__img" />
</div>

<style>
  .nintendo__container {
    position: relative;
    width: 100%;
    height: 100vh;
    background-color: white;
  }

  .nintendo__img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  .nintendo__mask {
    position: absolute !important;
    width: 100%;
    height: 100%;
  }
</style>
