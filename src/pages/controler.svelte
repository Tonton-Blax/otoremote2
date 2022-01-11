<script>
    import UnipolarGauge from "@components/UnipolarGauge.svelte";
    import BipolarGauge from "@components/BipolarGauge.svelte";
    import BipolarPad from "@components/BipolarPad.svelte";
    import UnipolarPad from "@components/UnipolarPad.svelte";
    import UnipolarSlider from "@components/UnipolarSlider.svelte";
    import BipolarSlider from "@components/BipolarSlider.svelte";
    import { onMount } from 'svelte'
    import Button, { Label } from '@smui/button';
    export let polarity = "Unipolar"
    const compTypes = ["Gauge", "Pad", "Slider"]
    let compTypesIndex = 0;
    let comp = { UnipolarGauge, BipolarGauge, BipolarPad, UnipolarPad, UnipolarSlider, BipolarSlider }
    $: console.log(compTypesIndex);

    onMount(async()=>{
        const root = document.documentElement;
        root.style.setProperty('--screen-width', window.screen.width * 0.8 + "px");
        root.style.setProperty('--screen-height', window.screen.height * 0.8 + "px");
        root.style.setProperty('--screen-height-weighted', window.screen.height * 0.65 + "px");
    })
</script>

<main>
    <svelte:component this={comp[polarity + compTypes[compTypesIndex]]} />
</main>
<section>
    <Button on:click={() => polarity = polarity == "Unipolar" ? "Bipolar" : "Unipolar"} variant="unelevated">
        <Label>{polarity == "Unipolar" ? "Bipolar" : "Unipolar"} </Label>
    </Button>
    <Button on:click={() => compTypesIndex = compTypesIndex === compTypes.length - 1 ? 0 : compTypesIndex + 1 } variant="unelevated">
        <Label>{compTypes[(compTypesIndex + 1) % (compTypes.length)]}</Label>
    </Button>
</section> 

<style>
    :global(body) {
        height:100vh;
        overflow-y: hidden;
    }
       main {
           display:flex;
           justify-content: center;
           align-items: center;
           height:fit-content;
       }
</style>