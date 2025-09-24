# Noisebox Patch Review

## Structure
- The engine lives in a dedicated `noisebox-engine.pd` abstraction so the main patch only hosts the interface, scope writer, and
touch pad. The abstraction fans the voice across oscillator, filter, delay, distortion, and output subpatches to keep the signal
flow legible.

## Controller wiring
- Every front-panel control is routed to a named parameter that the engine consumes. The oscillator frequency slider, waveform
selector, and hold toggle feed the pitch-quantising stage before smoothing, while the oscillator LFO rate/wave/depth values drive
the modulation generator.
- Filter, delay, and feedback controls reach their respective modules to set the dual filters, delay time, modulation depth, and
feedback amount, so those sliders actively shape the signal chain.
- Distortion range and volume sliders are read prior to the output stage; the processed signal is mirrored to the scope monitor
and routed through the volume multipliers, confirming those UI elements are functional.
- The frequency touch pad and oscilloscope subpatches are wired to update oscillator tuning and drive the display, so both non-
slider controllers serve a purpose.

## Audio path
- The abstraction modulates the oscillator, cascades a 24 dB low-pass filter, passes the signal through the LFO-driven delay with
feedback, shapes the result with a second filter and wavefolding distortion, mirrors it to the oscilloscope, and finally applies
the smoothed volume control before sending the stereo pair back to the main patch and on to `dac~`, yielding a complete audible
signal path.
