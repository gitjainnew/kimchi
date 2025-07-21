Mochi Health Platform Documentation
===================================

.. meta::
   :description: Technical documentation for the Mochi Health platform, including eligibility logic, virtual visit workflows, and medication program operations.

Overview
--------

This documentation describes the internal logic, eligibility flow, and service infrastructure of the **Mochi Health Virtual Obesity Care Platform**. It is intended for developers, clinical operations teams, and healthcare administrators integrating or managing services within the Mochi Health system.

Platform Goals:

- Support obesity management through remote care delivery
- Enable access to GLP-1 medications via clinical evaluation
- Automate eligibility screening, scheduling, and prescription workflows

Eligibility Logic
-----------------

The platform determines eligibility for GLP-1 treatment using the following criteria:

- **Age ≥ 18**
- **BMI ≥ 30**, or **BMI ≥ 27** with comorbid conditions:
  - Type 2 Diabetes
  - Hypertension
  - Hyperlipidemia

.. note::
   Mochi does not currently operate in Alabama.

The eligibility engine takes the following inputs:

.. code-block:: json

   {
     "age": 32,
     "bmi": 29.7,
     "conditions": ["hypertension"],
     "state": "NY"
   }

If conditions are met, the user is approved for clinical intake.

Virtual Care Workflow
---------------------

The standard care workflow includes the following steps:

1. **Screening**  
   A user completes a web-based questionnaire capturing demographics, health status, and history.

2. **Virtual Consult**  
   Users are matched with licensed physicians for real-time consultations. All visits occur via HIPAA-compliant video.

3. **Medication Evaluation**  
   The physician determines if a GLP-1 is clinically appropriate. If approved, a prescription is issued.

4. **Insurance Handling**  
   The platform handles prior authorization with the payer or offers compounding alternatives if uninsured.

5. **Ongoing Management**  
   Patients receive monthly check-ins, side effect management, and coaching through an assigned care team.

Medication Support
------------------

Mochi supports both name-brand and compounded GLP-1 medications. Approved drugs include:

- **Wegovy**
- **Ozempic**
- **Zepbound**

The system integrates with partner pharmacies for fulfillment and refill scheduling.

Insurance Integration
---------------------

The platform integrates with third-party insurance APIs to automate:

- Prior authorization submission
- Re-authorization for renewals
- Denial appeals (where permitted)

Users can proceed with self-pay if no coverage is available. Compounded options range from **$199 to $250/month**, significantly lower than commercial list prices.

Technical Notes
---------------

- All services are hosted in a HIPAA-compliant cloud environment.
- API access uses token-based OAuth 2.0.
- Logging and auditing are enforced per healthcare regulatory requirements.

Troubleshooting & FAQs
----------------------

**Q: What happens if a user is denied insurance coverage?**  
A: They are offered a compounded medication alternative and notified in the patient dashboard.

**Q: How long does it take to start treatment?**  
A: Onboarding and consults are typically completed within 7–10 business days.

**Q: Can a user opt out of monthly care?**  
A: Yes, users can cancel membership from their dashboard anytime. Active treatment ends after physician review.

License and Contact
-------------------

All contents © 2025 Mochi Health Platform. Internal documentation only.

For technical issues, contact the operations team via internal support channels.

