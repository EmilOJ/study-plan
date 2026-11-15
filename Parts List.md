# Engineering parts and procurement gates

Revised 14 November 2026. This is the authoritative specification checklist for the revised plan, not a confirmed shopping cart or current price list. Check the exact module revision, supply/logic levels, exposed pins, shipping and vendor documentation before ordering. The HTML table and core checklist use the same architecture.

## Core and PCB

| Needed by | Item | Acceptance before purchase/use |
|---|---|---|
| Nov 14 | Owned NUCLEO-U575ZI-Q; USB data cable | Official example builds, flashes and reaches a breakpoint. Record board revision. |
| Nov 19 | Multimeter, PulseView-compatible analyzer, solder/flux/wick, headers, breadboard and passives | Check analyzer input limits, meter fuses and exact header pitch. Logic analyzer is not an analog scope. |
| Nov 30 | Adafruit 4517 LSM6DSOX + LIS3MDL breakout | I²C and interrupt pins exposed; correct logic supply and effective pull-ups. Use I²C on this combination board. |
| Dec 7 | Current-limited bench supply and documented wide-input 5 V regulator module | Support the proposed 9–30 V bench envelope at derated load; check connector and thermal limits. Select actual module before footprint/layout. |
| Dec 7–15 | Fuses/holders, appropriate protection parts, decoupling, headers, mounting hardware and test points | Size from the actual power/stress/pin map. TVS nominal voltage alone does not establish protection. |
| Dec 15 target | Carrier fabrication/assembly | Order after schematic/pin/fit/layout/export reviews. Get quote including assembly, shipping and holiday lead time. Number of boards follows the quote; no assumed $30–60 total. |
| Dec 21 | SparkFun SAM-M10Q breakout; 3.3 V USB-UART with exposed TX/RX/GND | UART and PPS exposed; compatible with u-center 2. Configure/reapply settings reproducibly. No RTK hardware required. |
| Jan 4 | Existing USB camera; flat ChArUco board; rigid camera/IMU mount | Verify capture, fixed focus/resolution and manual exposure if available. Vision runs on PC. No custom optical window in core. |
| Jan 11–22 | Calipers, commercial gasketed box, O-ring/seal coupon, matching glands, fasteners/inserts, optional print | Fit the complete Nucleo/carrier/sensor assembly, cable bends and debug access. Order coupon early; custom enclosure delivery is not a January gate. |

An oscilloscope with suitable probes is useful for power and analog lessons; borrowing/shared access is sufficient. Without it, mark analog waveform/ripple measurements unavailable and use simulations plus meter/digital evidence within their limits.

## Marine/control extension

| Needed by | Item | Quantity/scope |
|---|---|---|
| Jan 26 | 3.3 V logic-compatible RS-422 interface and USB-RS422 adapter | One full-duplex module **or two** SP3485-class half-duplex modules for separate fixed TX/RX directions. The adapter must expose the required pairs. |
| Feb 1 | CAN transceiver module and USB-CAN adapter | One transceiver for the U575 plus one adapter forms two nodes. Verify transceiver supply separately from logic I/O. Confirm the exact Windows driver/backend works before week 12. |
| Feb 1 | Twisted pair, 2 × 120 Ω termination, reference-ground wire | Isolated lab bus. A second transceiver is useful only with another CAN controller; C031 is not one. |
| Feb 13, optional | Micro-C starter kit, compatible field connector, fused 12 V power tap | Exact mating pinout/voltage verified. Never feed 24 V to NET-S. Twisted-pair lab substitute is acceptable. |
| Feb 15 | Two 10 kΩ pots or dual-gang pot, end-stop resistors, RC components and neutral microswitch | Opposite-track diagnostics and reserved voltage margins. A dual gang is not certified redundant sensing. |
| Feb 18 | MCP6002, reference/summing-network parts, trimmers, output-disable gate/relay parts, dummy load | Exact circuit must be simulated/reviewed for gain/offset, swing, reset and supply-loss cases. Reserve a protected divider/buffer before C031 ADC measurement of up to 4.5 V. |
| Feb 19 | LM393, hysteresis/pull-up resistors, clamps/attenuation and optional 12 V pulse fixture | One comparator conditioner is required; optocoupler variant is optional. Check common-mode range and use a 3.3 V logic-side pull-up. |
| Mar 1 | Correct ring-terminal and ferrule crimp tooling/dies, matching terminals/wire, strain relief, adhesive heat-shrink, glands, tape | Separate tooling may be needed for different terminal families. No mandatory coax/SMA purchase for the M10. |
| Mar 5 | SHT40 breakout and sacrificial/empty enclosure | Bounded condensation experiment; main electronics stay out. Desiccant/vent comparison is an extension. |
| Mar 15 | 24LC256, decoupling/pull-ups and verified low-voltage power-cut switch/fixture | One required parameter-storage medium. Cuts must not be bypassed by USB, debugger or signal backpower. |

## Optional hardware, only for a chosen extension

- Reviewed optoisolated listener: select a complete receiver design. A 6N137 sketch requires its actual supply, enable, pull-up and input-current constraints; do not assume 3.3 V supply compatibility.
- USB isolator: verify speed, power and interface compatibility. It may not work for the USB camera or every ST-LINK configuration and is not a universal protection guarantee.
- Logic-level MOSFETs: check guaranteed RDS(on) at a gate voltage no higher than the actual drive; “logic level” or threshold voltage is insufficient. SMD devices may need adapters.
- Real dual-antenna/RTK receivers and antennas are outside this plan’s core. The heading week uses SAM-M10Q diagnostics and a simulator.

The old cart notes and distributor stock assertions have been removed from the active checklist because they were not verified during this review. No purchases, cart changes or messages to suppliers were made.
