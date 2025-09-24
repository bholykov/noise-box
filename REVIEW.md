# Noisebox Patch Review

## Controller wiring
- Every front-panel control is routed to a named parameter that the engine consumes. The oscillator frequency slider, waveform selector, and hold toggle all feed the frequency conditioning before the base pitch storage, while the LFO rate/wave/depth values drive the modulation generator.
- Filter, delay, and feedback controls each arrive inside the engine to set the dual filters, delay time, modulation depth, and feedback amount, ensuring those sliders actively shape the signal chain.
- Distortion range and volume sliders are read prior to the output stage; the processed signal is mirrored to the scope monitor and routed through the volume multipliers, confirming those UI elements are functional.
- The frequency touch pad and oscilloscope subpatches are wired to update oscillator tuning and drive the display, so both non-slider controllers serve a purpose.

## Audio path
- The engine modulates the oscillator, passes it through the first filter, feeds the delay (with its own LFO and feedback), shapes the result with a second filter and wavefolding distortion, and finally applies the volume control before sending the stereo pair to `dac~`, yielding a complete audible signal path.

