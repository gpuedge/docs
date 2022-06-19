---
id: hello-docker
title: Hello Docker
#sidebar_label: 🧮 Count on NEAR
---

Lets use the Web UI to run a simple Docker job. We will
  1. Find a node with available resources and run Docker `Hello World`
  2. Select resources we want to utilize
  3. Approve the wallet deposit
  4. Read the output
  5. Collect our refund

## Launching Docker
  1. Click Misc->Docker Container
  <img src={require("@site/static/docs/assets/misc_docker_title.png").default}  />
  2. Leave defaults. 2 CPU, 2 RAM, 0 GPU  
  (0.0077) is our credit cost per hour  
  1hr is our maximum duration  
  Press `Run!`
  <img src={require("@site/static/docs/assets/misc_docker.png").default}  />
  3. Approve the wallet deposit. (Enable popups)
  <img src={require("@site/static/docs/assets/wallet_approve.png").default}  />
  4. 📜 For logs. ❌ to cancel
  <img src={require("@site/static/docs/assets/table_1.png").default}  />
  <img src={require("@site/static/docs/assets/logs.png").default}  />
  4. View total spent (after deposit refund)
  <img src={require("@site/static/docs/assets/table_2.png").default}  />

## Moving Forward

Try to change the cpu count or ram now, or add GPUs.

Happy coding!
