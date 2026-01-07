# Webhook Scans API

## Overview

The Webhook Scans API is used to receive **patient scan data** from external systems (scanners / third-party vendors) into the **Dentist API** system.

This endpoint is **server-to-server (webhook)** and uses the application's standard response format.

---

## Base URL

```
https://dentist-api.sadigit.co.id
```
```json
{
    "platform": "dmeu2",
    "env": "production",
    "service": "monit",
    "event_id": 526143558,
    "creation_date": 1717614661,
    "type": "PlanningScanPublished",
    "about":
    {
        "user_type": "public",
        "role": "patient",
        "id": 635567,
        "_links":
        {
            "self": "https://gateway.eu2.dental-monitoring.com/api/v2/patients/635567",
            "events": "https://gateway.eu2.dental-monitoring.com/api/v2/patients/635567/events"
        }
    },
    "by":
    {
        "user_type": "service"
    },
    "resource":
    {
        "type": "scan",
        "url": "https://gateway.eu2.dental-monitoring.com/api/v2/scans/20629156"
    },
    "_links":
    {
        "self": "https://gateway.eu2.dental-monitoring.com/api/v2/events/526143558"
    }
}```
---

## Endpoint

```
POST v1/webhooks/scans/{doctor_id}/{event_type}
```
