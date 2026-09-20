# Alex Classic

Alex Classic is an accessibility-focused preservation and reverse-engineering project for the legendary Alex speech synthesizer shipped with OS X 10.5 Leopard, Build 9A581.

## Project overview

The project investigates how to preserve Alex’s distinctive speech quality as an offline, inspectable voice engine rather than depending on a modern platform speech service whose behavior can change underneath users. The goal is a technically grounded reconstruction that respects the original voice while making the pipeline usable by blind developers and listeners.

## Technical scope

- Extract and catalog the approximately 670 MB PCM wavetable dataset contained in `Alex.SpeechVoice`.
- Analyze formants, phoneme transitions, pitch movement, timing, and coarticulation behavior.
- Preserve the breath model and expressive cues that make Alex sound natural rather than reducing the voice to generic concatenated samples.
- Build reproducible tools for inspection, conversion, validation, and regression testing.

The repository will distinguish confirmed observations from reverse-engineering assumptions.

## Target architecture

The target is a portable synthesis pipeline with two front ends: an iOS Audio Unit for integration with accessible audio workflows, and a standalone offline synthesizer for macOS, iOS, and other compatible environments.

The engine should accept text or phonetic input, select and transform the appropriate wavetable material, apply formant and timing behavior, and render audio without requiring a cloud connection.

## Roadmap

### Phase 1: Leopard wavetable extraction and decompression

- Identify the `Alex.SpeechVoice` container and document its relevant headers, indexes, compression, and checksum behavior.
- Build a deterministic extractor that preserves source offsets and emits validated PCM or lossless intermediate assets.
- Record provenance, tool versions, hashes, and extraction limitations so results are reproducible and auditable.

### Phase 2: Formant and phoneme transition mapping

- Catalog phoneme units, allophones, diphones, and transition boundaries in the extracted material.
- Measure formants, pitch contours, duration, coarticulation, and breath/noise components.
- Define a machine-readable mapping format with explicit units, sample rates, confidence levels, and unknown values.

### Phase 3: DSP and synthesis engine prototype

- Implement offline unit selection and wavetable playback with deterministic timing and pitch control.
- Prototype formant-preserving pitch shifting, crossfades, envelope shaping, and expressive/breath components.
- Add golden audio fixtures, numerical checks, listening tests, and regression reports; document artifacts rather than masking them.

### Phase 4: iOS Audio Unit and sovereign local speech service

- Package the engine as an iOS Audio Unit with a clearly labeled, keyboard-accessible configuration surface and VoiceOver-friendly status reporting.
- Provide a local speech-service interface for offline text or phonetic input, with no cloud dependency or telemetry.
- Define resource, latency, interruption, battery, and licensing behavior before treating the prototype as production-ready.

Each phase should preserve accessibility, local data ownership, and clear separation between verified findings and hypotheses. Interfaces must expose meaningful labels, focus order, errors, progress, and completion state to screen-reader and keyboard users.

## Accessibility rationale

Modern iOS speech has not always preserved the reliability and character blind users depend on. VoiceOver degradation, pitch distortion, and changes in speech behavior can make navigation and concentration harder, especially when users have no practical visual fallback.

An offline, sovereign voice engine provides an alternative: the voice data remains available locally, processing is inspectable, and the user is not dependent on a remote service or an operating-system update to retain a familiar speech experience. Accessibility here is not only a user-interface concern; it is also a preservation, reliability, and digital-sovereignty concern.

## Status

This is an evolving research and engineering project. No claim is made that the complete synthesizer has already been reconstructed. The repository is intended to hold verified extraction work, analysis tools, design notes, and later implementation components.
