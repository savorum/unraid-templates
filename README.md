# Savorum for Unraid

Community Applications template for [Savorum](https://savorum.app/).
Uses `ghcr.io/savorum/savorum:documents` with bridge networking.

## Install

1. Find **Savorum** in Unraid's **Apps** tab and select **Install**.
2. Set **Server address** to the URL you use to open Savorum. Adjust **Web
   port** and **Appdata** if needed.
3. Select **Apply**, then open **WebUI** from the Docker tab.

## Settings

Advanced fields are under **Show more settings**. For other options, add a
**Variable** using the environment-variable name from the
[configuration reference](https://docs.savorum.app/admin/configure/) as its
**Key**.

Appdata maps to `/data`. Startup prepares its permissions, then runs Savorum
as `65532:65532` with no Linux capabilities. Keep the existing **Extra
Parameters** and **Post Arguments** when customizing.

## Documentation

[Accounts](https://docs.savorum.app/admin/accounts/) ·
[Single sign-on](https://docs.savorum.app/admin/single-sign-on/) ·
[Remote access](https://docs.savorum.app/admin/remote-access/) ·
[Backup and restore](https://docs.savorum.app/admin/backup-restore/) ·
[Get help](https://savorum.app/contact/)

## License

[LICENSE](LICENSE) is Savorum's GNU Affero General Public License v3.0.
Savorum's name and brand rights remain with their owners.
