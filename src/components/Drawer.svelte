<script>
    export let open = false;
</script>

<div class:open>my drawer</div>

<style>
    div {
        /* animation: 3s linear 1s infinite running slidein; */
        height: 100px;
        background-color: red;
        left: -50%;
        position: absolute;
    }

    .open {
        left: 0;
    }
</style>
