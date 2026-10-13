# Publish Savorum to Community Applications

This repository owns Savorum's Unraid template, listing, and installation
guide. The [application repository](https://github.com/savorum/savorum)
owns the container image.

## Release and submit

1. **Check the released image.** The template uses the public
   `ghcr.io/savorum/savorum:documents` image. Its startup command uses the
   image's shell and `setpriv` to prepare appdata and drop privileges.

   ```sh
   docker buildx imagetools inspect ghcr.io/savorum/savorum:documents
   docker run --rm --entrypoint /bin/sh ghcr.io/savorum/savorum:documents -ec 'command -v bash; command -v chown; command -v chmod; command -v setpriv'
   ```

   Confirm runtime entries for `linux/amd64` and `linux/arm64`, excluding
   attestation manifests. Check anonymous access without saved credentials:

   ```sh
   registry_check_dir="$(mktemp -d)"
   docker --config "$registry_check_dir" manifest inspect ghcr.io/savorum/savorum:documents
   rmdir "$registry_check_dir"
   ```

2. **Validate the template:**

   ```sh
   xmllint --noout ca_profile.xml templates/savorum.xml
   ```

   Complete the Unraid checks below with the released image. Check that the
   icon, screenshots, README, support page, and documentation open without
   signing in. Use a square, opaque icon; Community Applications supplies the
   corner treatment.
3. **Publish this repository's changes.** Keep the repository public and
   unarchived, with its root license and profile.
4. **Validate, Scan, and submit for review** through the
   [submission portal](https://ca.unraid.net/submit/new). Resolve findings
   before submitting. Repeat Validate and Scan after meaningful template
   edits.

See the [submission help](https://ca.unraid.net/submit/help),
[repository format](https://ca.unraid.net/submit/help/repository-xml),
[profile format](https://ca.unraid.net/submit/help/repository-info-xml), and
[field reference](https://ca.unraid.net/submit/help/xml-field-reference).

## Unraid checks

- Install with a fresh appdata path and a free web port. Confirm that startup
  prepares the folder without terminal commands, the server runs as
  `65532:65532`, and WebUI opens from another LAN device.
- Confirm that **Show more settings** is collapsed. Test authentication after
  administrator creation and adding a variable from the configuration reference.
- Open **Console** and run `savorum --help` in Bash. Check that startup creates
  `.cache/savorum/typst` in appdata without a cache warning.
- Add a recipe and photo. Restart, then recreate the container with the same
  appdata folder. Confirm the library persists and shutdown completes cleanly.
- Back up to separate storage and restore into an empty test folder. Verify
  the backup and open the restored recipe and photo. Preserve webhook keys
  according to the recovery guide.
- Apply an update from the Docker tab. Check health, recipes, and photos.
  Use a backup and its compatible image for recovery; database downgrades
  are not supported.
- If using a proxy, test HTTPS, **Server address**, **Trusted proxies**, and
  sign-in. Check Unraid autostart and shutdown if enabled.
