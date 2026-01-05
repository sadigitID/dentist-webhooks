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
POST v1/webhooks/scans/{patient_id}
```

---

## Description

This webhook endpoint is used to receive **scan update notifications** from an external manufacturing or scanning system.

The system validates the webhook signature, locates the active case for the given patient, records an activity log, and processes the scan update.

---

## Path Parameters

| Parameter  | Type   | Required | Description       |
| ---------- | ------ | -------- | ----------------- |
| patient_id | string | Yes      | Unique patient ID |

**Example**

```
v1/webhooks/scans/605914
```

---

## Request Headers

| Header              | Value                   | Required | Description                                  |
| ------------------- | ----------------------- | -------- | -------------------------------------------- |
| Content-Type        | application/json        | Yes      | Request payload format                       |
| X-Webhook-Signature | sha256=<HMAC_SIGNATURE> | Yes      | HMAC SHA256 signature for request validation |

> Add Authorization header or signature if the webhook is secured.

---

## Request Body

Send a JSON object containing the scan information.

**Example**

```json
{
  "scan_id": 1
}
```

---

## Success Response

**HTTP Status:** `202 Accepted`

```json
{
  "status": true,
  "message": "Scan update processed successfully",
  "data": {
    "patient_id": "605914",
    "case_number": "CASE-2025-0001"
  }
}
```

---

## Response Format Standard

All successful responses follow this format:

```json
{
  "status": true,
  "message": "string",
  "data": "any"
}
```

---

## Error Responses

### 400 Bad Request – Missing Signature

```json
{
  "status": false,
  "message": "Missing webhook signature",
  "data": null
}
```

### 401 Unauthorized – Invalid Signature

```json
{
  "status": false,
  "message": "Invalid webhook signature",
  "data": null
}
```

### 404 Not Found – Case Not Found

```json
{
  "status": false,
  "message": "Case With Patient ID not found",
  "data": null
}
```

### 500 Internal Server Error

```json
{
  "status": false,
  "message": "Internal server error",
  "data": null
}
```

---

## Notes

- This endpoint is for webhook use only (not for frontend/public clients)
- Recommendations:
  - IP Whitelisting
  - Signature / Token Validation
  - Payload logging for audit purposes
- `patient_id` **must** be sent via the URL path

---

## Example cURL

```bash
curl -X POST \
  https://dentist-api.sadigit.co.id/v1/webhooks/scans/605914 \
  -H "Content-Type: application/json" \
  -H "X-Webhook-Signature: sha256=<HMAC_SIGNATURE>" \
  -d '{"scan_id":1}'
```

---

## Changelog

| Version | Date       | Description             |
| ------- | ---------- | ----------------------- |
| 1.0.0   | 2025-01-01 | Initial webhook release |