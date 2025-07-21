Mochi Health Documentation: Review Befor Subscription
====================================

.. meta::
   :description: Official documentation for developers integrating with the Mochi Health platform. Learn how to authenticate, access API endpoints, manage user workflows, and implement virtual obesity care solutions.

.. image:: jit.png
   :width: 250px
   :align: center
   :alt: Mochi Health Developer Portal


Overview
--------

**Mochi Health** provides a virtual obesity treatment platform that offers telehealth services, insurance assistance, and GLP-1 prescription management. This documentation is intended for developers, healthcare partners, and organizations integrating with Mochi’s API to enable eligibility checks, onboarding workflows, and medication management.

Key features of the Mochi API:

- User eligibility assessment
- Secure virtual visit scheduling
- Insurance verification & prior authorization automation
- Prescription issuance and refill tracking
- Integration with compounding pharmacy networks

Getting Started
---------------

To use the Mochi Health API, you must request API credentials from our [developer onboarding team](mailto:dev@mochihealth.com). Once approved, you'll receive:

- A `Client ID` and `Client Secret`
- Access to sandbox and production environments
- Rate limits and authentication scopes

Authentication
--------------

Mochi uses **OAuth 2.0 Client Credentials Flow** to authenticate server-to-server API calls.

Example Token Request:

.. code-block:: bash

   curl -X POST https://api.mochihealth.com/oauth/token \
     -H "Content-Type: application/json" \
     -d '{
       "client_id": "YOUR_CLIENT_ID",
       "client_secret": "YOUR_CLIENT_SECRET",
       "grant_type": "client_credentials"
   }'

Successful Response:

.. code-block:: json

   {
     "access_token": "eyJhbGciOi...",
     "token_type": "Bearer",
     "expires_in": 3600
   }

Use the access token in the Authorization header:

.. code-block:: http

   Authorization: Bearer <access_token>

Eligibility Check API
----------------------

This endpoint determines if a user qualifies for a GLP-1-based treatment plan.

**Endpoint:**

``POST /v1/eligibility/check``

**Request Body:**

.. code-block:: json

   {
     "age": 34,
     "bmi": 32.5,
     "comorbidities": ["hypertension"],
     "state": "CA"
   }

**Response:**

.. code-block:: json

   {
     "eligible": true,
     "recommended_plan": "GLP1_standard",
     "requires_physician_review": false
   }

Scheduling a Virtual Visit
--------------------------

Use this endpoint to generate a virtual visit link for a patient.

**Endpoint:**

``POST /v1/appointments/schedule``

**Payload:**

.. code-block:: json

   {
     "patient_id": "user_345",
     "preferred_time": "2025-07-25T14:00:00Z",
     "visit_type": "initial"
   }

**Response:**

.. code-block:: json

   {
     "appointment_id": "appt_9823",
     "join_url": "https://visit.mochihealth.com/join/appt_9823"
   }

Prescription Management
-----------------------

Use the `prescriptions` endpoint to view or initiate prescription workflows.

**GET /v1/prescriptions/:patient_id**

**POST /v1/prescriptions/new**

Include information such as dosage, medication type, and compounding preferences. Mochi will handle insurance authorization if applicable.

Webhooks
--------

Mochi Health supports webhooks for real-time updates on:

- Appointment confirmations
- Eligibility changes
- Prescription status updates
- Insurance decision events

To register a webhook:

.. code-block:: json

   {
     "event": "prescription.approved",
     "url": "https://yourdomain.com/webhooks/mochi"
   }

Security and Compliance
-----------------------

All endpoints are HIPAA-compliant and enforce strict security headers and token validation.

- OAuth 2.0 with short-lived tokens
- TLS 1.2 or higher required
- All patient data encrypted at rest (AES-256)

Support and Contact
-------------------

For support during development or integration:

- **Email:** devsupport@mochihealth.com
- **Docs Repo:** https://github.com/mochihealth/dev-docs
- **API Status:** https://status.mochihealth.com
- **Production URL:** https://api.mochihealth.com

License
-------

This documentation and API are © 2025 Mochi Health. All rights reserved.

