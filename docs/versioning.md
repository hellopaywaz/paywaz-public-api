# Paywaz API Versioning & Deprecation Policy

## Versioning Model

Paywaz uses date-based API versions in the format:

YYYY-MM-DD

Example:
2025-01-01

API versions are supplied via the `Paywaz-Version` HTTP header.

If no version is supplied, the account's default pinned version is used.

---

## Backward Compatibility

- All API versions are immutable once released
- New fields may be added at any time
- Existing fields will never change meaning within a version

---

## Deprecation Policy

When an API feature is deprecated:

1. The feature is marked as deprecated in OpenAPI
2. A `Paywaz-Deprecation` response header is returned
3. The feature remains available for **at least 6 months**
4. Removal occurs only in a new API version

---

## Webhooks

Webhooks are versioned independently using `eventVersion`.

Webhook schemas will never change without a version bump.
