Is resetting your smart bulb a bit tricky? If you're using Home Assistant, a blueprint can help you do this as long as you have a smart switch or smart plug with a lamp that HA can control.

Here's what you need to do (MANUALLY):
1. Download the YAML file

2. Upload this file to your HA system. The directory might be something like: /homeassistant/config/blueprints/automation/Rest_3R_Bulb/r3_light_factoryreset.yaml

3. Then, you'll see this blueprint in the HA GUI.

4. To create the automation using the blueprint, simply click into its detail page and create a "Boolean Input". This input allows the automation to be activated via a virtual switch. Just give it a name, create it, and select it.

5. Choose the "Light Switch" as the actuator for the automation, click save, and you're all set.

After completing these steps, you can activate the automation by manually running it or by going to Settings > Devices & Services > Helpers to turn on the viture switch.

We hope this blueprint saves you the trouble of resetting your bulb. 

Lastly, huge thanks to @russellhq for the idea for the code. Here is the original link: https://community.home-assistant.io/t/osram-zigbee-bulb-factory-reset/260725
