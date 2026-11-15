# Engineering review — 14 November 2026

The project is feasible as a staged **bench sensor-pod prototype followed by a marine/control demonstrator**. The original plan was not credible as a promise of a qualified marine instrument, fully robust VCU, complete protocol implementation, and independently verified precision sensing within the stated daily blocks. Its strongest feature was one continuous project; that structure is retained.

All **113 active engineering lessons** have been rewritten with a bounded core task, verification, evidence, prerequisite guidance and optional extension. Existing dates and off-days are retained. The calendar is a target; the dependency gates decide when to proceed.

The original folder name is misleading: the plan already ran from **14 November 2026 to 28 March 2027**. The revised plan makes **23 January** an explicit, useful release milestone and treats the rest as an extension. Engineering has 3 h 15 per active day: 191 h 45 through Jan 23 and 367 h 15 in the full plan. These are available hours, not a prediction that every learner will finish every feature.

## Main changes and why

| Original issue | Where | Revision |
|---|---|---|
| Setup installed almost the entire toolchain before proving any tool worked | Nov 14 | Establish firmware build/debug and host tests first; install other tools when needed. |
| Requirements and verification criteria arrived at the end | Week 19 | Start 10–12 requirements, pin map and risks on Nov 21; maintain evidence at every gate. Final week closes the release. |
| Many sources/videos could not fit the 45-minute theory block | Throughout | One targeted source/section, recall and a prediction; no stealing verification time for open-ended reading. |
| Custom startup, linker work, bring-up and unfamiliar build tooling in one day | Nov 23 | Inspect/modify working vendor startup first; custom startup is a separate extension. |
| Maximum-clock programming introduced multiple power/flash/security dependencies immediately | Nov 23–24 | Inspect security settings, retain a verified clock baseline and measure a slow derived signal. No blind option-byte changes. |
| “Single producer/consumer” alone was treated as sufficient concurrency proof | Nov 26 | Specify ownership and synchronization; use bounded critical sections first and test wrap/overflow. |
| Null writes and recursive overflow were assumed to give clean diagnostic faults | Nov 27 | Use a controlled runtime divide trap and watchpoint; record actual exception/frame conditions. |
| SPI, sensor interrupt, I²C DMA and sustained 416 Hz were combined in one lesson | Dec 2 | Core is measured 208 Hz acquisition and loss accounting; SPI/DMA are independent optional branches. |
| Protocol throughput and packet/measurement-loss distinctions were underspecified | Dec 2–4 | Add worst-case framed-byte budget, boot IDs, bounded parser, independent event counters and deterministic corruption corpus. CRC is not perfect detection. |
| Nine clocks were assumed to recover any stuck I²C target | Dec 5 | Bound recovery and distinguish recoverable release from permanent-low failure. |
| A first custom buck/protection design was on the PCB critical path | Week 4 | Rev A uses a documented power module. Discrete power design stays in simulation/Rev B. |
| ≥36 V input rating plus an unspecified TVS was treated as sufficient for 24 V marine transients | Dec 7–8 | Define a bench input envelope and coordinate clamp voltage, overshoot, VGS, pulse energy and source impedance. Unsupported surge claims are removed. |
| The plan assumed all peripheral signals could be assigned through Arduino headers | Dec 9–10 | Verify actual alternate functions, connector access, conflicts and power paths before release; use Zio/morpho where required. |
| Transceivers were added before their interfaces had been learned/bench-tested | Dec 10 | Reserve documented external-module connections on Rev A; custom circuits become a later verified change. |
| Fabrication date overrode review completion | Dec 15 | Dec 15 is an order target; unresolved electrical/mechanical blockers hold the release. |
| Three-hour logging was implicitly inside a 2½-hour build | Dec 16 | Begin collection on Dec 15; distinguish active work from unattended elapsed time. |
| Allan minimum/noise-density comparison and calibration plots overstated conclusions | Dec 16–18 | State units/conventions, finite-record limits and held-out checks; sphere residual is not absolute heading accuracy. |
| GNSS rate/persistence was assumed rather than receiver/configuration dependent | Dec 22 | Start at 1 Hz, read back settings, measure rate and verify retained/reapplied configuration. Use u-center 2 for M10. |
| PPS fitting residual implied absolute timestamp accuracy | Dec 23–24 | Associate epoch correctly, validate on later edges and publish lock/holdover/uncertainty. Sensor latency and independent UTC accuracy remain distinct. |
| RTOS adoption had no working fallback, and an indiscriminately fed watchdog could hide task failure | Week 7 | Keep the superloop release, start with two tasks and feed watchdog from required-service progress. |
| Camera calibration could be “improved” by discarding views merely to hit an RMS target | Jan 5 | Preserve objective rejection reasons and evaluate separate views. |
| Horizon geometry and camera–IMU clock/frame mapping were too simplistic | Jan 7–8 | Use calibrated camera geometry, explicit axes and a controlled one-axis effective-delay experiment with independent segment checks. |
| Enclosure fit considered only the carrier STEP; January print lead time was too short | Week 9 | Measure the entire Nucleo/carrier/sensor stack, order a small coupon earlier and maintain a commercial-box fallback. |
| NMEA HDT was filled with magnetic heading; validity was assumed available in HDT | Jan 27; Mar 12 | Use magnetic sentence/reference semantics, suppress invalid HDT and define downstream freshness handling. |
| One SP3485 was conflated with a full-duplex link; raw differential lines were probed like logic pins | Week 11 | Separate TX/RX direction and pairs; use logic-side analyzer probes and rated instruments on the bus. |
| CAN termination, idle voltages and fault signatures were described too categorically | Week 12 | Use device-specific expectations and record actual outcomes. ACK-only errors and short unterminated buses do not guarantee the imagined result. |
| NMEA2000 transport, address management and many PGNs were new custom implementations in one week | Week 13 | Do an earlier stack feasibility check, integrate a maintained stack, start with three PGNs and retain an explicitly host-mediated fallback. |
| Gateway round-trip test could create feedback and obscure heading reference | Feb 12 | Add source identity, direction policy, loop tests and a combined quantization bound. |
| Ratiometry varied only sensor excitation, and open wiper could resemble a valid endpoint | Feb 16–17 | Use correct excitation/reference reasoning and reserved diagnostic margins; test legitimate ends as well as wiring faults. |
| 4.5 V output was connected to the helper ADC without a specified reduction; reset pulldown implied broad safety | Feb 18 | Protect ADC inputs, measure the affine transfer and define a separate bench enable/disable mechanism and tested fault envelope. |
| Environmental lessons included an improvised rotating imbalance and three hour-long cooling cycles in one session | Mar 4–5 | Use controlled low-energy sources and one matched condensation experiment; further cycles are explicit elapsed work. |
| Every heading failure, including startup reversal, was promised detectable | Mar 11 | Add detected/ambiguous/undetectable coverage. Independent alignment evidence is required for an internally consistent startup reversal. |
| Allan bias instability alone supposedly guaranteed a 30-second heading bound | Mar 12 | Evaluate declared model bounds against simulator truth over multiple dropout durations; shorten holdover when needed. |
| EEPROM, flash, CLI, migration and 100 physical interruptions were combined in one day | Mar 16 | Design/test the format the day before, implement one medium, test every write stage in software and a bounded set on hardware. |
| Controller, plant and HIL integration all started on one day | Mar 19 | Prepare/test the plant on Mar 18, reuse interlocks and tune against a declared model before hardware integration. |
| Productisation week generated all documentation, environmental tests, fixture and volume costs | Week 19 | Consolidate existing work, run selected missing tests, demonstrate a minimal fixture and estimate a 20-unit pilot with gaps visible. |

## Efficiency and workload judgement

The plan assumes basic C++ familiarity, not prior mastery of these hardware topics. The baseline exercise exposes that assumption early. If it fails, use recovery time to establish it and cut advanced branches; do not pretend the later driver work is independent of those skills.

The densest weeks remain **3 (acquisition/protocol), 4 (hardware decisions), 8 (vision), 13 (stack integration), 14 (analog interfaces) and 18 (persistence/HIL)**. They now have vendor/library scaffolding, smaller required subsets and explicit fallbacks. These changes improve feasibility; they cannot guarantee a daily duration before your actual pace is measured.

Each day contains 45 minutes of recall/targeted theory, 90 implementation, 30 verification, 15 evidence and 15 contingency. Saturdays reserve 60 implementation minutes for the oldest blocker or closed-book reconstruction. Dec 25 and Jan 9 are additional recovery slots. Long logging, shipping, printing and cooling are separately identified. If core work overruns twice in a week, split future lessons across sessions and shift dates; remove optional branches first.

Short lessons do not need artificial padding. Use one boundary test or a delayed recall check, then stop if the evidence is strong. Conversely, a single summary paragraph does not establish a practical skill: every promised practical outcome now points to an artifact and a test in the HTML’s outcome matrix.

The core result is **independent implementation and diagnosis of a bounded prototype**, not guaranteed professional mastery, certification or a deployable autopilot. Measured performance can legitimately fail a target: that completes a useful learning experiment but does not make the product requirement pass.

## Reference checks

The technical corrections were checked against manufacturer/maintainer sources. The revised HTML includes the linked reference register. Particularly relevant:

- The [ST U575 datasheet](https://www.st.com/resource/en/datasheet/stm32u575zi.pdf) confirms FDCAN; the [Nucleo manual](https://www.st.com/resource/en/user_manual/um2861-stm32u5-nucleo144-board-mb1549-stmicroelectronics.pdf) is the source for connector and power design checks.
- [NXP’s I²C specification](https://www.nxp.com/docs/en/user-guide/UM10204.pdf) supports bounded bus-clear handling; [Adafruit’s selected-board pinout](https://learn.adafruit.com/st-9-dof-combo/lsm6dsox-lis3mdl-pinouts) prevents confusing chip features with breakout access.
- The [M10 integration manual](https://content.u-blox.com/sites/default/files/documents/SAM-M10Q_IntegrationManual_UBX-22020019.pdf) governs configuration/rates/timing, with exposed signals documented by [SparkFun](https://docs.sparkfun.com/SparkFun_u-blox_SAM-M10Q/hardware_overview/).
- [TI’s protection note](https://www.ti.com/lit/an/slva139/slva139.pdf) and [TVS-coordination example](https://www.ti.com/lit/ds/symlink/lm74502-q1.pdf) support checking component stress instead of inferring protection from nominal voltage alone.
- [Allan-noise interpretation](https://www.mathworks.com/help/fusion/ug/inertial-sensor-noise-analysis-using-allan-variance.html), [OpenCV calibration](https://docs.opencv.org/4.10.0/da/d13/tutorial_aruco_calibration.html) and [pose estimation](https://docs.opencv.org/4.10.0/df/d4a/tutorial_charuco_detection.html) provide the basis for the revised measurement exercises.
- [OpenCPN’s sentence definitions](https://www.opencpn.org/wiki/dokuwiki/doku.php?id=opencpn%3Amanual_basic%3Anmea0183) distinguish true/magnetic heading; the [NMEA2000 library](https://github.com/ttlappalainen/NMEA2000) explicitly requires hardware adaptation on other systems. [python-can’s backend documentation](https://python-can.readthedocs.io/en/stable/interfaces/gs_usb.html) makes the adapter/toolchain dependency concrete.

This was a plan review. No actual carrier schematic, firmware, measurement logs or control hardware existed in the reviewed folder to validate. Exact BOM choices, final pin allocations, board settings, performance and quoted lead times must pass the scheduled design/measurement gates. Prices, stock and prior shopping-cart state were not rechecked or changed.

## File and scope notes

The generated HTML and its canonical Python source are updated together. Japanese scenarios, vocabulary data and personal-development source modules are preserved byte-for-byte; those tracks were not reviewed. Where their scenario prompts use hypothetical engineering results, the revised engineering requirements/evidence take precedence.

The HTML retains existing date-based completion keys. Previously ticked dates may still appear ticked even though their core criteria changed; recheck them against the new evidence requirement. Opening the output copy at a different file path may show different browser storage depending on the browser.

Validation results are recorded in `Validation Report.md`. The in-app browser blocked local-file preview, so no browser visual or interaction pass is claimed. The source/build, generated structure, anchors, calendar and non-engineering preservation were checked programmatically.
