---
title: "Heathkit SB-301 Receiver — Restoration Plan"
subtitle: "Rev. 2 — checked against the original Heath assembly manual (595-946-01)"
date: "October 2026"
geometry: margin=0.9in
fontsize: 10pt
colorlinks: true
toc: true
---

<!-- Build: pandoc sb301-restoration-plan.md -o sb301-restoration-plan.pdf --pdf-engine=xelatex -V mainfont="DejaVu Serif" -->

# 1. Source documents

| Document | Where | Use |
|---|---|---|
| **Heath SB-301 Assembly & Operation manual**, 595-946-01 (©1966, printed 11-29-68), 100 pp. + fold-outs | Free PDF from W5RKL (w5rkl.com) | **Primary reference.** Parts lists, resistance chart (Fig. 1-1), alignment, voltage/resistance charts (Figs. 5-2, 5-3), troubleshooting chart, schematic. |
| AF6C "Heathkit of the Month #36" | w6ze.org | Background and history. |
| K9STH LMO service notes | Linked from heathkit-interests.blogspot.com | Read before opening the LMO. |
| Heath list archive / Heathkit-Radios (groups.io) | puck.nether.net, groups.io | Field experience on failures. |

**Manual page references below use the manual's printed page numbers**, not PDF page numbers. In the W5RKL scan, the Specifications section is bound at the back, after the parts list.

**Numbering scheme (schematic note 1):** 0–99 = RF board, 100–199 = IF board, 200–299 = chassis. Resistors are 1/2 W unless marked. The manual's voltages are measured with an 11 MΩ VTVM, ±10% on the schematic and ±20% on Fig. 5-3.

# 2. Receiver at a glance

## 2.1 Factory specifications

| Item | Spec |
|---|---|
| Coverage | 3.5–4.0, 7.0–7.5, 14.0–14.5, 15.0–15.3 (WWV), 21.0–21.5, 28.0–30.0 MHz |
| IF | 3.395 MHz (1st IF 8.395–8.895 MHz passband coupler T2) |
| Sensitivity | < 0.25 µV for 10 dB (S+N)/N, SSB |
| Overall gain | < 1.5 µV for 0.5 W audio |
| Stability | < 100 Hz/hr after 20 min warm-up; < 100 Hz for ±10% line change |
| Audio | 1 W at < 8% distortion; 8 Ω speaker, high-Z phones, 500 Ω anti-VOX |
| Power | 105–125 / 210–250 VAC, 50/60 Hz, **50 W** |
| Fuse | **2 A slow-blow** (120 V); 1 A slow-blow (240 V) |
| Pilot lamps | **#47** (×2, sockets TA and TK) |
| Filters | SSB 2.1 kHz @6 dB / 5.0 kHz @60 dB (supplied); SBA-301-1 AM 3.75/10 kHz; SBA-301-2 CW 400 Hz/2.0 kHz |

## 2.2 Tube complement (per manual)

| V | Tube | Function | Failure notes |
|---|---|---|---|
| V1 | 6BZ6 | RF amp | Gas → AGC line pulled positive; weak → poor high bands |
| V2 | 6AU6 | 1st mixer | Moderate |
| V3 | 6AU6 | 2nd mixer | Moderate |
| V4 | 6AB4 | Heterodyne osc | Weak → low injection (see test point A, §4.8) |
| V5 | **6CB6** | LMO (inside LMO 110-40) | Manual: LMO was **calibrated with the supplied tube**; replace with same type *and brand* or expect a small cal shift |
| V6, V7 | 6BA6 | 1st/2nd IF | Weak → low gain, S-meter won't zero |
| V8 | 6AU6 | 100 kHz calibrator | Low |
| V9 | 6AS11 (12-pin Compactron) | Product det / BFO / BFO amp | Known failure; scarce; most testers can't test it |
| V10 | 6HF8 | 1st audio / audio output | Heater-cathode leakage → hum; hottest tube |

*Correction from Rev. 1:* that draft listed V5 as 6BZ6, from the AF6C article. This manual specifies the **6CB6**, and some production units differ. Fit whatever type your LMO is labeled for.

## 2.3 Power supply (manual p. 91, schematic)

- T1 power transformer (54-146-24). Separate 6.3 VAC filament/pilot winding.
- **D6, D7** silicon (1N2079, Heath 57-27): full-wave B+.
- **C233** 4-section can, 100-40-40-40 µF (Heath **25-163**). Its sections are separated by **R216 100 Ω 2 W**, **R217 330 Ω 2 W** and **R218 470 Ω**.
- B+ is about **148–160 V** (Fig. 5-3). The LMO gets about **142 V**.
- **D8** (1N2079) half-wave makes the negative bias of about **−60 to −65 V**. Its parts are **R207 3.3 kΩ 1 W**, **R208 10 kΩ 2 W**, **R209 12 kΩ**, and filters **C234/C235 10 µF**.
- The RF Gain control (10 kΩ) sets the −1 to −20 V gain bias.
- Line bypass: **C229, C231** 0.005 µF 1.4–1.6 kV discs.

# 3. What fails, ranked

Rankings combine the manual's circuit knowledge with field reports from the Heath list and Heathkit-Radios.

## 3.1 Capacitors

**Complete electrolytic inventory (Parts List #3/#4):**

| Ref | Value | Location / role | Replace with |
|---|---|---|---|
| C233 A–D | 100-40-40-40 µF (25-163) | B+ filter can | New can (Hayseed Hamfest) or restuff/discrete, **≥250 V** |
| C234, C235 | 10 µF 150 V (25-147) | **Negative bias** filters (D8 supply) | 10 µF 250 V. **Positive lead to chassis/ground side** — reversed vs. B+ |
| C237 | 10 µF 150 V (25-147) | Chassis, per schematic | 10 µF 250 V; observe schematic polarity |
| C238 | 10 µF 15 V (25-54) | Low-voltage bypass (chassis) | 10 µF 50 V |

*Correction from Rev. 1:* there are **no 50 µF cathode bypass caps** in this receiver. The electrolytics are exactly those listed above.

**Other capacitors:**

| Part | Likelihood | Symptom | Action |
|---|---|---|---|
| C233 can | **Very high** | Hum, low B+, hot can; can cook R216/R217 | Replace. Resistance at can lugs should rise to ≥ 20 kΩ within 10 s (Fig. 1-1). |
| C234/C235/C237/C238 | **Very high** | Wrong bias → gain/AGC/mute problems; hum | Replace all. |
| C229, C231 line bypass (.005 µF 1.4 kV) | High (safety) | Fail short across line | Replace with X1/Y2 safety caps. |
| Silver micas at V9 (BFO / product detector) | Medium | Weak BFO, rough SSB | Isolate and test; one restorer found all four out of 5%. |
| 1 pF phenolic (IF board, 28-2) and 2.2 pF phenolic (RF board, 28-1) | Medium | Open, or drifted (2.2 pF measured 5 pF) | Replace with C0G. |
| .2 µF Mylar/resin (27-34: IF board and C236/AGC) | Low–medium | Leakage → AGC/S-meter drift | Leakage-test at voltage; replace if any. |
| Ceramic discs | Low–medium | Bypass failure | Spot-test; full replacement optional. |
| Micas | Low | — | Leave unless out of tolerance. |

## 3.2 Resistors

The resistors are ~55-year-old carbon composition and drift **high**. One restorer found only 1 of the IF-board resistors within 5%.

| Ref / location | Why it matters (manual cross-ref) |
|---|---|
| **R216 100 Ω 2 W, R217 330 Ω 2 W, R218 470 Ω** | B+ dropping between can sections; scorch when C233 leaks. One list member found R217 lifted by a prior owner. |
| **R207 3.3 kΩ 1 W, R208 10 kΩ 2 W, R209 12 kΩ** | Bias supply; drift shifts mute, RF-gain range and AGC threshold. |
| **R112 4.7 kΩ, R206 3.6 MΩ, R212 470 Ω** | AGC time constants (with C113 fast / C228 slow). |
| **R103 100 Ω, R104 33 kΩ, R108 68 Ω, R109** + S-meter adjust (200 Ω, 10-61) | S-meter network. Replacing an out-of-spec R104 revived one dead meter. Troubleshooting chart: "S-meter does not zero" → V6/V7 tube, B+ at V6 pins 5/6, **open V7 cathode resistor**. |
| Cathode resistors **R2** (V1), **R5** (V8), **R15** (V2), **R21/R12** (mixers), **R115** (V10) | Named in the troubleshooting chart as "open cathode resistor" causes. |
| High-value plate/screen loads (≥ 100 kΩ) | Drift most; cut gain. |
| AM detector network (R113 47 kΩ, R114 330 kΩ) | Distorted AM. |
| Resistors inside the LMO | Leave unless the LMO misbehaves (§4.6). |

Method: lift one lead, measure, replace anything > 10% out. Carbon comp/film in RF and oscillator stages; metal film is fine in audio, power and DC networks.

## 3.3 Diodes (corrected per manual)

| Ref | Factory type | Heath p/n | Function | Notes |
|---|---|---|---|---|
| **D1, D2** | S-187 silicon | 56-28 | ANL clipper | Low failure. Troubleshooting: if installed backwards, AGC goes dead. |
| **D3, D4** | 1N458 silicon (specs page says 1N548) | 56-24 | **AGC detector** | Medium failure. Replace with a **small-signal** silicon diode (1N4148/1N914 class), **never a power rectifier** (1N400x). Rectifier reverse-recovery made one set's AGC act "backwards." |
| **D5** | 1N191 germanium | 56-26 | AM detector | Sub 1N34A / 1N270. Fragile leads. |
| **D6, D7** | 1N2079 silicon | 57-27 | B+ full-wave | Low; 1N4007 if leaky. |
| **D8** | 1N2079 silicon | 57-27 | −60 V bias | Low; 1N4007. |
| LMO shift diode | (inside LMO) | — | USB/LSB shift | Suspect only if the FREQUENCY SHIFT adjustment can't null (§4.8). |

*Correction from Rev. 1:* the earlier draft called the AGC diodes germanium. Per the parts list and specifications they are **silicon signal diodes**. The circuit description's "D3, the AM detector diode" conflicts with the schematic, which labels the AM detector **D5**. Trust the schematic.

## 3.4 Tubes, by risk

1. **6AS11** (V9): partial failure is the classic symptom. Buy a spare.
2. **6HF8** (V10): hum and leakage; runs hottest.
3. **6BZ6** (V1): gas shows as a positive AGC voltage.
4. **6BA6** (V6/V7) and **6AB4** (V4): emission loss; low test-point-A voltage on high bands.
5. **6CB6** (V5): rarely fails. Changing brand can shift dial calibration slightly (manual p. 77).

List-reported substitutions are 6GM6 for V1 and 6AH6 for the 2nd IF, with mixed results. Try them only after the set meets the stock benchmarks in §4.8.

## 3.5 Mechanical and connections

The manual (p. 77) says ~90% of returned kits failed from poor connections or solder joints. K9STH says the same about loose chassis hardware.

| Item | Symptom | Fix |
|---|---|---|
| Board and chassis ground hardware | Hum, intermittents | Loosen, clean and retighten every screw/nut through the chassis. The RF board foil edge was sanded for chassis contact during assembly (Detail 3-10S); clean it again. |
| LMO worm/gear grease | Stiff, warbly tuning; better when warm | Clean and relube (§4.6). |
| LMO rotor ground wiper | Jumpy tuning | Clean, or add a braid jumper from rotor shaft to frame. |
| Dial plate / spiral pawl | Binding, rubbing | Manual p. 59: loosen the hub setscrew and move the dial *slightly* toward the shaft end. |
| Drive-shaft bushing (455-42) and friction pulley | Tight or slipping tuning | Clean and lube the bushing; check the pulley engages the dial drive ring. |
| Band, Mode, Function, AGC, Converter wafers; AF/RF pots | Dead bands, crackle | DeoxIT D5 and exercise. The chart lists reversed rotor/wafer faults; note orientation before removing anything. |
| Preselector **insulated coupling** (456-4) | Cracked; preselector slips | Replace (Delrin couplings available). |
| Tube socket contacts | Intermittent stage | Re-tension. |
| Pilot lamps | Overload of the 6.3 V winding | **#47 only** (0.15 A). |

# 4. Restoration plan

## 4.1 Phase 0: Assess cold

- Photograph top, bottom and rear. Note mods such as caps on SPARE jacks, lifted leads or non-stock tubes.
- Label and pull the tubes and crystals. Compare against §2.2 and the crystal list (§5.3).
- Inspect C233 for bulging, the 2 W resistors for scorching, T1 for tar or smell, and the coax and harness.
- **Fuse:** confirm a 2 A slow-blow. A wrong fuse let one set smoke its power section.
- Do the **manual's resistance check (p. 65, Fig. 1-1)** before applying power:
  - Settings: FUNCTION OFF, AGC OFF, MODE LSB, AF GAIN and PRESELECTOR fully CCW, BAND 3.5, CONVERTER VHF 1, RF GAIN fully CCW.
  - Disconnect the yellow transformer lead at terminal strip N.
  - Pull the LMO tube.
  - Readings must be within ±20% (table below).

| Point (Fig. 1-1) | Expected |
|---|---|
| C233 ("capacitor L") lugs | **≥ 20 kΩ after 10 s** (charging) |
| Terminal strip N lug 1 | ∞ |
| MUTE jack BE | OFF 15 k, STBY 15 k, OPR 0, CAL 0 |
| ANTI-VOX BG | ≈ 40 Ω |
| SPKR BH | ≈ 1.4 Ω |
| HET OSC jack | 0 Ω |
| LMO, BFO jacks | ∞ |
| AC input pins | ∞ to chassis |
| Antenna jacks BA/BC/BD vs CONVERTER switch | 0 on the selected input, ∞ otherwise |
| Accessory octal BR | pins per figure (20 k, 0, ∞; AGC pin ≈ 5.6 MΩ with AGC OFF) |

Fig. 5-2 gives a full tube-socket resistance map (power off, tubes in, cord unplugged) for deeper checks.

## 4.2 Phase 1: Clean

- Chassis: dry brush and vacuum, then mild cleaner on swabs. **Keep solvents off the ink-stamped chassis and coil-cover labels.**
- Front panel: remove the knobs (#4 and #8 Allen setscrews). Soap and water only.
- Boards: IPA to remove flux. Protect the IF can windings.
- Switches and pots: DeoxIT after cleaning.

## 4.3 Phase 2: Power supply first

1. Replace C233, rated ≥ 250 V.
2. Replace C234, C235, C237 and C238. **C234/C235 are in the negative bias supply**, so get the polarity right from the schematic.
3. Replace C229/C231 with X1/Y2.
4. Check R216, R217, R218, R207, R208 and R209. Replace any that are scorched or > 10% high.
5. Replace D6–D8 with 1N4007 if any test leaky (optional insurance).
6. Optional: fit a 3-wire grounded cord bonded to the chassis, and keep the 2 A slow-blow fuse.

## 4.4 Phase 3: Resistor survey

Work RF board → IF board → chassis. Prioritize §3.2's named parts and anything ≥ 100 kΩ.

## 4.5 Phase 4: Signal-path caps and diodes

- Replace the 1 pF and 2.2 pF phenolics with C0G.
- Test the V9 silver micas.
- D3/D4: replace only with small-signal silicon. D5: germanium only.
- Leakage-test the .2 µF Mylars.

## 4.6 Phase 5: LMO and dial

The manual says *never open the LMO* (warranty) and to keep the original-brand 6CB6. Restorers open them routinely, but only for mechanical service:

- The LMO comes out without removing the front panel: unsolder the leads, remove 4 nuts, and loosen the dial-collar nut.
- Remove only the gear-end plate. **Do not remove the side plate that carries the variable capacitor**, or calibration is lost.
- **Do not rotate the capacitor shaft while the stop-washer stack is loose.**
- Clean the hardened grease from the worm, split anti-backlash gear and stop washers, and relube with synthetic or moly grease. Keep the split gear's springs tensioned.
- Clean the rotor ground wiper, or add a braid jumper.
- Reinstall and redo the **dial mechanical setup (pp. 57–59):**
  - Push the circular dial on until the nylon spiral follower sits at the bottom of the first groove, then tighten the setscrew.
  - Turn from full CCW (90) to the first 0. The slide pointer should be at 0; if not, slide the pointer-drive-arm base **left/right** only.
  - Five turns should land the pointer on 5; if not, move the base **up/down** only. Iterate.
  - Full travel is 5 turns plus about 10 kHz, smooth, with no pawl rubbing.
  - The zero-set dial must clear the plastic window. Bend the bracket slightly if needed.

## 4.7 Phase 6: First power-up

- Use a variac with an isolation transformer, or a dim-bulb tester. Bring it up slowly while watching C233 and the 2 W resistors.
- **Connect a speaker whenever the set is on** (manual p. 67).
- Set FUNCTION to OPR. The S-meter pins full scale until the tubes warm. Then set the **S-METER ADJ** (top of chassis) for zero with the antenna off and RF GAIN fully CW.
- Reference draw from one restored unit at 124 VAC: ~0.5 A OPR, ~0.4 A STBY. That is consistent with the 50 W spec.
- Check voltages against **Fig. 5-3** using the controls listed on that figure: AGC OFF, MODE USB, BAND 3.5, RF GAIN full CW, AF GAIN full CW and pushed in, PRESELECTOR peaked, CONVERTER HF.
  - B+ ≈ 148 V (RF/IF boards), ≈ 160 V at V10, ≈ 142 V at LMO B+.
  - Bias ≈ −60 V.
  - The V9 inset gives per-mode pin voltages; use it for BFO/product detector faults.
- AGC line: ≈ −0.7 V with no signal (field reference). **Any positive AGC voltage means a gassy tube on the AGC line:** swap V1, V6, V7 one at a time.

## 4.8 Phase 7: Alignment (manual pp. 67–71)

Use a 30+ minute warm-up (spec stability is after 20 min). Use only the plastic tool. **Never touch L21** (BFO output coil, factory set).

1. **Crystal calibrator.** FUNCTION CAL, AF GAIN fully CCW. Feed the SB-301 antenna into another receiver tuned to WWV (2.5/5/10/15 MHz) or a broadcast station on a 100 kHz multiple. Adjust **trimmer C (C5, 8–50 pF, RF board)** for zero beat.
2. **Heterodyne oscillator.** FUNCTION OPR. 11 MΩ VTVM, −DC 5 V scale, from chassis to **test point A** on the RF board. Peak each HET OSC coil (marked on the coil cover) on the **slow-rising side** of the peak. The fast-dropping side is wrong.

| Band | 3.5 | 7.0 | 14.0 | 15.0 | 21.0 | 28.0 | 28.5 | 29.0 | 29.5 |
|---|---|---|---|---|---|---|---|---|---|
| TP-A (−V DC) | 2.8 | 2.7 | 2.8 | 2.9 | 2.8 | 2.4 | 2.5 | 2.4 | 2.7 |

3. **IF (T3, T4).** Calibrator method: BAND 3.5, MODE LSB, AGC FAST, RF GAIN full CW, AF 3 o'clock, FUNCTION CAL. Tune to one side of zero beat for the maximum S-meter reading, then peak T3 and T4. Generator method: 3.395 MHz unmodulated, 1 mV through .01/.001 µF to V6 pin 1, then peak T3/T4 alternately.
4. **Antenna and RF plate coils.** Set the PRESELECTOR per **Fig. 2-2** for each band. Peak in this order: 3.5 ant → 3.5 RF (then **re-peak T3/T4**) → 7.0 → 14.0 → 21.0 → 29.0 MHz (adjust the "28.0" coils). There are no adjustments on 15.0, 28.0, 28.5 or 29.5. Keep the signal centered in the filter (maximum S-meter).
5. **LMO shifter.** Tune to 3.8 MHz. FUNCTION CAL, MODE USB. Zero beat with Main Tuning and peak the preselector. Switch to LSB without touching the dial and adjust the **FREQUENCY SHIFT** screw on the LMO for exact zero beat. Recheck USB and repeat as needed.
6. **Dial calibration.** Zero beat at 3.8 MHz and center the zero-set mark. Remove the tuning knob, hold the LMO drive shaft with a screwdriver through the escutcheon hole, loosen the circular-dial setscrew, set **0** under the zero-set mark and retighten. Check the spiral pawl engagement and refit the knob.
7. **Touch-up.** Re-peak the HET OSC coils for maximum S-meter, slow side. On 15 MHz, re-zero the calibrator trimmer C against WWV.

**Sensitivity benchmark (Fig. 5-3, RF voltages).** Signal needed for **0.5 W into 8 Ω** (≈ 2 V RMS across the speaker load), controls as for Fig. 5-3:

| Inject at | Frequency | Level |
|---|---|---|
| V9 pin 6 | 3395 kHz | 30 mV |
| V7 pin 1 | 3395 kHz | 17 mV |
| V6 pin 1 | 3395 kHz | 250 µV |
| V3 pin 1 | 8.5 MHz | 200 µV |
| V2 pin 1 | 3.5 MHz | 200 µV |
| V1 pin 1 | 3.5 MHz | 9 µV |
| HF ANT jack | 3.5 MHz | 1.3 µV |

Inject through .001 µF with 50 Ω to ground; the antenna jack is driven directly. Work backward from the speaker: the first stage that needs far more signal than listed is the bad one.

**Field benchmark (calibrator signal, healthy set):** 3.7 MHz S9+40, 7.2 S9+40, 14.2 S9+30, 21.2 S9+20, 28.2 ≈ S7.

## 4.9 Phase 8: Optional mods (reversible)

- **AM audio:** 470 kΩ 1/2 W across the AM detector diode (D5 on this schematic; Heath *News and Views*).
- **Softer audio:** C243 and C256 from .001 to .005 µF.
- **Transceive stability with SB-401:** regulate the HET OSC and LMO B+.
- **Attenuator:** reuse the CONVERTER switch as 0/−10/−20 dB.

# 5. Operation and station notes (from the manual)

## 5.1 Operating tips

- Zero-set routine: zero beat the calibrator at the nearest 100 kHz point, set the zero-set knob, then switch to OPR. This corrects het-crystal tolerance.
- SSB: RF GAIN full CW, AGC SLOW, AF GAIN about 10 o'clock.
- **Do not run AF GAIN wide open and ride volume with RF GAIN.** It degrades signal-to-noise (p. 76).
- CW with the 400 Hz filter: find the signal in USB at a 1000 Hz note, then switch to CW. Zero beat is inaudible in CW.
- Weak signals: AGC OFF or FAST may beat SLOW.
- ANL: pull the AF GAIN knob. Use it only on weak signals; it distorts strong ones.

## 5.2 With the SB-401

- MUTE: an open ground mutes V1, V2, V6, V7 and V10B. With the FUNCTION switch in **STBY**, the transmitter's VOX relay grounds the mute line to receive. In OPR the receiver grounds it itself, which gives hot monitor audio during transmit. **Leave the SB-301 in STBY.**
- Make the LMO, BFO and HET OSC transceive cables **exactly 24 in. of RG-62/U** (p. 73). Copy originals exactly if you rebuild them.
- Interconnect per **Fig. 4-1**.

## 5.3 Crystals (Parts List #5)

| Use | Frequencies (MHz unless noted) |
|---|---|
| Calibrator | 100 kHz |
| BFO | 3392.110 kHz (RTTY, Y10), 3393.6 kHz (LSB, Y11), 3396.4 kHz (USB/CW/AM, Y12) |
| Heterodyne | 12.395, 15.895, 22.895, 23.895, 29.895, 36.895, 37.395, 37.895, 38.395 |

The 15.895 MHz (40 m) crystal is shared across HW-100/101, SB-100/101/102, SB-300/301 and SB-400/401.

# 6. Tips and tricks

- Mark each tube's socket before pulling it.
- Bag removed parts per board.
- Use a desoldering station; chassis lugs need a chisel tip.
- Re-solder every board-to-chassis ground tab.
- Keep the original 6CB6 with the LMO.
- Before removing any rotary-switch wafer, photograph its rotor orientation. Reversed rotors appear repeatedly in the troubleshooting chart.
- Spares worth stocking: 6AS11, 6HF8, #47 lamps, 1N4148s, 1N34A, a 2 A slow-blow fuse.

# 7. Maintenance schedule

| Interval | Task |
|---|---|
| Each session | 20–30 min warm-up before critical tuning; zero-set with the calibrator. |
| Every 6 months | Exercise every switch and pot through full travel. |
| Yearly | Vacuum; calibrator S-meter benchmark; check S-meter zero; listen for hum growth. |
| Every 2–3 years | Retighten chassis hardware; DeoxIT switches; check B+, bias and AGC voltages vs. Fig. 5-3. |
| Every 5 years | Test tubes (6AS11, 6HF8 first); relube the dial bushing; HET OSC TP-A check and touch-up alignment. |
| ~15–20 years | Re-check electrolytics. |

Store dry and at stable temperature with the cover on. Power up a few times a year.

# 8. Parts sources

- **Hayseed Hamfest (N0JMY):** SB-301 recap kit, direct-replacement C233 can.
- **Mouser / Digi-Key:** electrolytics, resistors, X1/Y2 caps, C0G, silver mica, 1N4148, 1N4007.
- **Nebraska Surplus Sales:** small molded caps, germanium diodes (1N270).
- **eBay (Mahoney's Radio):** SB-301 panel label kits.
- **Heathkit-Radios (groups.io):** donor parts, LMOs, crystals, insulated couplings.

# 9. Rev. 2 change log (manual review)

| Item | Rev. 1 | Rev. 2 (per manual) |
|---|---|---|
| LMO tube V5 | 6BZ6 | **6CB6**; replace with same brand |
| AGC diodes D3/D4 | Germanium (1N34) | **Silicon signal** (1N458/1N548) → sub 1N4148, never rectifiers |
| AM detector | Called D3 | **D5** (1N191 germanium) |
| Electrolytics | Included "50 µF cathode bypasses" | Exactly C233 can + C234/C235/C237 (10 µF 150 V) + C238 (10 µF 15 V) |
| Power resistors | 100 Ω and 330 Ω 2 W | Added R218 470 Ω, R207 3.3 k 1 W, R208 10 k 2 W, R209 12 k |
| Fuse / lamps / power | Unverified | 2 A slow-blow; #47; 50 W |
| Pre-power test | Generic | Manual Fig. 1-1 resistance table |
| Alignment | Summary | Full sequence, TP-A voltages, LMO shifter, dial cal, L21 warning |
| Benchmarks | Forum S-meter only | Added manual stage-gain table (Fig. 5-3) |
| Specs | — | Added factory specifications |

# 10. References

- Heath Co., *Assembly and Operation of the Heathkit SSB Receiver Model SB-301*, 595-946-01 (1966/1968). Scan via W5RKL.
- Eckweiler AF6C, "Heathkit of the Month #36: SB-301," w6ze.org.
- Heathkit-Interests blog, SB-301 restoration log (2019–2022).
- Heath mailing list archive (puck.nether.net/pipermail/heath): "SB-301/SB-401 Functional Repair Guidelines" (Oct 2010); "SB-301 Problems" (Mar 1998); S-meter threads (Mar 2003, Mar 2009); "SB-301 Mods/Updates" (Nov 2004); filter-can thread (Feb 2005); LMO grease threads (2002, 2016, 2021).
- Heathkit-Radios and heathkit groups on groups.io: SB-301/401 operation and LMO threads.
