<script>
    import { Device } from "@capacitor/device";
    async function getInfo() {
        const info = await Device.getInfo();
        alert(JSON.stringify(info));
    }
</script>

<div on:click={getInfo}>Device?</div>
