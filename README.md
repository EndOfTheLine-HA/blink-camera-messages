# Blink Camera Messages

<img src="docs/logo.svg" alt="Blink Camera Messages logo" width="128">

Create Home Assistant buttons that speak saved messages through compatible
Blink camera speakers. Home Assistant renders your text with your chosen
text-to-speech provider, then sends the audio over MQTT. BlinkBridge plays
it over the camera's existing IMMI live view.

[![Open in Home Assistant Marketplace](https://my.home-assistant.io/badges/marketplace_repository.svg)](https://my.home-assistant.io/redirect/marketplace_repository/?owner=EndOfTheLine-HA&repository=blink-camera-messages&category=integration)

## Install and configure

1. Set up [BlinkBridge with MQTT speaker support](https://github.com/EndOfTheLine-HA/blinkbridge/tree/codex/blink-speaker-poc).
   Configure your camera in BlinkBridge's `cameras.live` list. Use the same
   MQTT broker as Home Assistant.
2. Open **Settings → Marketplace → Add from link** and enter
   `EndOfTheLine-HA/blink-camera-messages`. Choose **Integration** if prompted.
   Install it and restart Home Assistant.
3. In **Settings → Devices & services → Add integration**, select **Blink
   Camera Messages**. Enter the BlinkBridge MQTT topic prefix (default
   `blinkbridge`) and choose a text-to-speech provider.
4. Open **Configure → Add message**. Choose a button name and camera, enter
   the message and optionally set a volume boost. Press the resulting
   button to test it. Use **Configure** to edit or remove presets.

The integration requires Home Assistant 2026.11.0 or newer. Saved button
playback and a Frigate face recognition automation were tested on a Blink
Mini with video still reaching Frigate after playback.
Playback requires a currently active IMMI live view. Keep messages under
17 seconds. Volume boost requires FFmpeg on the Home Assistant host.

## Automations

Use **List cameras** to find the camera ID. Call **Speak through Blink camera**
with plain text or a template.

```yaml
action: blink_camera_messages.speak
data:
  camera: "123456789"
  message: "Thank you for the delivery."
```

See the [Frigate example](examples/frigate-greeting.yaml) for a face event
with an explicit name mapping and cooldown. Replace the example camera
names and ID before enabling it.

The Home Assistant setup and preset flow are adapted from
[Ring Camera Messages](https://github.com/EndOfTheLine-HA/ring-camera-messages)
under its MIT license.
