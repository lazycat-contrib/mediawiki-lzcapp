# MediaWiki (LazyCat LPK)

Wiki engine that powers Wikipedia.

- Upstream: https://github.com/wikimedia/mediawiki
- Image: `library/mediawiki:1.46.2` (official Docker Hub image, mirror mode, digest-matched)
- License: GPL-2.0 (full text in `content/licenses/COPYING`)
- Containers: MediaWiki + MariaDB 10.11

## Notes

- Version resolved with the Docker Hub API (`ordering=last_updated`); the registry
  `tags/list` endpoint truncates at 1000 entries and can report stale versions.
- MediaWiki's installer writes a `LocalSettings.php` that must end up at
  `/var/www/html/LocalSettings.php`. That path is inside the mounted
  `/lzcapp/var/html` volume so the file survives restarts; the usage text walks the user
  through placing it.
- Database connection is entered on the installer's database step (host `db`, db/user
  `mediawiki`, password from the deploy param); the admin account is created there too.
- `lzcapp/var/html` also holds the rest of the webroot, so upgrades and uploads persist.
- No mail service configured.
- Not yet verified on a real device.
