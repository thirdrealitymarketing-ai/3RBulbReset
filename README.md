Is resetting your smart bulb a bit tricky? If you're using Home Assistant, a blueprint can help you do this as long as you have a smart switch or smart plug with a lamp that HA can control.

Here's what you need to do:
1. Create a text file, open it, and copy the following code:
----------------------------------------Do NOT Copy This Line----------------------------------------

blueprint:
  name: Third Reality Zigbee Bulb Factory Reset
  description: Factory resets Third Reality Zigbee bulbs for re-pairing with a ZigBee Hub
  domain: automation
  input:
    input_boolean:
      name: Input Boolean
      description: This Input boolean will trigger the factory reset automation
      selector:
        entity:
          domain: input_boolean
    light_switch:
      name: Light Switch
      description: The light switch to use for factory resetting the Third Reality bulb
      selector:
        entity:
          domain: switch
trigger:
  - entity_id: !input input_boolean
    from: 'off'
    platform: state
    to: 'on'

action:
  - service: switch.turn_on
    entity_id: !input light_switch
  - delay: '3'
  - repeat:
      count: '5'
      sequence:
        - service: switch.turn_off
          entity_id: !input light_switch
        - delay: '1'
        - service: switch.turn_on
          entity_id: !input light_switch
        - delay: '1'
  - service: input_boolean.turn_off
    entity_id: !input input_boolean

----------------------------------------Do NOT Copy This Line----------------------------------------

2. Rename this text file to *.yaml. For example: [r3_light_factoryreset.yaml]

3. Upload this file to your HA system. The directory might be something like: /homeassistant/config/blueprints/automation/Rest_3R_Bulb/r3_light_factoryreset.yaml

4. Then, you'll see this blueprint in the HA GUI.

5. To create the automation using the blueprint, simply click into its detail page, and create a "Boolean Input". This input allows the automation to be activated via a virtual switch. Just give it a name, create it, and select it.

6. Choose the "Light Switch" as the actuator for the automation, click save, and you're all set.

After completing these steps, you can activate the automation by manually running it or by going to Settings > Devices & Services > Helpers to turn on the viture switch.

We hope this blueprint saves you the trouble of resetting your bulb. Lastly, thanks to @russellhq for the idea for the code. Here is the original link: https://community.home-assistant.io/t/osram-zigbee-bulb-factory-reset/260725
