# Privacy & Legal Readiness Reference

Use this reference when auditing a website or web app for privacy, consent, content-trust, accessibility, and basic legal-readiness gaps.

This checklist is derived from the project's supplied reference material. It is an engineering/product-readiness checklist, not legal advice. Requirements vary by jurisdiction, product, audience, data collected, and business model.

## 20 checks

1. Privacy policy is present and appropriate to the product and data collected.
2. Terms of service are present where appropriate.
3. Refund/cancellation policy is present where the product sells paid goods or services.
4. Cookie policy or equivalent cookie/tracking disclosure is present where applicable.
5. Cookie consent banner is implemented where consent is legally required.
6. Forms explain and obtain required consent before collecting data.
7. No unnecessary personal data is collected.
8. Third-party SDKs are inventoried and audited for the data they receive.
9. Dark patterns are removed from consent, subscriptions, checkout, cancellation, and other consequential flows.
10. Hidden fees or material charges are not concealed until late in the purchase flow.
11. Fake reviews/testimonials are removed.
12. Unsupported claims are removed or replaced with claims the product can substantiate.
13. Accessibility alt text is present and meaningful where images need it.
14. Color contrast is sufficient for readable content and controls.
15. Keyboard navigation works for interactive flows.
16. Business/contact details are visible where users reasonably need them.
17. Age/parental consent requirements are considered when collecting children's data.
18. Marketing emails include a working unsubscribe mechanism where required.
19. Fonts, images, illustrations, music, video, and other third-party assets have appropriate licenses/permissions.
20. Users have a supported process for requesting deletion of their personal data where applicable.

## Audit behavior

For each check:

- Verify the actual implementation and relevant product flow.
- Distinguish required consent from merely displaying a disclosure.
- Do not invent legal obligations for a jurisdiction that has not been established.
- If the repository cannot establish whether an external/legal requirement applies, mark the engineering check UNKNOWN and state what must be confirmed.
- Do not treat a generic privacy-policy template as proof that the product's actual data practices are compliant.
- For data deletion, verify both the request interface/process and the backend deletion or retention behavior where the product controls it.
- For third-party SDKs, inspect network requests, initialization code, consent gates, and documented data collection where available.

## Trust and claim integrity

Privacy/legal readiness overlaps with product trust. Flag:

- fabricated reviews, ratings, customer counts, awards, logos, case studies, or metrics
- unsupported guarantees or performance claims
- misleading pricing or fees
- manipulative cancellation or consent UX
- contact details that are presented as real but are placeholders

A clean legal page does not compensate for deceptive product behavior elsewhere.
