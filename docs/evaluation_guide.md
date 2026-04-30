# CO326 Edge AI Mini Project - Practical Guide for Group 17

This guide breaks your 2-week mini project into clear, small tasks so your team can finish without confusion.

## 1) What your system must do
Your final pipeline should be:

**Sensor/Data -> Python Edge AI -> MQTT Broker -> Node-RED -> Dashboard**

Minimum you must show in demo:
- Data is generated (or read from dataset)
- Data is processed locally in Python
- AI/anomaly rule runs locally (edge)
- Data + alerts are published via MQTT
- Node-RED dashboard displays values and alert status

## 2) Repository structure required for evaluation
Create and keep this structure:

```
edge-ai-group17/
├── python/                  # Python scripts (publisher, edge_ai, etc.)
├── node-red/                # flows.json and Node-RED dashboard config
├── docs/                    # report + architecture images
└── README.md
```

## 3) Evaluation-focused 14-day plan

### Days 1-2: Environment + GitHub setup
- Verify Docker and Docker Compose work
- Run: `docker-compose up --build`
- Confirm Node-RED opens on `http://localhost:1880`
- Push initial commit with clean folder structure

### Days 3-4: Data acquisition
- Build/update `mqtt_publisher.py`
- Simulate sensor values (example: ambient light, occupancy)
- Publish to topic:
  - `sensors/group17/lighting/data`

### Days 5-6: MQTT communication validation
- Connect Python to instructor MQTT broker
- Verify published messages are visible in Node-RED debug
- Keep logs/screenshots as proof

### Day 7: Dashboard
- Add at least:
  - Chart (time series)
  - Gauge (live numeric value)
  - Text widget (status)

### Days 8-9: Edge AI logic (20 marks)
Implement one of:
- Rule-based anomaly detection (fast + easy)
  - Example: `lux < 5` (possible blackout), `lux > 900` (flash anomaly)
- OR simple ML model

Recommended for quick success: start with threshold/rule-based, then optionally add ML.

### Days 10-11: Alerts integration
- Publish alert topic:
  - `alerts/group17/lighting/status`
- Display alert in Node-RED dashboard text/card with color

### Days 12-13: Testing + debugging
Check each link in chain:
1. Python publishes JSON
2. MQTT broker receives
3. Node-RED subscribes and parses JSON
4. Dashboard updates live
5. Alerts trigger correctly

### Day 14: Final demo prep
Prepare a 3-5 minute demo:
1. Start containers
2. Run publisher and edge AI
3. Show live chart/gauge
4. Force anomaly and show alert
5. Show repository commits + report

## 4) What lecturer usually checks during evaluation/demo
To score well, make sure evaluators can clearly see these in order:
1. **Live simulation is running** (values changing every few seconds)
2. **MQTT topic correctness** (`sensors/.../data` and `alerts/.../status`)
3. **Edge AI decision** (normal vs alert) is made in local Python
4. **Dashboard reacts live** (chart, gauge, text)
5. **Proof in GitHub** (multiple commits over multiple days)

## 5) Demo simulation script (say + do this in front of lecturer)

### Step A - Start services
- `docker-compose up --build`
- Show Node-RED at `http://localhost:1880` and dashboard at `http://localhost:1880/ui`

### Step B - Start data simulation
- Run publisher script and explain: "This simulates light sensor values."
- Show changing JSON in terminal or Node-RED debug panel.

### Step C - Show edge AI logic
- Explain simple rule: if `lux < 5` or `lux > 900`, publish alert.
- Show terminal prints: NORMAL / ALERT.

### Step D - Force an anomaly
- Temporarily send a bad value (example `lux=950`).
- Show alert topic message: `alerts/group17/lighting/status`.
- Show dashboard text color/status changes to ALERT.

### Step E - Close with outcomes
- Show chart history, current gauge, and alert count/status.
- Show GitHub commits and `docs/report`.

## 6) Scoring strategy (how to maximize marks)

- **System functionality (25):** stable end-to-end data flow demo
- **Edge AI (20):** clear local intelligence logic with explanation
- **MQTT (15):** correct topic design + reliable publish/subscribe
- **Dashboard (10):** readable, meaningful live visualization
- **GitHub & code quality (15):** clean commits, structure, script naming
- **Documentation (10):** complete README + 5-10 page report
- **Innovation (5):** one extra feature (e.g., adaptive threshold, notification)

## 7) Minimum README checklist
Your `README.md` must include:
- Project Title
- Group Members
- Project Description
- System Architecture
- How to Run
- MQTT Topics Used
- Results (screenshots)
- Challenges
- Future Improvements

## 8) Minimum report checklist (docs/report.pdf or docs/report.md)
- Problem statement
- Architecture diagram
- Implementation details (Python + Node-RED + MQTT)
- AI/anomaly logic and formulas
- Test results/screenshots
- Challenges and fixes
- Conclusion and future work

## 9) Commit plan (important for marks)
Do not upload everything at the end. Use frequent commits, for example:
- `setup docker compose and project structure`
- `add mqtt publisher for light data`
- `add node-red dashboard widgets`
- `implement anomaly alert logic`
- `add final report and screenshots`

## 10) Common mistakes to avoid
- No `docs/` folder
- Missing screenshots in README
- Publishing to wrong MQTT topics
- Doing AI in cloud instead of local Python
- One big last-day commit

## 11) Simple task split for your 3-member team
- **Member A:** Python publisher + edge AI rules
- **Member B:** Node-RED flow + dashboard UI
- **Member C:** Documentation + integration testing + GitHub hygiene

Then cross-check each other's work during Day 12-13.
