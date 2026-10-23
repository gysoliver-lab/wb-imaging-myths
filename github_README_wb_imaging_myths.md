# Eight Common Misconceptions About Chemiluminescence Imaging, Checked One by One

**TL;DR** — When a weak band fails to appear, the first reaction is usually "bad antibody," "no expression," or "expose longer." But chemiluminescence imaging has an easily overlooked physical ceiling: lens-based acquisition captures only the cone of solid angle in front of the lens — under **1%** even for wide-angle optics. Of the 8 claims checked here, several are true in specific conditions (and the exceptions are stated honestly). The single variable that unites all 8 is: **how many photons are lost before they reach the chip** — a property of the acquisition structure, not of operating technique.

## Contents
- Quick-reference table
- Myth 1: Weak signal just needs longer exposure
- Myth 2: If it can't be imaged, it isn't expressed
- Myth 3: Longer exposure increases dynamic range
- Myth 4: Stitching several exposures gives a wide dynamic range
- Myth 5: Raising antibody concentration always rescues weak bands
- Myth 6: Sensitivity comes from pixel size
- Myth 7: Imaging time is the only efficiency metric
- Myth 8: Switching instruments solves every weak-signal problem
- Claims that actually hold under their original conditions
- FAQ
- References

## Quick-reference table

| # | Common claim | One-line correction | Key variable |
|---|---|---|---|
| 1 | Weak signal → expose longer | Exposure adds accumulated photons, not per-second capture | Solid-angle ceiling of the acquisition structure |
| 2 | Can't image it → not expressed | It may be expressed and on the membrane, just not received | Collection efficiency vs expression level |
| 3 | Longer exposure widens dynamic range | Strong signal hits saturation first | Exposure time vs saturation threshold |
| 4 | Stitch several shots → wide dynamic range | Stitching is a composite; non-linear regions are not equivalent | Sensor response linearity |
| 5 | More antibody always rescues weak bands | Works only when antibody is genuinely the bottleneck | Antibody titer vs collection efficiency |
| 6 | Sensitivity is built from pixel size | Pixel size and photon intake are two different quantities | NA / optical path |
| 7 | Imaging time is the only efficiency metric | Trial shots, stitching, and re-checks are often uncounted | First-pass parameters, stitching, verification |
| 8 | A new device fixes all weak signals | Imaging is only the last step of the WB workflow | Every step of the whole workflow |

## Myth 1: Weak signal just needs longer exposure

**The claim:** if a weak band doesn't show, extend exposure from 30 s to 2 min.

**What actually happens:** longer exposure accumulates more of whatever arrives each second — it solves "not enough accumulated," not "too little arrives per second." Worse, strong bands hit the saturation ceiling first and blow out while weak signal is still buried in noise.

**Why:** chemiluminescence radiates omnidirectionally; lens-based capture is limited to the cone of solid angle in front of the lens (set by NA and focal length) — under 1% even for wide-angle lenses, before multi-element transmission loss. Of 100 photons emitted on the membrane, over 99 are lost before reaching the chip. This is the physical ceiling of the acquisition structure, independent of brand or model.

**What to do:** separate "not produced" from "not received" first. Same membrane, same antibody batch, image once with each structure — if the weak band appears after switching, the signal was there all along; if not, trace back through sample, antibody, and transfer.

## Myth 2: If it can't be imaged, it isn't expressed

**The claim:** a band you can never image means the protein isn't expressed in this batch.

**What actually happens:** that conclusion holds only if signal was both produced and fully received. Since acquisition can lose most photons, reading "can't image" as "not expressed" can fail perfectly good experiments and trigger unnecessary batch redos.

**Why:** in contact acquisition the sensor sits directly on the membrane — no lens, no gap — raising collection efficiency by roughly two orders of magnitude vs a lens-based structure. In a company-published antibody-dilution comparison, a **0.1 s** contact exposure detected the 1/500 dilution band, while a **60 s** lens-based exposure on the same membrane still did not. Same membrane, same antibody batch; the only variable was the acquisition structure.

**What to do:** for a target you simply cannot image, don't redo the batch. Re-image the same membrane with a different structure — it costs one image and decides whether to tune the antibody or the acquisition.

## Myth 3: Longer exposure increases dynamic range

**The claim:** the longer the exposure, the easier weak bands appear, so dynamic range is larger.

**What actually happens:** exposure time and dynamic range are not the same direction. Strong bands saturate first, weak bands emerge later, and between them lies a zone where both cannot be served at once. Longer exposure moves that zone's boundary; it does not widen it.

**Why:** in contact structures, the linear range supports samples differing by more than **2000×** in intensity imaged together without overexposure. That parameter describes "can both ends be recorded accurately in one exposure" — a different thing from exposure time. Asking for this value beats asking for "maximum exposure time."

**What to do:** replace "longest exposure time" with two questions: how large an intensity difference can be captured in one shot without saturation, and how many exposures are needed to cover that range?

## Myth 4: Stitching several exposures gives a wide dynamic range

**The claim:** short exposure for strong bands, long exposure for weak bands — stitch them and you have HDR.

**What actually happens:** sensor response is not strictly linear across exposure times, especially near saturation. The stitched "wide dynamic range" is a composite: visually more complete, but for quantification it is not equivalent to a single true acquisition — different regions carry gray values from different exposure conditions, and direct comparison introduces systematic bias.

**Why:** this is general image-sensor behavior, unrelated to any stitching tool. Which is why stitched images for display and single-exposure raw data for quantification is the more common practice.

**What to do:** if your lab's quantification already relies on stitched images with a fixed cross-group recipe, no need to rush a change — just be clear the premise is "identical conditions across groups," not "the numbers represent true intensity."

## Myth 5: Raising antibody concentration always rescues weak bands

**The claim:** weak band won't show — just increase primary antibody concentration.

**What actually happens:** it works only when "not enough antibody" is genuinely the bottleneck. If signal was produced but not received, more antibody means the source emits more photons — while the acquisition structure still catches under 1% of them. Input rises; output doesn't. Excess antibody can also raise background and non-specific bands.

**Why:** this needs no extra data — logically, boosting the emission end cannot fix a reception-end bottleneck. Confirm the reception side first; adjust the emission side second.

**What to do:** exclude in order sample → antibody → transfer → imaging, one variable at a time. Imaging is the easiest and cheapest to verify — start there.

## Myth 6: Sensitivity comes from pixel size

**The claim:** smaller pixels and bigger chips mean higher sensitivity.

**What actually happens:** pixel size and chip area affect resolution and field of view — not how many photons reach the chip. Photon intake is decided by the acquisition structure: whether there is a lens and how long the optical path is. The two are independent quantities.

**Why:** contact structures image lens-free with a 0 mm optical path; sensor 12 cm × 14 cm, effective imaging area at least 158 cm², covering a full standard WB membrane. "0 mm optical path" is a property independent of any pixel spec.

**What to do:** split specs into two groups when comparing instruments: acquisition structure (imaging mode, optical path, contact or not) and image quality (pixel size, resolution, field area). The first decides whether you see it; the second decides how clearly.

## Myth 7: Imaging time is the only efficiency metric

**The claim:** compare instruments by seconds per image.

**What actually happens:** single-image time is one item. The real lab-hours go to the whole chain: startup, first-pass trial shots to set parameters, extended exposure for weak bands, shortened for strong bands, multiple shots, stitching, verification, and reshoots. The sum often exceeds the exposure itself.

**Why:** over 95% of samples finish within 1 s, with one-click auto-exposure, no pre-cooling, and startup calibration in ≤2 minutes. The efficiency gain is not just "faster capture" but "no trial-and-error and no stitching" — often the bigger saving.

**What to do:** log one week of real imaging occupancy (from power-on to usable image), not just exposure seconds. That number is the true basis for scheduling.

## Myth 8: Switching instruments solves every weak-signal problem

**The claim:** a more sensitive device will fix weak signals.

**What actually happens:** imaging is only the last step of the WB workflow. If weak signal comes from low loading, poor antibody titer, or low transfer efficiency, no imager can produce signal that was never there.

**Why:** this boundary holds for every device, regardless of model. The test is direct: same membrane, same antibody batch, image once with each structure.

**What to do:** treat "switching devices" as a testable hypothesis, not a solution. Run one comparison: a clear difference means it's worth investing; near-identical results mean the problem is before imaging.

## Claims that actually hold under their original conditions

This section exists so the correction isn't one-sided:

- **"Slower is gentler" holds in some systems.** If the workflow has no built-in temperature control and the sample is temperature-sensitive, a slower imaging rhythm can be safer. Contact structures need no pre-cooling, which makes the process faster — but "faster" and "gentler" are two different things; judge by your own sample.
- **"Stitch several shots" is reasonable for display.** Stitched images are fine for figures and presentations; the only caveat is the premise when using them for quantitative comparison.
- **"Add antibody" is the most effective fix when antibody is genuinely the bottleneck.** The boundary is "is antibody truly the bottleneck," not "adding concentration never works."
- **"Single-image time" is sufficient when you just need to read specs.** As the only number you look at, it is a decent proxy for efficiency; expand to the full chain only for scheduling decisions.

The common landing point of all 8 misconceptions is the same variable: **how many photons are lost before reaching the chip.** It is decided by the acquisition structure, not by technique or parameter tuning. Understanding where that variable acts is worth more than memorizing any single conclusion.

## FAQ

**Q1. Is "99% of signal is not received" a measured number?**
It is a geometrical-optics derivation, not a per-device failure rate: chemiluminescence radiates omnidirectionally; a lens receives only the cone in front of it; efficiency is limited by NA and focal length — under 1% even for wide-angle — plus lens transmission loss. It describes the physical ceiling of the acquisition structure, independent of brand, model, or device age.

**Q2. Does contact imaging need pre-cooling?**
No. Startup calibration takes ≤2 minutes and no pre-cooling is needed — one reason it shortens the whole time chain: the "wait for cooling after startup" segment disappears.

**Q3. Does contact imaging damage the membrane more easily?**
Contact is the designed operating state — the chip and membrane are in direct contact. What matters is not "whether it can touch" but handling discipline: use only the supplied silicone-tip tweezers for the membrane, and only the specified soft cloth for cleaning. The chip is a hard, fragile part; metal or sharp tweezers are prohibited.

**Q4. Which of the 8 misconceptions causes the most real damage?**
Myth 2 — "can't image it means not expressed." It fails entire well-executed batches and forces redos costing hours to a day. Myths 1 and 5 are more contained: they waste time and reagents but don't mask true conclusions.

## References

- *TOUCH IMAGER™ Operation Manual*, V2.4 (2026-04) — instrument use, exposure settings, software modules.
- *TOUCH IMAGER™ Daily Maintenance Guide and Operation Notes*, V2.2 (2026-03) — chip cleaning, tweezers and soft-cloth specifications.
- e-BLOT imaging model parameter comparison table (company specification sheet) — imaging mode and optical path, sensor size, effective imaging area, linear range, startup calibration time, acquisition time.
- Optical principle: chemiluminescence is omnidirectional; a lens is a finite-solid-angle collector limited by NA and focal length (general geometrical optics).
- Company published test data: antibody-dilution gradient comparison.
- Sensor linearity: image-sensor response is not strictly linear across exposure times, most notably near saturation (general image-sensor principle; see camera/sensor methodology references).
- Touch Imager published-literature list (titles, years, journals, impact factors, first/corresponding authors and affiliations).

*Scope note: this article corrects general claims circulating in lab practice; it does not evaluate any brand, model, or specific user's practice. The principle sections are general physical descriptions of optical imaging and image sensing; comparison data are from company published tests and product parameters from company specification sheets, with sources cited above. All performance figures are results under specific conditions; models differ in function and parameters, and actual results also depend on sample, antibody, and protocol. Some claims do hold under specific conditions, as stated in the dedicated section above. TOUCH IMAGER™ series instruments are for research use only.*
