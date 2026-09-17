# Domain, Subdomain & Search Operations Reference

Use this reference for projects moving from a development URL to a real domain and for sites where search discoverability matters.

The supplied video demonstrates a practical domain setup with separate roles for the public website, application, email, and marketing/news content, plus sitemap submission and Search Console verification.

## Domain architecture

Audit the domain structure and document the purpose of each host that exists.

Common patterns include:

- `www` or apex/root domain for the public website
- `app` for an authenticated application when separation is useful
- `mail` or provider-managed mail infrastructure for email
- `news` or another dedicated content host when a separate content property is intentional

Do not create subdomains just because they look professional. Every host should have a real purpose, correct DNS, appropriate TLS, and an owner.

## DNS checks

When DNS configuration is available, verify:

- records point to the intended current service
- no decommissioned or unclaimed service remains referenced
- A/AAAA/CNAME records match the deployment architecture
- mail-related records are intentional and controlled
- HTTPS certificates cover every public hostname
- redirects between apex, `www`, and application hosts are intentional
- canonical URLs do not conflict across hosts

Never use DNS names or provider IPs as assumptions. Inspect the actual project/provider configuration when possible.

## Public vs authenticated hosts

If the product separates a marketing site and authenticated app:

- keep public marketing pages crawlable when intended
- keep authenticated/private application routes out of search indexing
- do not use `robots.txt` as access control
- enforce authentication server-side for private resources
- avoid leaking private URLs, metadata, or user data through public pages

## Sitemap operations

For public sites:

- generate a valid `sitemap.xml`
- include intended public canonical URLs
- exclude authenticated/private pages
- avoid duplicate or parameter-heavy URLs unless intentionally canonical
- keep the sitemap synchronized with real routes
- submit the sitemap through the site's chosen search-engine tooling when the owner controls it

A sitemap is a discovery aid, not a guarantee that a URL will be indexed.

## Search Console

When the owner controls the property, verify that the correct production domain/property is configured and the sitemap is submitted successfully.

Do not mark Search Console setup as repository-verified unless the required external evidence is available.

## Verification

Check:

1. Every public hostname resolves to the intended service.
2. Every public hostname uses HTTPS.
3. Redirect and canonical behavior is intentional.
4. Private application pages require authentication and are not exposed through public indexing paths.
5. Sitemap contains only intended public URLs.
6. Search tooling is connected to the correct production property where external access is available.
