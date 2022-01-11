<script>
    import { createEventDispatcher } from "svelte";
    import RangeSlider from "svelte-range-slider-pips";
    export let speed = [7];
    const dispatch = createEventDispatcher();
    //let bipolar = 
    let values =  [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14];
    let sliderValues = [...values]
</script>


<div class="column">
    <RangeSlider float pips
        vertical id="reverse-pips"
        min={0}
        max={14}
        all='label'
        bind:values={speed}
        formatter={ v => sliderValues[v] }
        on:change={(e) => dispatch("speed", sliderValues[e.detail.value])}
    />
</div>

<style>
    :global(.rangeSlider.vertical) {
        min-height: var(--screen-height-weighted)
    }
</style>