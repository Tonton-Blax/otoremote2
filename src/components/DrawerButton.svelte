<script>
    export let open = false;
</script>

<div on:click="{() => open = !open}">
   X
</div>

<style>
    div {
        background-color: orange;
        height: 100px;
        width: 100px;
        font-weight: bold;
    }
</style>