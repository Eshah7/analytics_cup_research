# SkillCorner X PySport Analytics Cup - Research Track
**Submission By:** Esha Shah

Please review the `submission.ipynb` file for the full code. An online static version can be found here: [Marimo Notebook](https://static.marimo.app/static/false-run-analysis-43m0).

---

## Research Track Abstract(max. 500 words)
### Quantifying the Unseen: Valuing False Runs with Expected Possession Value (EPV)
#### Introduction
Most popular analytics focus on possession and on-ball actions; the impact demonstrated through false runs (decoy movements to break defensive structures without receiving the ball) is undervalued and unmeasured. The challenge is to isolate the effect of a false run on the overall team success. A false run is difficult to identify in event data, yet it creates space by pulling defenders out of position, enabling teammates to exploit the resulting gap or incorrect marking. 

This research introduces a framework for detecting false runs and quantifying their impact using causal inference techniques applied to SkillCorner's tracking and dynamic event data. What would have happened if the false run never happened? I will compare the actual game states against "ghost" scenarios where runners stayed in their original positions, to measure the value added by off-ball movements. 

#### Methods
The method of identifying and quantifying false runs consists of 3 parts: detecting false runs, developing an Expected Possession Value (EPV) model using tracking data, and calculating the lift between actual game states and "ghost" scenarios.

**False Run Detection**

I identified potential candidate false runs from SkillCorner's dynamic events data by filtering for events with the following conditions: 

- Events started and ended in the attacking third
- Identified as an off-ball run 
- Runners did not receive the ball (player_posession or on_ball_engagement events) within 5 seconds (50 frames) following the run
- Certain off-ball run types: 'behind', 'run_ahead_of_the_ball', 'cross_receiver', 'pulling_wide', 'pulling_half_space', 'overlap', 'underlap'

These filters ensured that these were genuine decoy movements rather than attempts to receive the ball. Additionally, these events were incorporated with the tracking dataset at both start(frame_start) and end (frame_end) timestamps. I excluded any runs with missing positional data to avoid any modelling issues. 

**Expected Possession Value Model (EPV)**

To quantify the increase in attacking threat, I developed an EPV model using XGBoost that predicts the probability of a shot occurring within the next 10 seconds (100 frames) based on the current game state. The model uses 4 features derived from tracking data at each frame: 

- *Distance to Goal*: The Euclidean distance from ball position to the center of the opposing goal, $$\sqrt{(goal_x - ball_x)^2 + (goal_y)^2}$$.
- 

#### Results

#### Conclusion

---
## More Information
This repository contains the submission template for the SkillCorner X PySport Analytics Cup **Research Track**. Find the Analytics Cup [**Rules**]([https://github.com/SkillCorner/opendata/tree/master/data](https://pysport.org/analytics-cup/rules)) and [**tutorials**](https://github.com/SkillCorner/opendata/tree/master/resources) on the [**SkillCorner Open Data Repository**](https://github.com/SkillCorner/opendata).

All thoughts and ideas are my own; the formatting and code were elevated with the use of Gemini AI. Thank you for your time!
