<script>
    var name = "Dashbox";
    var image = "dashbox.png";
    import Camera from "@components/Camera.svelte";
    import Drawer from "@components/Drawer.svelte";
    import DrawerButton from "@components/DrawerButton.svelte";
    import DeviceInfo from "@components/DeviceInfo.svelte";

    let open = false;
</script>

<Drawer bind:open />
<DrawerButton bind:open />
<DeviceInfo />
<div class="main">
    <img src={image} alt="svelte and capacitor logos" />
    <h1>Welcome to {name}!</h1>
    <span><a href="/controler">Favorites</a></span>
    <spane><a href="/pacers">Pacers</a></spane>
    <Camera />
</div>

<style>
    .main {
        text-align: center;
        margin: 50px auto;
    }

    img {
        max-width: 100%;
    }
</style>
