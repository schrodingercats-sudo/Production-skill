# Consumer Risk & Product Trust Reference

Use this reference for products that collect personal data, sell subscriptions, accept payments, host user uploads, or provide AI-generated guidance.

The supplied video uses deliberately exaggerated hypothetical costs to illustrate product failures. Production Pup must treat the underlying patterns as risks, not repeat the video's dollar amounts as predicted liability.

## Risk patterns to audit

### 1. Privacy policy does not match reality

Check whether the privacy documentation accurately describes:

- data actually collected
- analytics and tracking
- AI/model processing where relevant
- third-party data processors or SDKs
- user uploads and storage
- retention/deletion behavior

A privacy policy that omits actual collection or processing should be flagged for correction and appropriate legal review.

### 2. User uploads are not actually deletable

If the product promises deletion:

- provide a real deletion path where applicable
- verify backend/storage deletion behavior
- inspect object storage, database records, thumbnails, derived files, and backups/retention where controlled by the product
- explain any retention that is required or technically unavoidable

Do not claim deletion is complete if only the UI record is removed.

### 3. Public storage buckets

Audit object storage permissions. User uploads should not become publicly readable merely because a bucket or object policy was convenient during development.

Verify:

- private objects remain private
- authorization is checked before access
- signed URLs expire when appropriate
- object names are not treated as authorization
- deletion and retention rules match the product's promises

### 4. Fake testimonials and trust claims

Remove fabricated testimonials, reviews, customer stories, logos, metrics, certifications, or endorsements. Replace them with real evidence or remove the section.

### 5. Difficult cancellation

For subscriptions:

- cancellation should be discoverable
- the flow should not intentionally create unnecessary friction
- the user should understand when access ends and whether another charge will occur
- cancellation state should be confirmed

Do not hide cancellation behind unrelated support requests unless there is a genuine product reason and applicable requirements are satisfied.

### 6. Auto-renewal and trial transitions

Audit free trials and subscriptions for:

- clear price after trial
- billing frequency
- renewal behavior
- required notices/reminders where applicable
- clear cancellation path
- confirmation of subscription state

Do not invent jurisdiction-specific legal requirements. Flag the flow for legal review when applicability is uncertain.

### 7. High-risk AI responses

If the product gives health, financial, legal, safety, or other high-consequence guidance:

- do not present generated output as guaranteed professional advice
- disclose material limitations where appropriate
- avoid unsupported certainty
- provide appropriate escalation or emergency guidance when the product context requires it
- keep high-risk actions behind appropriate user confirmation and permissions
- log and monitor failures according to the product's risk model

The engineering audit should identify unsafe behavior without making a legal conclusion about liability.

## Evidence rules

For every finding:

- identify the actual product behavior
- cite the relevant code/configuration or external evidence
- distinguish an engineering defect from a legal question
- do not repeat hypothetical monetary penalties as facts
- recommend legal review when jurisdiction-specific applicability cannot be established

This reference is a product-risk checklist, not legal advice.
