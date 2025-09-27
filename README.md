
  CHANGELOG.en.md
  - English-first changelog mirroring the project's bilingual changelog
  - Keep 'Unreleased' at top, then historical releases in descending order
  - Use categories: Added, Changed, Fixed, Security
# Changelog

All notable changes to Mythic X Professional are documented here.

This file follows the Keep a Changelog format and the project follows Semantic Versioning.

## [Unreleased]

### Added
- In-app update checker with streamed download progress (improved reliability for presigned/private URLs)
- Settings: manual "Check for updates" and download hooks

### Changed
- Updater shows a single final in-app toast when already up-to-date (removed transient "Checking..." toast)
- Version comparison normalized to handle `v` prefixes and prerelease labels

### Fixed
- Analyzer and async BuildContext issues related to dialogs/notifications

---

## [1.2.0] - 2025-09-27

### Added
- Admin endpoints for publishing update metadata (version, installer URL, release notes, checksum)
- PowerShell/VBScript helper for invisible restart and in-place replacement on Windows
- Support for optional HTTP headers when downloading installers (presigned/private URLs)

### Changed
- Improved download progress heuristics for chunked/unknown-length responses
- Updater API: explicit "no update" return and guaranteed in-app notification for latest-version cases
- Documented `build_and_release.yml` workflow in repo docs

### Fixed
- Version comparison edge cases (handles `1.2.3-beta`, `v1.2.3`, etc.)
- Multiple static analyzer warnings fixed in update and notify modules

---

## [1.1.0] - 2025-08-10

### Added
- Dashboard and authentication flows (Login/Register/Google) with sample data

### Changed
- UI improvements and theme refinements

---

## [1.0.0] - 2025-05-18

### Added
- Initial public release

---

## Release checklist & tips

1. Bump the app version in `pubspec.yaml` and regenerate `lib/generated_version.dart`:

```powershell
# Windows (PowerShell)
powershell -ExecutionPolicy Bypass -File .\\scripts\\gen_version.ps1

# Unix
./scripts/gen_version.sh
```

2. Move Unreleased entries into the new release heading and add the release date.

3. Commit and tag the release:

```powershell
git add CHANGELOG.md pubspec.yaml lib/generated_version.dart
git commit -m "chore(release): 1.2.0"
git tag -a v1.2.0 -m "Release v1.2.0"
git push origin main --follow-tags
```

4. Create a GitHub Release and upload artifacts (use `gh` or the web UI):

```powershell
gh auth login
gh release create v1.2.0 path\\to\\artifact.exe -t "v1.2.0" -n "Release notes"
```

If you want, I can prepare `lib/generated_version.dart` and open a release branch containing only build/release files. Tell me whether to commit and push the changelog now.
