# Guidelines for Rome Repo

_Last updated 10th of March, 2026 - 15:02_

## Device Requirements
On par with the Rome app, this should only have ROMs for devices shipped with **Android 10+**, which I see as a good balance between extensiveness and overwhelmingness.

## Glossary
Please make sure to always use these names/this wording when applicable.

| Category  | Meaning and usage |
|-----------|-------------------|
| "Factory" | A manufacturer's default skin for said device, for example a MIUI rom for a Xiaomi phone is considered factory firmware.
| "AOSP"    | AOSP, Pixel-like or similar ROMs (such as LineageOS, Evolution X, crdroid, etc.) |
| "Port"    | A skin that isn't officially supported by it's original manufacturer, for example: an OxygenOS ROM for a Xiaomi phone is considered a port. **This category includes GSIs and must only be included if compatibility is verified for said device.** |

The following table is what is identified by the Rome app.

| Skin codename | Full name             |
|---------------|-----------------------|
| `los`         | LineageOS             |
| `evox`        | Evolution X           |
| `miui`        | MIUI                  |
| `hyos`        | Xiaomi HyperOS        |
|- UPCOMING SKINS BELOW -|- NOT YET SUPPORTED BY ROME APP -|
| `infx`        | Infinity X            |
| `mieu`        | Any Xiaomi.eu ROM     |
| `oneu`        | Samsung OneUI         |
| `oxos`        | OnePlus's OxygenOS    |
| `coos`        | Oppo's ColorOS        |

## Device folder structure
Add it's folder in the project root, referencing it by it's codename (i.e. `sapphire/`).

> If two phone models have support for eachother's ROMs (such is the case with the `sapphire` and `sapphireN`), make sure they alias to one another.
>
> It is not necessary to fill out support, SOC or other info aside the market name for aliased devices, see folder structure of the `sapphire` and `sapphireN` for reference.

Your `info.json` should look like this:
```
{
    "marketName" : "Redmi Note 13 (4G)", // Full market name
    "types" : ["factory", "aosp", "port"], // Supported/existing ROMs
    "type" : "phone", // "phone", "tablet", "dap", "emulator"
    "soc" : {
        "manufacturer" : "qc", // "qc": "Qualcomm"; "mt": "MediaTek"
        "displayName" : "Snapdragon 685", // SOC's market name
        "model" : "SD6225" // Internal model name
    },
    "aliasOf": "sapphiren" // Add only in case of shared support, otherwise remove.
}
```

Add `factory/`, `aosp/` and `port/` ROMs as supported.

For the `factory/` folder, add a `list.json` like this:
```
{
    "V14.0.4.0.TNGMIXM" : { // Version name as referenced by manufacturer
        "url" : "https://example.com/rom-file.zip", // Prefer using direct downloads instead of file sharers if possible.
        "initialBuild" : true, // Whether it's the earliest firmware for said phone.
        "skin" : "miui", // See skin codename chart
        "androidVersion" : "13",
        "skinVersion" : "14.4" // Display-friendly version name, should follow the X.Y(.Z) scheme
    }
}
```

### About the `aosp/` folder especifically
Separate AOSP skins by their folders and a similar format as follows the JSON above.