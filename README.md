# @rowbotik/bambu-node

A fork of [THE-SIMPLE-MARK/bambu-node](https://github.com/THE-SIMPLE-MARK/bambu-node) with added support for **Bambu Lab H2S and H2D** printers.

## What's different

The upstream library only recognises X1C, X1, X1E, P1P, P1S, A1, and A1M. H2S and H2D firmware never responds to the `get_version` round-trip the library uses for model detection, so connecting to either printer threw `"Printer model not supported!"`.

This fork adds:

| Serial prefix | Model |
|---|---|
| `093` | H2S |
| `094` | H2D |

Both are now present in the `PrinterModel` enum and are detected from the OTA module serial number like every other model.

## Installation

```bash
npm install @rowbotik/bambu-node
```

If you're already using `bambu-node` and want to swap without changing any imports:

```bash
npm install bambu-node@npm:@rowbotik/bambu-node
```

## Usage

Identical to the upstream package — see the [original README](https://github.com/THE-SIMPLE-MARK/bambu-node) for full API documentation.

```typescript
import { BambuClient, PrinterModel } from "@rowbotik/bambu-node"

const client = new BambuClient({
    host: "192.168.1.x",
    accessToken: "your_access_token",
    serialNumber: "093...",   // H2S
})

await client.connect()
// client.data.model === PrinterModel.H2S
```

## Supported models

| Model | Serial prefix | Notes |
|---|---|---|
| X1C | `00M` | |
| X1 | `00W` | |
| X1E | `03W` | |
| P1P | `01S` | |
| P1S | `01P` | |
| A1 | `030` | |
| A1 Mini | `039` | |
| H2S | `093` | Added in this fork |
| H2D | `094` | Added in this fork |

## Contributing

PRs welcome. If the upstream project gains H2S/H2D support this fork will become redundant — raise an issue or PR there first.

## License

[MIT © Márk Böszörményi, Aaron Scherer](LICENSE)
