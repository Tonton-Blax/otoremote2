<script>
  import { Camera, CameraResultType, CameraSource } from "@capacitor/camera";
  import { Capacitor } from "@capacitor/core";
  import { Device } from "@capacitor/device";

  const platform = Capacitor.getPlatform();

  const takePicture = async () => {
    const deviceinfo = await Device.getInfo();

    const photoOptions = {
      quality: 90,
      allowEditing: true,
      resultType: CameraResultType.Uri,
      source: CameraSource.Prompt,
    };

    if (deviceinfo.model === 'iPhone') {
      photoOptions.source = CameraSource.Photos;
    }

    const image = await Camera.getPhoto(photoOptions);

    // image.webPath will contain a path that can be set as an image src.
    // You can access the original file using image.path, which can be
    // passed to the Filesystem API to read the raw data of the image,
    // if desired (or pass resultType: CameraResultType.Base64 to getPhoto)
    var imageUrl = image.webPath;
  };
</script>

<p on:click={takePicture}>This is a camera</p>

<style>
  p {
    font-weight: 200;
  }
</style>
