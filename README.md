# Pitch Control

**A Flutter game you steer with your voice: sing higher and the ball rises, go quiet and it falls, and you dodge the spikes.**

<img src="porocilo/figures/game_start.jpg" alt="Start of a game: a blue ball near the orange floor, one red spike hanging from the ceiling, score and top score at the top, five hearts for lives" width="220"/>
<img src="porocilo/figures/obstacles_many.jpg" alt="A rapid run of spikes from the ceiling and the floor" width="220"/>
<img src="porocilo/figures/lives.jpg" alt="Later in a game with two of the five lives lost" width="220"/>

## Why it exists

Solo coursework at the Faculty of Computer and Information Science, University of Ljubljana (Jan 2025). The question was whether the pitch of a voice works as a continuous game control, where speech commands only give discrete ones. The written report is in [`porocilo/`](porocilo/) and the slides are in [`predstavitev/`](predstavitev/).

## How it works

| File | What it does |
|---|---|
| `lib/pitch_detector_service.dart` | Captures the microphone at 44.1 kHz with `flutter_audio_capture` and runs `pitch_detector_dart` on each buffer. Any sound also starts or restarts the game. |
| `lib/ball_controller.dart` | The game loop: gravity, spikes from the ceiling and the floor, occasional rapid runs of spikes, speed that rises over time, collisions, 5 lives, score and top score. |
| `lib/game_screen.dart`, `lib/spike_painter.dart` | Draws the ball, the spikes and the hearts. |

The pitch range from E3 (164.81 Hz) to about C♯5 (553.25 Hz) maps linearly to the height of the screen. When the voice asks for a point above the ball, the ball gets exactly the upward speed it needs to reach that height under gravity (`v = √(2gh)`), so it moves in a natural arc instead of jumping. When the voice stops, gravity brings it down.

## Run it

Needs Flutter with Dart 3.5 or later and a phone with a microphone.

```sh
flutter pub get
flutter run
```

Allow microphone access when asked.

## Tech

Flutter, Dart, `flutter_audio_capture`, `pitch_detector_dart`, `permission_handler`, `provider`.

## Status

Coursework, finished in Jan 2025. Made by [Erik Pahor](https://github.com/MuteMuty), alone.
