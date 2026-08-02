# SignalRGB Corsair iCUE LINK Hub — XC7 Temperature Fix

Drop-in replacement for SignalRGB’s built-in **Corsair iCUE LINK Hub** plugin.

**Fixes:** LINK XC7 RGB Elite cold-plate temperature not showing (stock plugin sets `probe: false` and binds temps via a shared shift pool).

This fork maps temperature (and RPM) sensors by **hub channel index**. XC7-only setups (no fans) can still register and poll temperature.

Plugin file: `Corsair_ICUE_Link_Hub_Fix_Temp.js`. Device `Name()` matches stock (`Corsair iCUE LINK Device`), so a custom install **overrides** the built-in plugin for the same VID/PID.

[![Add To SignalRGB](https://marketplace.signalrgb.com/resources/add-extension-256.png "Add to My SignalRGB Installation")](https://srgbmods.net/s?p=addon/install?url=https://github.com/hceve520/signalrgb-corsair-icue-link-xc7-fix-temp)

## Preview

[![Preview](https://i.imgur.com/QI9zaEf.png)](https://imgur.com/a/cGmJRRf)

## Install

### One-click

1. Click **Add To SignalRGB**.
2. Confirm the SignalRGB prompt and restart if asked.
3. Open the iCUE LINK Hub device — XC7 should expose a temperature sensor.

One-click URL:

```text
https://srgbmods.net/s?p=addon/install?url=https://github.com/hceve520/signalrgb-corsair-icue-link-xc7-fix-temp
```

### Manual

1. Copy `Corsair_ICUE_Link_Hub_Fix_Temp.js` to:

   `%userprofile%\Documents\WhirlwindFX\Plugins\`

2. Restart SignalRGB.

User plugins in Documents override AppData built-ins with the same VendorId + ProductId. The device page should show it as a **Custom User Plugin**.

## What changed vs stock

| Area | Stock | This fix |
|------|--------|----------|
| XC7 (`type 0x09`) | `probe: false` | `probe: true` |
| Temp binding | Non-zero slots + `shift()` pool | Hub **channel** index |
| Temp parse | Ignore status byte | `status == 0x00` = Available |
| Temp-only hub | Enumeration waits forever for fans | Temps alone are enough to start polling |

## Requirements

- [SignalRGB](https://www.signalrgb.com/)
- Corsair iCUE LINK System Hub + LINK XC7 RGB Elite
- Prefer quitting iCUE when testing exclusive HID access (this plugin uses the Corsair mutex)

## Credits

- Base plugin: SignalRGB / WhirlwindFX `Corsair_ICUE_Link_Hub.js`

## License

MIT

## Disclaimer

Not affiliated with Corsair, WhirlwindFX, or SignalRGB. Use at your own risk. Community override of a built-in plugin may miss future stock updates until you remove the custom file.
