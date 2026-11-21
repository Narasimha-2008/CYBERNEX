# CYBERNEX — Functional Log Analysis Website

This package adds a real browser-side CSV upload and analysis workflow.

## Run
Open `index.html` in Chrome or Edge. No server or external AI service is required.

## What is implemented
- Multiple CSV upload with drag/drop and browse
- CSV parser that reads actual file bytes
- File-size/type validation
- Empty/invalid timestamp/duplicate-row checks
- Column mapping for non-standard column names
- Normalization of available fields
- Deterministic detection rules:
  - Brute Force: >=5 failures in 10 minutes
  - Possible Account Compromise: success after >=3 failures in 10 minutes
  - New Device: new device/IP for a user in the available dataset
  - Unusual Login Time: 22:00–06:00
  - Privileged Access: privileged/restricted action associated with normal/elevated role information
  - Unusual File Access: >200 file-access events in 10 minutes
  - Possible Data Exfiltration: >100 MB outbound transfer
- 30-minute event correlation using username, source IP, and device ID
- Risk scoring: Brute Force +25, New Device +20, Unusual Login Time +15, Privileged Access +15, Large Data Transfer +16, capped at 100
- Severity bands: Low 0–24, Medium 25–49, High 50–74, Critical 75–100
- Evidence/explanations/recommendations
- Incident investigation view
- Local upload history
- Synthetic Attack Simulation Center using the same detection pipeline
- Responsive desktop/mobile layout
- Local-only processing; no uploaded CSV contents are sent to an external AI service

## Integration
If your current CYBERNEX site already has an existing shell, keep its navigation/theme and transplant the Log Analysis page plus the functions in `app.js`. The detection/correlation functions are deliberately separated from the UI so the same functions can be called by the existing Attack Simulation Center.

## Important
This is a frontend/local prototype. For production deployment, move persistence and processing to a secured backend, enforce server-side size/type validation, authentication/authorization, retention controls, encryption at rest, and audit logging.


## Quick test
1. Open `index.html`.
2. Click **Add CSV Logs** or **Browse files**.
3. Add the CSV files in `samples/` or your own CSV logs.
4. Review the column mapping and validation.
5. Click **Run detection engine**.
6. Open the generated incident from **Incidents** or **Investigation**.

The upload area accepts multiple CSV files at once and reads their real contents locally in the browser.
