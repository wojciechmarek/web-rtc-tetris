<script lang="ts">
  import { onMount } from "svelte";
  import Nintendo from "../components/controller/Nintendo.svelte";
  import Status from "../components/controller/Status.svelte";
  import Warning from "../components/controller/Warning.svelte";

  import { ApiUtils, WebRTCUtils } from "@utils/index";

  const {
    initWebRTCPeerBasedOnOfferAndIceCandidates,
    getIceCandidates,
    calculateRemoteIpAddress,
    sendKeyIdThoughtChannel
  } = WebRTCUtils();
  const {
    getOfferAndIceCandidatesByIdFromTheServer,
    postTheAnswerAndIceCandidatesToTheServer
  } = ApiUtils();

  export let id: string;
  let remoteIp = "";

  onMount(async () => {
    const remoteOfferAndIceCandidates =
      await getOfferAndIceCandidatesByIdFromTheServer(id);
    const answer = await initWebRTCPeerBasedOnOfferAndIceCandidates(
      remoteOfferAndIceCandidates
    );

    console.log(remoteOfferAndIceCandidates);

    remoteIp = calculateRemoteIpAddress(
      remoteOfferAndIceCandidates.iceCandidates
    );

    const myIceCandidates = getIceCandidates();

    setTimeout(async () => {
      console.log("posting to the server:", id, answer, myIceCandidates);
      await postTheAnswerAndIceCandidatesToTheServer(
        id,
        answer,
        myIceCandidates
      );
    }, 1000);
  });

  const handleOnButtonPress = (event: CustomEvent) => {
    sendKeyIdThoughtChannel(event.detail);
  };
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
