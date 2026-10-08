# Prompt: Turn incident evidence into an interactive timeline

Investigate the supplied production incident and make it understandable through a **single offline HTML page**. The aim is to let another engineer *explore how the team reached its conclusions*, not merely read a chronological summary.

## Inputs

- Incident window: **[start/end timestamps and timezone]**.
- Evidence: **[logs, metrics, traces, deploy events, alerts, tickets, notes, or filenames]**.
- Context: **[services, architecture, affected endpoints, expected behavior]**.
- If the task is explicitly a demo with no real data, generate a clearly labeled **synthetic incident** and keep the scenario internally consistent.

## Evidence handling

1. Normalize timestamps to one timezone, retain original precision and note missing/uncertain clock offsets. Deduplicate repeated events without erasing meaningful differences.
2. Correlate deploys, feature flags, request traces, errors, infrastructure saturation, mitigations and recovery. Clearly separate **observation**, **hypothesis**, **confirmed cause** and **unknown**; chronology alone is not causality.
3. Never silently fabricate logs, alerts, metric values or root causes. If data is incomplete, expose that uncertainty. If using a made-up example, visibly label every source and the final conclusion as synthetic.
4. Remove secrets, tokens, customer identifiers and sensitive payloads from the page. Avoid embedding proprietary incident details when sharing publicly.

## The interactive explanation

- An event stream with timestamp, service, category and severity; filter/search by service or event type.
- A time scrubber or replay control that synchronizes selected event, log evidence and metric values.
- Dependency-free, readable visualizations of the important signals, with consistent axes, units and clear markers for deployments and interventions.
- An investigation panel explaining what each observation adds to or weakens about the leading hypothesis. Make the root-cause reveal optional so the viewer can reason through the data first.
- An end state: impact, mitigation, resolution, confidence/uncertainties and follow-up actions.

## Output and validation

- Deliver `incident.html` as **one complete HTML file** with inline CSS/JS/data. No scripts loaded from the internet, framework, build step, or telemetry.
- Make layout responsive, keyboard accessible and usable in light and dark modes. Provide textual descriptions so charts are not the only way to read evidence.
- Check timestamp sorting, units, nonnegative metric values, root-cause consistency and links between each event and its evidence.
- Open in a browser and test filters, event selection, time scrubber, replay/pause, metric switching, reveal/hide, mobile layout and console errors.
- Report what is real, what is synthetic, and any limitations of the available evidence.

**Key principle:** A good timeline is an argument backed by evidence, not simply a list of timestamped things.
