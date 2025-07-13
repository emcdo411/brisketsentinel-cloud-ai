# 🔥 BrisketSentinel — AI-Powered Grill Monitoring App

Real-time smoke intelligence for brisket perfection.  
Built with **RShiny**, **PowerShell**, and a future-ready cloud/API strategy.

---

## 📑 Table of Contents

- [🚀 Summary](#-summary)
- [📦 Tech Stack & Installed Packages](#-tech-stack--installed-packages)
- [🧠 Architecture Diagram](#-architecture-diagram)
- [💻 PowerShell Code (with & without API)](#-powershell-code-with--without-api)
- [📊 R Code (with & without API)](#-r-code-with--without-api)
- [🌐 Free Cloud/API Integration Options](#-free-cloudapi-integration-options)
- [🔎 Why This Matters](#-why-this-matters)
- [🧩 Conclusion](#-conclusion)

---

## 🚀 Summary

**BrisketSentinel** is a modular, cloud-adaptable grilling analytics tool designed for:
- **Solutions Architects** seeking IoT-to-Cloud integrations
- **Data Engineers** handling real-time telemetry
- **Non-technical users** needing easy-to-read cooking alerts

This app simulates and monitors brisket temperature, carcinogenic compound buildup (HCAs & PAHs), and smoke/fat drip dynamics using live or fallback JSON logs. Designed with scalability in mind, BrisketSentinel is API-friendly, dashboarded in RShiny, and ready for deployment via Docker or cloud edge devices.

---

## 📦 Tech Stack & Installed Packages

| Tool / Package | Description |
|----------------|-------------|
| ![RStudio](https://img.shields.io/badge/RStudio-IDE-blue?logo=rstudio) | App host + R dashboard engine |
| ![Shiny](https://img.shields.io/badge/Shiny-Dashboard-orange?logo=r) | UI and interactivity |
| ![PowerShell](https://img.shields.io/badge/PowerShell-System%20Telemetry-282C34?logo=powershell) | Log collector |
| ![ggplot2](https://img.shields.io/badge/ggplot2-Graphing-green?logo=r) | Chart rendering |
| ![jsonlite](https://img.shields.io/badge/jsonlite-JSON%20Parser-lightgrey?logo=json) | JSON ingestion |
| ![lubridate](https://img.shields.io/badge/lubridate-Time%20Parsing-cyan?logo=r) | Timestamp handling |
| ![dplyr](https://img.shields.io/badge/dplyr-Data%20Wrangling-blueviolet?logo=r) | Reactive data prep |
| ![DT](https://img.shields.io/badge/DT-Interactive%20Tables-yellow?logo=table) | DataTables integration |
| ![scales](https://img.shields.io/badge/scales-Finishing%20Touches-orange?logo=r) | Y-axis formatting |

---

## 🧠 Architecture Diagram

```mermaid
flowchart TD
  subgraph Local Device
    A[PowerShell Log Generator] --> B[JSON Log File]
  end

  subgraph RShiny App
    B --> C[read_log()]
    C --> D[Reactive Analysis]
    D --> E1[Trend Plots]
    D --> E2[Threshold Alerts]
    D --> E3[Downloadable Table]
    D --> E4[API Ready Output]
  end

  subgraph Optional Cloud
    F[Free API or S3 Bucket]
    E4 --> F
    F --> G[Remote UI or Edge Display]
  end



## 💻 PowerShell Code (With & Without API)

### ✅ Without API (local-only JSON log):

```powershell
$logPath = "C:\GrillLogs\brisket_temp_log.json"
$data = @()
for ($i = 0; $i -lt 13; $i++) {
  $entry = [PSCustomObject]@{
    Timestamp     = (Get-Date).AddMinutes(-$i * 5).ToString("s")
    TempF         = Get-Random -Minimum 200 -Maximum 300
    HCA_Signal    = Get-Random -Minimum 10 -Maximum 20
    SmokeDensity  = Get-Random -Minimum 5 -Maximum 15
    FatDripRate   = Get-Random -Minimum 5 -Maximum 10
  }
  $data += $entry
}
$data | ConvertTo-Json | Out-File -Encoding UTF8 $logPath
```

### 🌐 With API (logs POSTed to endpoint):

```powershell
Invoke-RestMethod -Uri "https://your-api.com/logs" `
  -Method POST `
  -Body ($data | ConvertTo-Json -Depth 5) `
  -ContentType "application/json"
```

---

## 📊 R Code (With & Without API)

### ✅ Without API (local log reading):

```r
data <- reactive({
  fromJSON("C:/GrillLogs/brisket_temp_log.json") %>%
    mutate(
      Risk_HCA = ifelse(TempF > input$tempThreshold & HCA_Signal > input$hcaThreshold, "HIGH", "OK"),
      Risk_PAH = ifelse(SmokeDensity > input$smokeThreshold & FatDripRate > input$dripThreshold, "HIGH", "OK")
    )
})
```

### 🌐 With API (pull JSON from remote source):

```r
data <- reactive({
  httr::GET("https://your-api.com/logs") %>%
    httr::content("text") %>%
    fromJSON() %>%
    mutate(...)
})
```

---

## 🌐 Free Cloud/API Integration Options

| Option                                                           | Use Case                                    |
| ---------------------------------------------------------------- | ------------------------------------------- |
| [Glitch.com](https://glitch.com)                                 | Host REST API endpoints for free            |
| [Render](https://render.com)                                     | Deploy API for pulling/pushing logs         |
| [GitHub Pages + Actions](https://pages.github.com)               | Host the dashboard + automate data          |
| [JSONBin.io](https://jsonbin.io)                                 | Simple JSON storage API                     |
| [Firebase Realtime DB (free tier)](https://firebase.google.com/) | JSON-based realtime backend                 |
| [Supabase](https://supabase.io)                                  | Full backend-as-a-service (Postgres + REST) |

---

## 🔎 Why This Matters

Food safety, fire prevention, and culinary consistency are now **data engineering problems**.

This project bridges:

* **IoT telemetry** (PowerShell logs)
* **Real-time alerting and dashboards** (RShiny)
* **Cloud-native readiness** for edge cooking devices, fire monitors, or health inspectors

Whether you’re an R developer, cloud architect, pitmaster, or public health student — BrisketSentinel turns logs into safety insights.

---

## 🧩 Conclusion

This repository is designed for:

* **Tinkerers** who love sensors and BBQ
* **Architects** who want API-ready designs
* **Teams** looking to extend PowerShell beyond scripts

Feel free to fork, modify, or deploy!

---

## 🐙 Author & Repo

**Repo**: [`brisketsentinel-cloud-ai`](https://github.com/your-username/brisketsentinel-cloud-ai)
**Maintainer**: [@emcdo411](https://github.com/emcdo411)

```

---

### ✅ Next Steps:
- Replace `"https://your-api.com/logs"` with a real endpoint if desired.
- Save as `README.md` in your repo folder.
- If you want badge links to render as icons inside GitHub, ensure the repo is public and Markdown is enabled (which it is by default).

Would you like help pushing this into your local GitHub repo or converting this into a GitHub Pages portfolio page?
```
