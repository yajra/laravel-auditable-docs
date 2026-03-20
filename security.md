---
title: "Security"
description: "Security policy for Laravel Auditable."
---

# Security

If you discover any security related issues, please email [aqangeles@gmail.com](mailto:aqangeles@gmail.com) instead of using the issue tracker.

Please include the following information:

- A clear description of the security issue
- Steps to reproduce the issue
- Any potential fixes or mitigations you've identified

We will work with you to address the issue promptly.

<a name="best-practices"></a>
## Best Practices

When using Laravel Auditable, consider these security practices:

- **Protect audit columns**: Ensure `created_by`, `updated_by`, and `deleted_by` columns are not mass-assignable
- **Validate user input**: Always validate that the authenticated user is authorized to perform actions
- **Use policies**: Consider using Laravel Policies to control who can create, update, or delete records
