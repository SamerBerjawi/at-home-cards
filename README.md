# At Home Cards

Custom Lovelace cards for Home Assistant, adapted from the [HAD dashboard](https://github.com/SamerBerjawi/had-homeassistantdashboard).

The preview includes the People and Lighting cards. Future releases will bring more of HAD's overview cards, room tiles, and entity cards to Lovelace.

## Install the preview

1. In Home Assistant 2026.11 or later, open **Settings → Marketplace → Add from link** and connect GitHub if prompted.
2. Enter `SamerBerjawi/at-home-cards` and choose **Dashboard** if asked for a type.
3. Open **At Home Cards**, select **Install**, then reload Home Assistant in your browser.
4. Edit a dashboard and select **Add card**, then choose **At Home People** or **At Home Lighting**.

If you manage dashboard resources in YAML, add the JavaScript module URL shown by Marketplace during installation.

## People card

The People card shows who is home, who is away, and named zones such as work or school. It displays entity photos or initials. Select a portrait to open Home Assistant's entity details.

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

Open the People or Lighting card editor and select a tile size. The four HAD presets are 1×1, 2×1, 1×2, and 2×2. In a Sections dashboard, one unit spans two default-mode columns (half a section) and three rows. Larger presets multiply those spans. Selecting a preset clears any saved width and height overrides so Home Assistant uses the recommended size. After upgrading, reselect your preset and save once. Masonry controls its own column widths. In YAML, use values such as `size: 1x2`.
