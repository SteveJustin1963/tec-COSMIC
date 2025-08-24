# TEC-1 cosmic ray detector

# Table of Contents

- [TEC-1 cosmic ray detector](#tec-1-cosmic-ray-detector)
  - [Using basic cosmic ray detector circuit](#using-basic-cosmic-ray-detector-circuit)
- [Muons created by cosmic rays](#muons-created-by-cosmic-rays)
  - [Step 1. What is a muon?](#step-1-what-is-a-muon)
  - [Step 2. Problem without relativity](#step-2-problem-without-relativity)
  - [Step 3. Relativity saves the day](#step-3-relativity-saves-the-day)
  - [Step 4. Evidence](#step-4-evidence)
- [Build a small cosmic-ray muon detector](#build-a-small-cosmic-ray-muon-detector)
  - [Three workable DIY paths](#three-workable-diy-paths)
    - [Plastic scintillator + SiPM (CosmicWatch)](#plastic-scintillator--sipm-cosmicwatch)
    - [Two GM tubes in coincidence (muon telescope)](#two-gm-tubes-in-coincidence-muon-telescope)
    - [Diffusion cloud chamber](#diffusion-cloud-chamber)
  - [Minimal shopping lists](#minimal-shopping-lists)
    - [Scintillator route](#scintillator-route)
    - [GM-coincidence route](#gm-coincidence-route)
    - [Cloud chamber route](#cloud-chamber-route)
  - [Quick Arduino coincidence sketch](#quick-arduino-coincidence-sketch)
  - [What data you can actually get](#what-data-you-can-actually-get)
  - [Bottom line](#bottom-line)



Cosmic-ray observatories are designed to detect and study high-energy particles that originate from outside of the Earth's atmosphere. These particles, known as cosmic rays, can include a wide range of particles such as photons, electrons, protons, and nuclei of heavier elements, as well as antimatter particles. They are typically detected using a variety of instruments such as particle detectors, telescopes, and radio antennas. The data collected by these observatories can be used to study a wide range of phenomena in astrophysics and particle physics, including the properties of the sources of cosmic rays, the nature of the interstellar medium, and the properties of the particles themselves.

## using http://cosmicray.com.au/basic-cosmic-ray-detector-circuit

- The circuit design is a low- cost reliable cosmic ray (muon) detector using Geiger–Müller Tubes which gives an output of a 5V TTL pulse, each time a cosmic ray (muon) is detected.
- It can be easily adapted for use with counters, Arduino, Raspberry Pi, sound cards, and other data loggers and the tec-1
- For best results, use GMTs with an all- metal- jacket designed for detecting gamma rays which reduces false detections from lower energy terrestrial sources.
- Use correct Geiger plateau voltage, series resistor, and coupling capacitor as per GMT manufacturers’ specifications for longer life and stability.
- The output of the Geiger–Müller tube (GMT) is a negative sawtooth pulse.
- The input of the 74HC14 Schmitt Trigger is biased at 5V through a 100k ohm resistor holding the input “high” and the output “low”.
- To filter local terrestrial radiation at least two GMT are required placed one above the other to monitor coincidence between the two GMT.
- The longer the pulse from each of the GMT, the higher the probability of a false coincidence detections coming from local terrestrial radiation.
- Shortening the pulse width will reduce false coincidence detections.
- Coincidence detection between the two GMT is achieved using a 74HC02 NOR gate where if the output of each GMT pulse shorting circuit enters.
- The power supply used should be an adjustable, ensuring the GMT is set to the correct plateau voltage, regulated to ensure a constant count rate over time and low noise to reduce any potential interference with the electronics.
- A very basic detector could just ignore the pulse shortening if a detector is only needed for display purposes.
- Further simplification can be achieved using a voltage summing amplifier, where the summed voltage of more than one GMT output pulse is a coincidence.

# Muons created by cosmic rays survive to reach Earth’s surface only because relativity slows their decay clock.

Got it. Let’s break down the **muon example** clearly:

---

### Step 1. What is a muon?

A muon is a particle, like a heavy electron, created when cosmic rays hit the upper atmosphere.
It’s unstable — lifetime = about **2.2 microseconds** (2.2 millionths of a second) when at rest.

---

### Step 2. Problem without relativity

If you multiply lifetime × speed, you get how far a muon should travel:

* Speed ≈ nearly the speed of light = 300,000 km/s.
* 2.2 microseconds × 300,000 km/s ≈ **660 meters**.

So if muons lived only 2.2 μs, they should die out after about 660 m.
But cosmic rays hit \~15 km (15,000 m) above Earth. Without help, almost **none** should reach the ground.

---

### Step 3. Relativity saves the day

At near-light speeds, time for the muon slows down relative to Earth (time dilation).
To us on Earth, its “decay clock” runs slower.

So instead of 2.2 μs, its effective lifetime becomes much longer — enough to survive the 15 km journey to the surface.

---

### Step 4. Evidence

Detectors at ground level (and even underground) **actually see muons** raining down.
This matches Einstein’s predictions perfectly.
If relativity weren’t true, there’d be no muons left to detect.

---

Two short instances:

* Muons from cosmic rays detected at sea level prove time dilation directly.
* Particle accelerators (like CERN) measure extended muon lifetimes at high speeds, confirming the same effect.

---

So the muon story is one of the **cleanest proofs** that relativity isn’t just theory — it’s happening in the atmosphere above your head right now.

Do you want me to also explain the *mathematical factor* (the Lorentz factor γ) that stretches muon lifetime so they can make it?

# Build a small **cosmic-ray muon detector** you can run at home.

Muon = a heavy, fast, unstable electron-like particle from cosmic rays; at sea level the flux is about **1 per cm² per minute**. That’s real, measured physics (not Kozyrev). ([Cosmic Connection][1], [HyperPhysics][2], [ScienceDirect][3])

Three workable DIY paths:

1. Easiest reliable: plastic-scintillator + SiPM (“CosmicWatch”)

* What it is: A plastic scintillator tile + a silicon photomultiplier (SiPM) + a tiny preamp/ADC board logs each muon hit, and two units can be put in **coincidence** to reject background. “Coincidence” = only count when both detectors fire within a tiny time window. ([GitHub][4])
* Why this works: Muons ionize the scintillator; light pulses are turned into electrical pulses by the SiPM; the firmware timestamps and stores hits. The open project documents the PCB, enclosure, firmware, and analysis scripts. ([GitHub][4])
* How to do it: Follow the CosmicWatch v3X docs (PCB + parts list + manual), assemble, power from USB, and optionally cable two units for coincidence mode to suppress gamma background. ([GitHub][4])

2. Cheapest parts-bin build: two GM tubes in coincidence (a “muon telescope”)

* What it is: Stack two Geiger-Müller tubes (e.g., SBM-20) \~2–3 cm apart, add a thin lead sheet between, and count **only** events where both tubes fire within \~1 ms using an Arduino/Nano. This rejects most local radioactivity and keeps mostly through-going muons. ([IEEE Spectrum][5])
* Why this works: Most terrestrial particles won’t traverse both tubes + lead; a relativistic muon will. An IEEE Spectrum hands-on build shows the geometry, code idea, and even a simple muon-tomography demo. ([IEEE Spectrum][5])
* How to do it (outline): 2× GM tube boards (with HV), 2× tubes (SBM-20 class), Arduino to time-stamp pulses, a coincidence window ≈1 ms, and vertical mounting. Expect to integrate for hours to get clean angular/attenuation plots. ([IEEE Spectrum][5])

3. Visual, classroom-friendly: a diffusion **cloud chamber**

* What it is: A cold, alcohol-supersaturated box where ionizing particles leave visible condensation tracks. Long, straight tracks are typically muons; short, fat tracks are alphas. ([CERN][6], [American Museum of Natural History][7])
* How to do it: Use dry ice or a Peltier plate and isopropanol per CERN/AMNH guides; observe tracks in a dark room with a flashlight. Not selective for muons, but you *will* see cosmic rays. ([CERN][6], [American Museum of Natural History][7])

Minimal, do-now shopping lists

A) Scintillator route (most robust data)

* PCB + parts per CosmicWatch v3X repo, 1× plastic scintillator tile, 1× SiPM, micro-USB power, optional 2nd unit for coincidence. Logs to microSD/USB; includes analysis scripts. ([GitHub][4])

B) GM-coincidence route (cheapest)

* 2× GM tube kits + 2× tubes (e.g., SBM-20), 1× Arduino Nano, small lead sheet, spacers \~25 mm, wiring for two digital pulse inputs; code counts only if |t1–t2| < 1 ms. The Spectrum build explains the geometry and coincidence method. ([IEEE Spectrum][5])

C) Cloud chamber route (demo)

* Clear container, black base, felt wick, 99% isopropanol, dry ice/Peltier, torch, and patience; follow CERN/QuarkNet how-tos. ([CERN][6], [quarknet.fnal.gov][8])

Quick Arduino coincidence sketch (GM route)

```
volatile unsigned long tA, tB;
volatile bool hitA=false, hitB=false, coinc=false;

void isrA(){ tA=micros(); hitA=true; }
void isrB(){ tB=micros(); hitB=true; }

void setup(){
  attachInterrupt(digitalPinToInterrupt(2), isrA, RISING);
  attachInterrupt(digitalPinToInterrupt(3), isrB, RISING);
  Serial.begin(115200);
}
void loop(){
  noInterrupts();
  bool a=hitA, b=hitB;
  unsigned long ta=tA, tb=tB;
  interrupts();
  if(a && b && (abs((long)(ta - tb)) <= 1000)){ // ~1 ms
    Serial.println("muon");
    noInterrupts(); hitA=hitB=false; interrupts();
    delay(10);
  }
}
```

(Adjust threshold and dead time to suit your tube electronics; Spectrum’s build used \~1 ms and \~25 mm spacing.) ([IEEE Spectrum][5])

What data you can actually get

* Count rate vs. angle: rotate the stack; muon flux falls roughly like cos²(θ); the DIY Spectrum build reproduced this with long integrations. ([IEEE Spectrum][5])
* Attenuation/shielding: compare outdoors vs. under concrete or underground; rates drop with overburden. (QuarkNet docs and many school labs do this.) ([QuarkNet][9], [studylib.net][10])

Two small instances

* A 5 × 5 cm scintillator tile should record steady single-hit rates and, in coincidence with a twin tile above it, give a clean through-going muon sample suitable for angle scans. ([GitHub][4])
* A two-tube GM stack with \~25 mm separation and \~1 ms window will reject most local gamma/β background and yield slow but unmistakable muon coincidences; plan on hours per data point. ([IEEE Spectrum][5])

Bottom line
You can exploit real relativity-grade physics at home: detect **atmospheric muons** and do angle/attenuation experiments. Start with CosmicWatch for reliability or GM-coincidence for cost, and use a cloud chamber if you want to *see* tracks. ([Cosmic Connection][1], [GitHub][4], [IEEE Spectrum][5], [CERN][6])

[1]: https://cosmic.lbl.gov/SKliewer/Cosmic_Rays/Muons.htm?utm_source=chatgpt.com "Muons - Lawrence Berkeley National Laboratory"
[2]: https://www.hyperphysics.phy-astr.gsu.edu/hbase/Particles/muonatm.html?utm_source=chatgpt.com "Atmospheric Muons - HyperPhysics"
[3]: https://www.sciencedirect.com/science/article/pii/S0168900218307599?utm_source=chatgpt.com "Characterization of atmospheric muons at sea level using a cosmic ray ..."
[4]: https://github.com/spenceraxani/CosmicWatch-Desktop-Muon-Detector-v3X "GitHub - spenceraxani/CosmicWatch-Desktop-Muon-Detector-v3X: The new CosmicWatch Desktop Muon detector"
[5]: https://spectrum.ieee.org/diy-muon-tomography "Map Hidden Structures With a $100 DIY Muon Tomographer - IEEE Spectrum"
[6]: https://home.cern/news/news/experiments/how-make-your-own-cloud-chamber?utm_source=chatgpt.com "How to make your own cloud chamber - CERN"
[7]: https://www.amnh.org/exhibitions/einstein/educator-resources/building-a-cloud-chamber-cosmic-ray-detector?utm_source=chatgpt.com "Building a Cloud Chamber (Cosmic Ray Detector) | AMNH"
[8]: https://quarknet.fnal.gov/resources/QN_CloudChamberV1_4.pdf?utm_source=chatgpt.com "How to Build a Cosmic-Ray Cloud Chamber - QuarkNet"
[9]: https://quarknet.org/sites/default/files/cf_6000crmdusermanual-small.pdf?utm_source=chatgpt.com "QuarkNet Cosmic Ray Muon Detector User’s Manual Series \"6000\" DAQ"
[10]: https://studylib.net/doc/18324862/quarknet-cosmic-ray-muon-detector-user-s-manual-series?utm_source=chatgpt.com "QuarkNet Cosmic Ray Muon Detector User`s Manual Series"

