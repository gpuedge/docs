---
id: hello-blender
title: Hello Blender
#sidebar_label: 🧮 Count on NEAR
---

Lets use the Web UI to run a simple Blender job. We will
  1. Find a node with available resources and run Blender 3.1
  2. Utilize all resources rendering Sample Deer (https://cloud.blender.org/p/gallery/6220ae43b4a486f53171c89e)
  3. Approve the wallet deposit
  4. View the logs
  5. Download our render

## Launching Blender
  1. Click Rendering->Blender
  <img src={require("@site/static/docs/assets/blender_title.png").default}  />
  2. Blender job automatically uses all available resources.  
  Set `Source URL` to the sample deer  
  https://storage.googleapis.com/5649de716dcaf85da2faee95/_%2Fbb3bb6d76cec47d696f661b4e062c28c.blend?GoogleAccessId=956532172770-27ie9eb8e4u326l89p7b113gcb04cdgd%40developer.gserviceaccount.com&Expires=1655298847&Signature=WPYK9dnf1nuT97CPKNAKWN9e9bU7%2FLAnEPJDRSFz0l%2FanrtyZWAZdk%2B0AtTURe7mwPUFfYnR1PV%2F2t7nj0ZKYslSMMdtI3yeKY3%2BRAl3Aewl6RSGjrHGHd2rBVxyfvd6%2B0u8JkFgeOuzQOSS0psBpR7sEyMDRvpCMA1j6rD7p7s4XkZn5BiBy%2F7ByYR0QOu%2BWhyfJNEmKg9h2sNzsFpg9B8u19pK904Ib0yni%2BY6qvkuDximuo42wnFikwKRbbtoJ3i6UM5Wx6zWkrJQMlpfbZzkrOcohuyNgSuHJy%2BkFa2fjbPZI1XrxDehOTo8ME8VgFDb0mv9yLKvQOJOFn5QGQ%3D%3D  
  Set `Samples` to 1000  
  Set `Width` to 3840  
  Set `Height` to 1920  
  (0.6658) is our credit cost per hour  
  1hr is our maximum duration  
  Press `Blend!`
  <img src={require("@site/static/docs/assets/blender.png").default}  />
  3. Approve the wallet deposit. (Enable popups)
  <img src={require("@site/static/docs/assets/wallet_blender_approve.png").default}  />
  4. 📜 For logs. ❌ to cancel
  <img src={require("@site/static/docs/assets/table_1.png").default}  />
  <img src={require("@site/static/docs/assets/logs_blender.png").default}  />
  5. View render by clicking `download` then extracting the zip
  <img src={require("@site/static/docs/assets/blender_download.png").default}  />
  <img src={require("@site/static/docs/assets/blender_zip.png").default}  />
  <img src={require("@site/static/docs/assets/blender_out.png").default}  />

## Moving Forward

Try to render your own `.blend` file now!
