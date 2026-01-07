# Webhook Scans API

## Overview

The Webhook Scans API is used to receive **patient scan data** from external systems (scanners / third-party vendors) into the **Dentist API** system.

This endpoint is **server-to-server (webhook)** and uses the application's standard response format.

---

## Base URL

```
https://dentist-api.sadigit.co.id
```

---

## Endpoint

```
POST v1/webhooks/scans/{doctor_id}/{event_type}
```
