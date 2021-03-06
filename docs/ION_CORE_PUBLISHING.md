# Ion Core Extension Publishing HOWTO

## Getting started

Since the core extension requires special Firefox-only privileges, it must use the Mozilla signing infrastructure.
This requires that the github repo is cloned to the `github.com/mozilla-extensions` organization, and have a working `.taskcluster.yml` file in the repository.

The Mozilla Taskcluster CI will then automatically start working for this new clone.

NOTE - this must be a clone and not a fork (TODO - file/link to bug on TC side about this?)

## Finding the QA-signed extension

Taskcluster CI output can be found in GitHub Actions:
https://github.com/mozilla-extensions/ion-core-addon/runs/1249808119

The "dep-signing-ion_core" task will link to the completed build on Taskcluster:
https://firefox-ci-tc.services.mozilla.com/tasks/ZcZWnI5pT4K_1ycCX3l7iw

Click the "Artifacts" link to find a link to the signed XPI `public/build/ion_core.xpi`.

## Testing the QA-signed extension

To test the QA-signed extension in Firefox, you must be running the Nightly release or an unbranded build (there are equivalents for Release and Beta), then navigate to `about:config` and create a new boolean pref named `xpinstall.signatures.dev-root` and set it to `true`.

NOTE - this will cause production-signed extensions (such as those from addons.mozilla.org) to not load. To allow these, set `xpinstall.signatures.required` pref to `false`.

## Producing a production-signed extension

Production signing requires sign-off from addons and releng.
See the #addon-pipeline channel on Slack for assistance.

## Publishing the Ion Core Extension

TODO - for now we are publishing the signed XPI as a github release, but in the future it will move to https://addons.mozilla.org
NOTE - if the extension is *not* hosted on addons.mozilla.org, then an alternative update URL must be specified in the `manifest.json` so do this before publishing! https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/browser_specific_settings#Firefox_Gecko_properties

Upload the signed extension to a github release, and point "Install" button on the static site in `docs/index.html` at the github release. An example of this would be:
https://github.com/mozilla-ion/ion-core-addon/releases/download/2.1/ion_core-2.1.xpi

## Updating the Core Extension

Push to the `github.com/mozilla-extensions` clone, and refer to the [Finding the QA-signed extension](#finding-the-qa-signed-extension) and subsequent sections.
