# Post-Release Monitoring Guide

This guide provides the methodology for monitoring a new release after it has been deployed to production. It is intended to be used by the `Release Manager` and the deployment team when executing the `monitor-release` task.

## Purpose
Post-release monitoring is the process of closely observing a new release to ensure it is stable, performant, and healthy. This critical phase helps catch issues that may not have been apparent during testing and validates that the release has achieved its goals without introducing negative side effects.

## Core Principles
- **Trust, but Verify:** Even if the deployment was smooth, assume nothing. Verify the release's health with data.
- **Holistic View:** Monitor a combination of system, application, and business metrics to get a complete picture.
- **Proactive, Not Reactive:** The goal is to detect anomalies and trends *before* they become major incidents.
- **User-Centric:** Pay close attention to user-reported issues and sentiment. They are the ultimate judge of release quality.

## Monitoring Phases

### Phase 1: Intensive Monitoring (First 4 Hours)
This is the most critical period, as most deployment-related issues surface quickly.
- **Frequency:** Check key dashboards every 15-30 minutes.
- **Key Metrics:**
  - **Error Rates:** The most important leading indicator. Any significant spike in 5xx errors or new exception types requires immediate investigation.
  - **Performance:** p95/p99 latency. A sudden degradation indicates a problem.
  - **Infrastructure:** CPU, memory, and disk I/O. Look for saturation or runaway processes.
- **Actions:**
  - The deployment team should remain on high alert.
  - Triage any new alerts immediately.
  - If a rollback trigger is met, initiate the rollback procedure without delay.
  - Post hourly status updates to stakeholders.

### Phase 2: Extended Monitoring (4-24 Hours)
After the initial period of stability, monitoring can become less frequent but should focus more on trends.
- **Frequency:** Check key metrics every 2-4 hours.
- **Key Metrics:**
  - **Trend Analysis:** Are error rates or latency slowly creeping up? Is memory usage steadily increasing (potential leak)?
  - **Business KPIs:** Are conversion rates, sign-ups, and transactions performing as expected over a longer period?
  - **Support Tickets:** Are users reporting any new, unexpected issues?
- **Actions:**
  - Investigate any negative trends.
  - Correlate user reports with observed metrics.
  - At the 24-hour mark, compile a comprehensive health report.

### Phase 3: Long-Term Monitoring (24-48 Hours)
This phase confirms the long-term stability of the release.
- **Frequency:** A final check at the 48-hour mark.
- **Key Metrics:**
  - **Sustained Health:** Confirm that all system and business metrics have remained stable for two full days.
  - **User Sentiment:** Review social media and community feedback for any emerging patterns.
  - **Feature Adoption:** If new features were released, check their adoption and usage metrics.
- **Actions:**
  - Declare the release officially "stable."
  - Transition from intensive monitoring back to standard, operational on-call procedures.
  - Schedule the post-release retrospective.

## Key Metrics to Watch
- **Application Metrics:** Error Rates (5xx, 4xx), Latency (p50, p95, p99), Throughput (RPS).
- **Infrastructure Metrics:** CPU Utilization, Memory Usage, Disk I/O, Network Traffic.
- **Database Metrics:** Query Latency, Connection Pool Usage, Replication Lag.
- **Business Metrics:** Conversions, User Sign-ups, Transaction Volume, Revenue.
- **User-Reported Metrics:** Support Ticket Volume, App Store Reviews, Social Media Sentiment.

The goal is to move from a state of high alert to confident stability, backed by data from all these sources.
