# PostHog Analytics Setup Plan — Landit

## Current State

- **PostHog project:** Created at `us.i.posthog.com`
- **API key:** `phc_uCSSQAz47a7tWdnpqrKdttANBti6wLWiKNgtcKvkRaM8`
- **SDK:** `posthog-ios` integrated via SPM
- **Opt-in:** Users must enable analytics in Settings (default off)
- **Landing page:** No PostHog JS snippet yet

## Events Already Instrumented (macOS App)

| Event                                          | Source                                             | Properties                                                                                                            |
| ---------------------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `app_launched`                                 | LanditApp.swift                                    | app_version                                                                                                           |
| `screen_viewed`                                | ContentView.swift                                  | screen_name                                                                                                           |
| `section_navigated`                            | ContentView.swift                                  | section_name                                                                                                          |
| `onboarding_step_viewed`                       | OnboardingView.swift                               | step_name                                                                                                             |
| `onboarding_completed`                         | OnboardingView.swift                               | —                                                                                                                     |
| `discovery_run`                                | BackgroundScheduler.swift                          | jobs_found, sources                                                                                                   |
| `discovery_funnel`                             | DiscoveryPipeline.swift                            | raw, after_dedup, after_location, after_visa, after_seen, scored, duration_seconds, source_count, failed_source_count |
| `discovery_source`                             | DiscoveryPipeline.swift                            | source_name, status, job_count, duration_seconds, error_kind                                                          |
| `scoring_run`                                  | BackgroundScheduler.swift, ScoringConfigView.swift | count, above_threshold                                                                                                |
| `interview_started`                            | InterviewSetupView.swift                           | type, difficulty, mode                                                                                                |
| `interview_completed`                          | InterviewSetupView.swift                           | type, score, duration_seconds                                                                                         |
| `status_changed`                               | PipelineView.swift, JobsListView.swift             | from, to                                                                                                              |
| `feature_used`                                 | Various                                            | feature_name                                                                                                          |
| `quick_action_clicked`                         | DashboardView.swift                                | action_name                                                                                                           |
| `coach_message_sent`                           | CareerCoachView.swift                              | —                                                                                                                     |
| `coach_voice_started`                          | CareerCoachView.swift                              | —                                                                                                                     |
| `cover_letter_generated`                       | CoverLetterView.swift                              | company                                                                                                               |
| `cover_letter_scored`                          | CoverLetterView.swift                              | —                                                                                                                     |
| `contact_saved` / `contact_deleted`            | ContactsListView.swift                             | —                                                                                                                     |
| `offer_saved` / `offer_deleted`                | OffersView.swift                                   | —                                                                                                                     |
| `note_saved`                                   | NotesView.swift                                    | —                                                                                                                     |
| `profile_saved`                                | SettingsView.swift                                 | —                                                                                                                     |
| `data_exported`                                | SettingsView.swift                                 | format                                                                                                                |
| `data_imported`                                | SettingsView.swift                                 | record_count                                                                                                          |
| `bulk_cleanup`                                 | HousekeepingView.swift                             | type, count                                                                                                           |
| `salary_data_viewed` / `salary_data_refreshed` | InsightsView.swift                                 | —                                                                                                                     |
| `answer_vault_save`                            | AnswerVaultView.swift                              | —                                                                                                                     |
| `ai_provider_used`                             | (defined, needs more callsites)                    | provider, feature                                                                                                     |

---

## Step 1: PostHog Dashboard Login & Project Verification

1. Go to https://us.app.posthog.com
2. Log in (or create account if not done)
3. Verify the project exists and the API key matches
4. Check **Activity** tab — if `app_launched` events appear, the SDK is already sending data
5. If no events: launch the app with analytics enabled, trigger a few actions, check again after 1-2 minutes

---

## Step 2: Add PostHog JS to Landing Page

Add this snippet to `index.html` just before `</head>`:

```html
<script>
  !(function (t, e) {
    var o, n, p, r;
    e.__SV ||
      ((window.posthog = e),
      (e._i = []),
      (e.init = function (i, s, a) {
        function g(t, e) {
          var o = e.split(".");
          (2 == o.length && ((t = t[o[0]]), (e = o[1])),
            (t[e] = function () {
              t.push([e].concat(Array.prototype.slice.call(arguments, 0)));
            }));
        }
        (((p = t.createElement("script")).type = "text/javascript"),
          (p.crossOrigin = "anonymous"),
          (p.async = !0),
          (p.src =
            s.api_host.replace(".i.posthog.com", "-assets.i.posthog.com") +
            "/static/array.js"),
          (r = t.getElementsByTagName("script")[0]).parentNode.insertBefore(
            p,
            r,
          ));
        var u = e;
        for (
          void 0 !== a ? (u = e[a] = []) : (a = "posthog"),
            u.people = u.people || [],
            u.toString = function (t) {
              var e = "posthog";
              return (
                "posthog" !== a && (e += "." + a),
                t || (e += " (stub)"),
                e
              );
            },
            u.people.toString = function () {
              return u.toString(1) + ".people (stub)";
            },
            o =
              "init capture register register_once register_for_session unregister unregister_for_session getFeatureFlag getFeatureFlagPayload isFeatureEnabled reloadFeatureFlags updateEarlyAccessFeatureEnrollment getEarlyAccessFeatures on onFeatureFlags onSessionId getSurveys getActiveMatchingSurveys renderSurvey canRenderSurvey getNextSurveyStep identify setPersonProperties group resetGroups setPersonPropertiesForFlags resetPersonPropertiesForFlags setGroupPropertiesForFlags resetGroupPropertiesForFlags reset get_distinct_id getGroups get_session_id get_session_replay_url alias set_config startSessionRecording stopSessionRecording sessionRecordingStarted captureException loadToolbar get_property getSessionProperty createPersonProfile opt_in_capturing opt_out_capturing has_opted_in_capturing has_opted_out_capturing clear_opt_in_out_capturing debug getPageViewId".split(
                " ",
              ),
            n = 0;
          n < o.length;
          n++
        )
          g(u, o[n]);
        e._i.push([i, s, a]);
      }),
      (e.__SV = 1));
  })(document, window.posthog || []);
  posthog.init("phc_uCSSQAz47a7tWdnpqrKdttANBti6wLWiKNgtcKvkRaM8", {
    api_host: "https://us.i.posthog.com",
    person_profiles: "always",
  });
</script>
```

Then add custom event tracking for key landing page actions:

```javascript
// In the download button click handler:
posthog.capture("landing_download_clicked", { platform: "macos" });

// In the GitHub link:
posthog.capture("landing_github_clicked");

// Track which screenshot tabs users click:
posthog.capture("landing_screenshot_tab", { tab: tabName });
```

---

## Step 3: Create PostHog Dashboards

### Dashboard 1: Core Growth Metrics (for Acquirers)

This is the dashboard you'd show Indeed/ZipRecruiter.

| Insight                        | Type    | Query                                                       |
| ------------------------------ | ------- | ----------------------------------------------------------- |
| **DAU**                        | Trend   | `app_launched` unique users, daily                          |
| **WAU**                        | Trend   | `app_launched` unique users, weekly                         |
| **MAU**                        | Trend   | `app_launched` unique users, monthly                        |
| **DAU/MAU Ratio**              | Formula | `DAU / MAU` (stickiness — >20% is strong)                   |
| **New vs Returning**           | Trend   | `app_launched` breakdown by "new vs returning"              |
| **Onboarding Completion Rate** | Funnel  | `onboarding_step_viewed` (Welcome) → `onboarding_completed` |
| **Total Downloads**            | Number  | GitHub API downloads (tracked externally)                   |

**How to create in PostHog:**

1. Go to **Dashboards** → **New Dashboard** → Name: "Landit — Growth"
2. Click **+ New Insight** for each row above
3. For DAU: Event = `app_launched`, Aggregation = "Unique users", Interval = "Day"
4. For MAU: Same but Interval = "Month"
5. For DAU/MAU: Use **Formula** mode — create two series (DAU as A, MAU as B), formula = `A/B`

### Dashboard 2: Feature Engagement

| Insight                       | Type      | Query                                            |
| ----------------------------- | --------- | ------------------------------------------------ |
| **Top Features**              | Bar chart | `feature_used` grouped by `feature_name`, top 10 |
| **Screen Popularity**         | Bar chart | `screen_viewed` grouped by `screen_name`         |
| **Discovery Usage**           | Trend     | `discovery_run` count per day                    |
| **Jobs Found per Run**        | Trend     | `discovery_run` avg `jobs_found`                 |
| **Interview Sessions**        | Trend     | `interview_started` count per week               |
| **Interview Completion Rate** | Funnel    | `interview_started` → `interview_completed`      |
| **Avg Interview Score**       | Trend     | `interview_completed` avg `score`                |
| **Coach Usage**               | Trend     | `coach_message_sent` count per day               |
| **AI Features**               | Bar chart | `ai_provider_used` grouped by `feature`          |

### Dashboard 3: Discovery Pipeline Health

| Insight               | Type      | Query                                                                                           |
| --------------------- | --------- | ----------------------------------------------------------------------------------------------- |
| **Funnel Conversion** | Funnel    | `discovery_funnel` — show raw → after_dedup → after_location → after_visa → after_seen → scored |
| **Source Health**     | Table     | `discovery_source` grouped by `source_name`, showing avg `job_count` and `status` distribution  |
| **Error Rates**       | Bar chart | `discovery_source` where `error_kind` exists, grouped by `error_kind`                           |
| **Avg Run Duration**  | Trend     | `discovery_funnel` avg `duration_seconds`                                                       |

### Dashboard 4: Landing Page

| Insight                   | Type      | Query                                     |
| ------------------------- | --------- | ----------------------------------------- |
| **Page Views**            | Trend     | `$pageview` count, daily                  |
| **Unique Visitors**       | Trend     | `$pageview` unique users, daily           |
| **Download Clicks**       | Trend     | `landing_download_clicked` count          |
| **Visit → Download Rate** | Funnel    | `$pageview` → `landing_download_clicked`  |
| **Screenshot Tab Clicks** | Bar chart | `landing_screenshot_tab` grouped by `tab` |

---

## Step 4: Key Metrics to Track for Acquisition

These are the numbers acquirers (Indeed, ZipRecruiter, LinkedIn) will ask about:

| Metric                       | Target | How to Measure                                                                        |
| ---------------------------- | ------ | ------------------------------------------------------------------------------------- |
| **MAU**                      | 1,000+ | `app_launched` unique users/month                                                     |
| **DAU/MAU (Stickiness)**     | >25%   | Formula insight                                                                       |
| **D1 Retention**             | >40%   | PostHog Retention insight: `app_launched` on Day 0, returning `app_launched` on Day 1 |
| **D7 Retention**             | >20%   | Same, Day 7                                                                           |
| **D30 Retention**            | >10%   | Same, Day 30                                                                          |
| **Avg Sessions/User/Week**   | >3     | `app_launched` count / unique users, weekly                                           |
| **Discovery Runs/User/Week** | >2     | Shows the product has a recurring loop                                                |
| **Interview Sessions/User**  | >1     | Shows engagement beyond job listing                                                   |
| **Onboarding Complete %**    | >70%   | Funnel                                                                                |

**How to set up Retention in PostHog:**

1. Go to **Insights** → **New Insight** → **Retention**
2. Cohort event: `app_launched`
3. Return event: `app_launched`
4. Period: Day
5. This shows D1, D7, D14, D30 automatically

---

## Step 5: Set Up Cohorts

Create these user segments in PostHog → **Cohorts**:

| Cohort              | Definition                                                       | Purpose                         |
| ------------------- | ---------------------------------------------------------------- | ------------------------------- |
| **Power Users**     | `app_launched` ≥ 5 times in last 7 days                          | Track your most engaged users   |
| **Discovery Users** | Performed `discovery_run` in last 30 days                        | Users using core feature        |
| **Interview Users** | Performed `interview_started` in last 30 days                    | Users using premium feature     |
| **New This Week**   | First seen in last 7 days                                        | Track new user behavior         |
| **Churned**         | No `app_launched` in last 14 days, but was active 15-45 days ago | Track who stopped using the app |

---

## Step 6: Set Up Actions & Alerts

In PostHog → **Data Management** → **Actions**:

1. **Core Loop Complete** = `discovery_run` → `status_changed` (to "Applied") within same session
2. **Interview Loop** = `interview_started` → `interview_completed` within same session

Set up **Alerts** (PostHog → Insights → each insight → "Subscribe"):

- Alert if DAU drops below 50% of 7-day average (early churn signal)
- Alert if `discovery_source` error rate exceeds 30% for any source (scraper broken)
- Weekly email digest of growth dashboard

---

## Step 7: Session Replay (Optional but High-Value)

PostHog supports session replay for web (landing page only, not native macOS).

Add to the PostHog init config on the landing page:

```javascript
posthog.init("phc_...", {
  api_host: "https://us.i.posthog.com",
  person_profiles: "always",
  session_recording: {
    recordCrossOriginIframes: true,
  },
});
```

This lets you watch how visitors interact with the landing page — which sections they scroll to, where they drop off, whether they click download.

---

## Summary — What to Do Right Now

1. **Log into PostHog** at https://us.app.posthog.com — verify events are flowing
2. **Add PostHog JS snippet** to `index.html` (see Step 2)
3. **Create the 4 dashboards** (Growth, Engagement, Discovery Health, Landing Page)
4. **Set up Retention insight** — this is the #1 metric acquirers will ask for
5. **Create cohorts** for Power Users and Churned segments
6. **Set up alerts** for DAU drops and scraper errors
7. **Share dashboard links** — PostHog lets you create public dashboard URLs for investor/acquirer presentations
