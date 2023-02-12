# Simple pulse desktop audio capture
Capture PulseAudio desktop audio with ease.

# Getting started
This crate exports the DesktopAudioRecorder struct, simply instantiate it with new and call `.read_frame()` in a loop to start recieving PCM audio data.

## Example
This example captures desktop audio and prints the PCM data for 5 seconds before quitting.
```rust
use std::time::Instant;
let mut recorder = DesktopAudioRecorder::new("Experiment").unwrap();

let start = Instant::now();

loop {
    match recorder.read_frame() {
        Ok(data) => println!("{:?}", data),
        Err(e) => eprintln!("{}", e)
    };

    if Instant::now().duration_since(start).as_millis() > 5000 {
        break;
    }
}
```
