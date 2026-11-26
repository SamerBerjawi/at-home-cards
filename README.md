# At Home Cards

Custom Lovelace cards for Home Assistant, adapted from the [HAD dashboard](https://github.com/SamerBerjawi/had-homeassistantdashboard).

The preview includes twelve overview cards. Future releases will bring more of HAD's overview cards, room tiles, and entity cards to Lovelace.

## Install the preview

1. In Home Assistant 2026.11 or later, open **Settings → Marketplace → Add from link** and connect GitHub if prompted.
2. Enter `SamerBerjawi/at-home-cards` and choose **Dashboard** if asked for a type.
3. Open **At Home Cards**, select **Install**, then reload Home Assistant in your browser.
4. Edit a dashboard and select **Add card**, then choose **At Home People** or **At Home Lighting**.

If you manage dashboard resources in YAML, add the JavaScript module URL shown by Marketplace during installation.

## People card

The People card shows who is home, who is away, and named zones such as work or school. It displays entity photos or initials. Select a portrait to open the person’s HAD details sheet.

Leave the entity selector empty to use visible `person` entities automatically, with device trackers as a fallback if there are no visible people. Select entities to show a specific household or group. You can also add a title and resize the card in the **Layout** tab of a Sections dashboard.

```yaml
type: custom:at-home-people-card
title: Household
entities:
  - person.alex
  - person.jordan
```

The cards run in Home Assistant using its current session. This repository distributes the built JavaScript module.

## Lighting card

Add **At Home Lighting** (`custom:at-home-lighting-card`) to discover lights automatically, or select specific lights in the editor. Use the expand arrow to open the room list, search lights, switch them individually or together, and adjust supported brightness controls.

## Widget size

Open the card editor and select a tile size. The four HAD presets are 1×1, 2×1, 1×2, and 2×2. In a Sections dashboard, one unit spans six Home Assistant grid columns (half a section) and three rows. Larger presets multiply those spans. Selecting a preset clears any saved width and height overrides so Home Assistant uses the recommended size. After upgrading, reselect your preset and save once. Masonry controls its own column widths. In YAML, use values such as `size: 1x2`.

## Overview cards

In the dashboard card picker, search for **At Home**. The collection includes People, Lighting, Switches, Fans, Scenes, Areas, Doors & windows, Weather, Thermostat, Media, Vacuums, and Cameras. Each card has an entity or area selector, an optional title, four size presets, and an expandable details sheet.

The cards render HAD’s overview widgets and Pro sheets. Weather includes the Sky, Minimal, and Trend designs. Selecting a room opens its area details inside Lovelace. Cameras use the installed WebRTC Camera player when available, with the Home Assistant player as the default on installations without WebRTC Camera. Available actions, camera playback, history, and forecasts depend on the selected integration and its capabilities.

## Camera streams

By default, At Home Cameras passes the selected camera entity to the player. If your working WebRTC Camera card uses a go2rtc stream name, RTSP URL, or a list of streams, copy its playback options under the corresponding camera entity in the At Home card’s YAML editor.

```yaml
type: custom:at-home-cameras-card
entities:
  - camera.front_door
webrtc:
  camera.front_door:
    url: front_door_hd
    mode: webrtc
```

Open the Cameras Pro sheet to play the selected stream. Compact tile designs can show a still preview.

## Room card

Choose **At Home Room** to show one Home Assistant area using HAD’s Rooms page tile. Select the room and tile size in the visual editor. A tap on the tile opens the selected area’s details. Quick actions depend on the devices assigned to that area. Use **At Home Areas** for the multi-room overview.

```yaml
type: custom:at-home-room-card
area: living_room
size: 2x1
```

Each Room card has its own appearance and quick-action settings in the visual editor. Enable **Area pictures** to use the picture assigned to the area in Home Assistant. Choose temperature or humidity as the primary reading, control the visibility of readings, status, activity, and counts, and choose which quick actions the tile can offer. The compact tile supports a lights action. Standard and expanded tiles can show up to two and three available actions respectively. The editor saves these settings under `room_options`.

Room tiles adapt to their rendered dimensions. Use the Room-only `2x0.5` preset for a compact horizontal tile (12 columns by 2 Sections rows). A full-height narrow tile stacks the controls above the room name and reading. Taller tiles can also show wrapped activity details.

## Entity cards

Add **At Home Light Entity**, **At Home Fan Entity**, **At Home Switch Entity**, or **At Home Scene Entity** and choose one entity in the visual editor. Each supports an optional display name and five tile sizes. The larger layouts expose additional controls when supported by the device.

| Batch | HAD entity tiles | Status |
| --- | --- | --- |
| 1 | Light, Fan | Updated in v0.2.14 |
| 2 | Switch (including plugs and helpers), Scene (including scripts and buttons) | Available in v0.2.14 |
| 3 | Climate, Cover, Sensor reading | Planned |
| 4 | Media player, Vacuum | Planned |
| 5 | Camera, Opening | Planned |
| Deferred | Lock, Motion, Safety, Car | Revisit with Security and Mobility |

The entity editor can require confirmation before a power toggle or scene run. Switch Entity accepts switches and input booleans. Its display role can be automatic, switch, plug, helper, or light. Scene Entity accepts scenes, scripts, and buttons and dispatches the matching Home Assistant service.
