# Apache2 Paywall Configuration

This repository provides a robust, server-level paywall solution for websites hosted on Apache2. It is designed for scenarios where you need to enforce payment or restrict access, even when the website is managed by a non-technical client who has access to the CMS (such as WordPress) but **not** to the raw server configuration.

## Why Use This?

- **CMS-Independent Enforcement:** The paywall is injected at the Apache2 configuration level, making it impossible for clients to bypass by editing website files or CMS settings.
- **Client-Proof:** Only those with access to the server's Apache configuration can disable or modify the paywall, ensuring compliance with payment or contractual terms.
- **No Code Changes Required:** Works with any CMS or static site, as it operates outside the application layer.

<img width="1170" height="2532" alt="IMG_7822_export" src="https://github.com/user-attachments/assets/be9aeb13-606c-4b73-a141-00642ceb0cc9" />

## How It Works

- The paywall is implemented by modifying the Apache2 virtual host configuration (e.g., `000-default.conf`).
- A CSS banner (`banner.css`) and optional HTML are injected into all served pages, overlaying a payment notice or restriction message.
- All requests are intercepted and the paywall content is served unless payment is received or the restriction is lifted by editing the server config.

## Files in This Repo

- `000-default.conf`: Example Apache2 virtual host configuration with paywall injection logic.
- `banner.css`: CSS for styling the paywall banner/overlay.
- `README.md`: This documentation.

## Setup Instructions

1. **Backup Your Existing Config:**
   ```bash
   sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf.bak
   ```

2. **Replace Apache Config:**
   - Copy the provided `000-default.conf` to your server's `/etc/apache2/sites-available/`.
   - Adjust paths and domain names as needed for your environment.

3. **Add Paywall Assets:**
   - Place `banner.css` (and any referenced HTML/images) in a web-accessible directory.
   - Update the config to point to the correct asset locations.

4. **Reload Apache:**
   ```bash
   sudo systemctl reload apache2
   ```

5. **Test the Paywall:**
   - Visit your site in an incognito window to verify the paywall is active.

## Customization

- **Banner Content:** Edit the HTML/CSS in the config and `banner.css` to change the paywall message, branding, or style.
- **Bypass/Disable:** Only users with server access can comment out or remove the paywall logic in the Apache config.

## Security Note

This approach is intended for situations where you need to enforce payment or contractual terms and the client has access to the CMS but **not** to the server configuration. If the client gains server-level access, they can remove the paywall.

## License

MIT License

---

**Author:** [alexander-wei](https://github.com/alexander-wei)
