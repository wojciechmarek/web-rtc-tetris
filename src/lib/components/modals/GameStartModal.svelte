<script lang="ts">
  import wasdKeysImage from "@images/wasd_keys.webp";
  import { createEventDispatcher } from "svelte";
  import QrCode from "svelte-qrcode";
  import Frame from "../common/Frame.svelte";
  import Button from "../common/Button.svelte";

  const dispatch = createEventDispatcher();

  export let qrCodeValue: string = "";
  export let isRemoteController: boolean = false;
  export let isQrCodeReadyToScan: boolean = false;

  let controllerStatus = "";

  $: {
    if (isRemoteController) {
      controllerStatus =
        "Remote controller connected! Press start to begin the game";
    } else {
      controllerStatus = "";
    }
  }

  const onRefreshCodeClick = () => {
    dispatch("refreshQrCodeClick");
  };

  const onSelectWasdKeyClick = () => {
    dispatch("selectWasdKeysClick");
  };
</script>

<div class="game-start__container">
  <div class="game-start__content">
    <h1 class="game-start__header">TETRIS</h1>
    <div class="game-start__controllers-container">
      <div class="game-start__controller">
        <Frame title="Remote controller">
          <div class="game-start__controller-image">
            {#if isQrCodeReadyToScan}
              <QrCode value={qrCodeValue} size={130} />
            {:else}
              <p class="game-start__controller-message">
                Wait... Setting up the connection.
              </p>
            {/if}
          </div>
        </Frame>
        <Button text="Refresh" on:click={onRefreshCodeClick} />
      </div>
      <div class="game-start__controller">
        <Frame title="Keyboard WASD keys">
          <div class="game-start__controller-image">
            <img
              src={wasdKeysImage}
              alt="keyboard buttons"
              class="game-start__controller-image_img"
            />
          </div>
        </Frame>
        <Button text="Select" on:click={onSelectWasdKeyClick} />
      </div>
    </div>
  </div>
  <p class="game-start__controller-connected">
    {controllerStatus}
  </p>
</div>

<style>
  .game-start__container {
    display: grid;
    justify-content: center;
    align-content: center;
    height: 100%;
  }

  .game-start__content {
    padding: 2em;
    background-color: #284fe6;
    border: 0.25em solid #1e287d;
  }

  .game-start__header {
    text-align: center;
    text-transform: uppercase;
    font-size: 3rem;
    margin: 0;
    padding: 0;
    text-shadow: #000000 0px 5px;
  }

  .game-start__controllers-container {
    display: flex;
    gap: 3em;
    margin-top: 2em;
  }

  .game-start__controller {
    display: flex;
    flex-direction: column;
    gap: 1em;
    width: 22.5em;
  }

  .game-start__controller-image {
    width: 160px;
    height: 160px;
    border-radius: 5px;
    background-color: white;
    padding: 0.125em;
  }

  .game-start__controller-message {
    color: black;
    padding: 1em;
  }

  .game-start__controller-image_img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    padding: 8px;
  }

  .game-start__controller-connected {
    height: 2em;
    text-align: center;
  }
</style>
