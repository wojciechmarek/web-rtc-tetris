<script lang="ts">
  import { onMount } from "svelte";
  import { Nintendo, Status, Warning } from "@components/controller";
  import { ApiUtils, WebRTCUtils } from "@utils/index";

  export let id: string;

  //#region Utilities
  const {
    initWebRTCPeerBasedOnOfferAndIceCandidates,
    getIceCandidates,
    calculateRemoteIpAddress,
    sendKeyIdThoughtChannel
  } = WebRTCUtils();
  const {
    getGameConnectionOfferFromTheServer,
    postControllerConnectionAnswerToTheServer
  } = ApiUtils();
  //#endregion

  //#region Private variables
  let remoteIp = "";
  //#endregion

  //#region Event handlers
  const handleOnButtonPress = (event: CustomEvent) => {
    sendKeyIdThoughtChannel(event.detail);
  };
  //#endregion

  //#region OnMount
  onMount(async () => {
    const gameConnectionOffer = await getGameConnectionOfferFromTheServer(id);

    const controllerAnswer = await initWebRTCPeerBasedOnOfferAndIceCandidates(
      gameConnectionOffer.offer,
      gameConnectionOffer.iceCandidates
    );

    remoteIp = calculateRemoteIpAddress(gameConnectionOffer.iceCandidates);

    const controllerIceCandidates = getIceCandidates();

    setTimeout(async () => {
      await postControllerConnectionAnswerToTheServer(
        id,
        controllerAnswer,
        controllerIceCandidates
      );
    }, 3000);
  });
  //#endregion
</script>

<div class="controller__container">
  <Status connectedTo={remoteIp} />
  <div class="controller__nintendo">
    <Nintendo on:buttonPress={handleOnButtonPress} />
  </div>
  <div class="controller__orientation-warning">
    <Warning />
  </div>
</div>

<style>
  .controller__container {
    width: 100%;
    height: 100vh;
    background-color: white;
    position: relative;
  }

  .controller__nintendo {
    width: 100%;
    height: 100%;

    @media (orientation: portrait) {
      display: none;
    }
  }

  .controller__orientation-warning {
    display: none;
    justify-content: center;
    align-items: center;
    position: absolute;
    width: 100%;
    height: 100%;

    @media (orientation: portrait) {
      display: flex;
    }
  }
</style>
