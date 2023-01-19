# tec-COSMIC
TEC-1 cosmic ray detector



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

