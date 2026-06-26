# AI-Driven Difficulty Optimizer for Text Adventures

Building AI -kurssiprojekti

## Yhteenveto

This project introduces an AI-driven playtesting and difficulty optimization tool designed specifically for text adventure games. By analyzing player choice logs and text-entry data, the system utilizes linear regression and hill-climbing optimization to balance game pacing, prevent player frustration, and dynamically adjust hint systems.

## Background

Text adventures and interactive fiction heavily rely on puzzles and narrative flow, but game designers face major challenges in balancing difficulty:
* **Player Frustration:** If a puzzle is too obscure or a text command is consistently rejected, players quit the game (e.g., getting stuck typing variations of "take key").
* **Pacing Issues:** Static games cannot adapt to different player skill levels or reading speeds.
* **Manual Playtesting:** Tracking down dead-ends, soft-locks, or overly difficult logic paths traditionally requires hundreds of hours of manual testing.

My personal motivation stems from developing text-based adventure games in Unity (C#) and realizing how hard it is to manually balance word-recognition and puzzle complexity for non-native speakers or casual gamers.

## How is it used?

The system runs in the background of a text adventure game (integrated directly into the game engine's input controller). It collects anonymous session data, tracks player progression times between rooms, and logs unrecognized command strings. 

The primary users are game developers who receive automated reports about where players get stuck. Ultimately, it affects the players themselves, who get a smoother, more responsive gameplay experience through dynamic hint generation.

An abstract architecture of the input tracking and analysis routine can be described like this:
```python
def analyze_player_friction(room_logs):
    # Analyze input failures and time spent in a specific room
    for room in room_logs:
        failed_commands = room['unrecognized_inputs']
        time_spent = room['duration_seconds']
        
        # Simple baseline check for high player friction
        if len(failed_commands) > 5 and time_spent > 300:
            print(f"Alert: High puzzle friction detected in {room['name']}. Suggesting dynamic hint.")
```

## Data sources and AI methods

The project relies on two main data sources:
1. **In-game Player Logs:** Anonymous text-input history, timestamped room transitions, and action success rates collected during beta testing.
2. **Text Similarity Vectors:** Utilizing open-source word embeddings to calculate distances between failed player inputs and accepted action keywords.

Key AI techniques utilized:
* **Linear Regression:** Used to predict total game completion time based on early-game puzzle friction and room traversal speeds.
* **Nearest Neighbor (KNN):** Grouping player behaviors into archetypes (e.g., speedrunners vs. thorough explorers) to tailor the experience.
* **Simulated Annealing / Hill Climbing:** Optimizing the hidden puzzle difficulty parameters and word-recognition thresholds to maximize player retention rates.

## Challenges

What this project does *not* solve:
* It cannot automatically fix bad narrative writing or poor fundamental game design.
* **Ethical Considerations:** Player input tracking must be entirely anonymous, transparent, and strictly opt-in to avoid privacy violations.
* The system might suffer from overfitting if trained on a very small group of hardcore beta testers, leading to poor difficulty scaling for more casual audiences.

## What next?

The project could evolve into a universal, open-source plug-in for popular game engines like Unity or Godot, allowing independent text adventure creators to balance their games effortlessly. To move forward, I would need collaboration with data engineering experts to build a robust cloud dashboard for real-time visualization of playtest analytics.

## Acknowledgments

* Inspired by the *Building AI* course created by Reaktor and the University of Helsinki.
* Inspired by classic interactive fiction systems and modern NLP text parsing tools.
