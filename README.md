# TUWien Autologin

Automatically fills and submits TU Wien login forms, including authenticator codes. Works on desktop Firefox 140+, Firefox for Android 140+, and desktop Chrome 121+.

Firefox: [Firefox Add-ons (AMO)](https://addons.mozilla.org/de/firefox/addon/tu-wien-automatic-login/).  
Chrome: [GitHub Releases](https://github.com/ThomasW2005/tuwien-auto-login/releases/latest).

> [!CAUTION]
> Das ist alles komplett gevibecoded haha

## Install: Firefox on a computer / Android

Open [the Addon Store page](https://addons.mozilla.org/de/firefox/addon/tu-wien-automatic-login/) and install the extension.

## Install: Chrome on a computer

1. Download the file ending in **`-chrome.zip`** from [the latest release](https://github.com/ThomasW2005/TUWien-MFA-Autofill-Firefox/releases/latest) and extract it.
2. Open **`chrome://extensions`** and turn on **Developer mode**.
3. Click **Load unpacked** and select the extracted folder containing `manifest.json`.

Keep that folder on your computer. Do not select the ZIP itself or GitHub's “Source code” downloads. These steps follow [Chrome's installation guide](https://developer.chrome.com/docs/extensions/get-started/tutorial/hello-world#load-unpacked).

## Set up after installing

1. Open **TUWien Autologin** from your browser's extensions menu.
2. Enter your TU Wien username/email and password.
3. Paste your authenticator's **setup secret** or `otpauth://totp/...` URI. This is the secret from your MFA setup QR code, not the changing six-digit code. Leave it empty for password-only login.
4. If shown, click **Allow access to TU Wien websites** and approve.
5. Enable **automatic login**, click **Save settings**, and visit your usual TU Wien service, such as TISS.

Configure each browser/device separately. Settings are not synced. Leave custom selectors empty unless automatic detection fails. Keep your device clock synchronized.

A blank secret field preserves a previously saved secret. To remove it, select **Remove saved authenticator secret** and save. Push approval, SMS, CAPTCHA, passkeys and hardware security keys cannot be automated.

## Updates

**Firefox:** Versions installed from AMO receive updates through AMO automatically when add-on automatic updates are enabled. Checks normally run about once every 24 hours; restarting Firefox does not guarantee an immediate update. On desktop, check now with **`about:addons` → gear icon → Check for Updates**. The installed version appears on the extension's settings page. See [Mozilla's update guide](https://extensionworkshop.com/documentation/manage/updating-your-extension/).

**Chrome:** Download and extract the new Chrome ZIP into the same folder you originally loaded, replacing its files. Then click **Reload** for the extension at `chrome://extensions` and refresh TU Wien tabs. Unpacked Chrome extensions do not update through AMO.

Keep the extension installed to retain its settings. The current manifest uses ID `tuwien-auto-login@local.extension`. Previously distributed packages using `TUWien-MFA-Autofill-Firefox@ThomasW2005.github.io` are a separate extension: they cannot automatically update to this ID or transfer their saved settings. Users moving between these IDs must install the new extension, configure it again, and disable or remove the old one to avoid duplicate login attempts.

## Credential storage and behavior

See the [privacy policy](PRIVACY.md) for data handling and deletion details. German submission text for Chrome Web Store privacy fields is available in [CHROME_WEB_STORE.md](CHROME_WEB_STORE.md).
Credentials and the authenticator secret are saved in `browser.storage.local` in your browser profile, **without encryption**. The extension does not transmit them to external servers; it writes them into allowed login forms, which submit to TU Wien. Anyone who can read your profile can retrieve both factors. Storing both factors together reduces MFA's protection. This storage choice enables unattended login across browser restarts; there is no master-password prompt. See [Mozilla's storage documentation](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage).

- Only exact TU Wien domains and their subdomains over HTTPS are allowed. Names like `eviltuwien.at` and `tuwien.at.example.com` are excluded.
- Only top-level POST forms are automated; foreign form actions and submit destinations, password change/reset and enrollment forms are skipped.
- Automatic submission is limited to one attempt per login flow and stage per minute, up to three per ten minutes. SimpleSAML `AuthState` identifies each flow, so a new login after logout can submit immediately. Pages without `AuthState` share a limit per origin and stage. Autofill remains available when automatic submission is paused. Use **Reset retry limits** after fixing credentials if you want to try immediately.
- Codes with five seconds or less remaining are delayed until the next TOTP interval. Each code issued for automatic submission is reserved across tabs and login flows; another automatic login waits until the next interval rather than reusing it. Expired codes on forms that have not submitted are refreshed. Codes used manually or on another device are not tracked.
- Required consent fields and other browser form validation are respected.
- Disable automatic login before logging out if you want to stay logged out. Use **Delete credentials** to clear the stored configuration.

## Development and releases

Edit `extension/`; generated files in `dist/` are replaced by the build. Both browser packages share the same Manifest V3 manifest and code. Firefox uses background scripts; Chrome uses the service worker.

```sh
python3 scripts/build.py
node tests/extension.test.cjs
node tests/chrome-options.test.cjs
```

For temporary Firefox development, open `about:debugging#/runtime/this-firefox`, select **Load Temporary Add-on**, and choose `extension/manifest.json`. This installation ends when Firefox restarts. For Chrome development, load `dist/chrome` as an unpacked extension.

To publish a new release:

1. Increase the version in `extension/manifest.json` and build. Keep the add-on ID stable across releases and leave `browser_specific_settings.gecko.update_url` absent for AMO distribution.
2. Run the tests above and `web-ext lint --source-dir extension`.
3. Upload `dist/tuwien-auto-login-VERSION-firefox.xpi` to [Mozilla's Developer Hub](https://addons.mozilla.org/developers/) for **public distribution on AMO**. For subsequent releases, upload to the same add-on entry. The generated XPI is unsigned; AMO handles review, signing, hosting, and updates.
4. For the initial listing, complete the description, permissions explanation, privacy disclosures, and desktop/Android compatibility settings. Add the published listing URL to the Firefox installation instructions above.
5. Create GitHub release `vVERSION` and upload `dist/tuwien-auto-login-VERSION-chrome.zip` for Chrome users. An optional Firefox release asset must be the signed XPI downloaded from AMO, not the unsigned build output.
6. Verify installation on desktop Firefox and Firefox for Android, and test an update from an older signed version with the same ID using **Check for Updates**.

AMO distribution does not require a GitHub Pages site or a custom update manifest. However, existing self-distributed installations with a custom update URL continue checking that URL. To migrate those users automatically, preserve their original add-on ID and publish a final higher-version signed update through the old endpoint that removes `update_url`; later listed updates with that ID can come from AMO. Keep the old endpoint and migration download available for users who have not yet updated. The current ID change instead requires manual migration as described above. See [Mozilla's self-distribution update behavior](https://extensionworkshop.com/documentation/publish/self-distribution/).

The automated tests cover login behavior, TOTP, permissions, settings, and packaging with simulated browser APIs and login forms. Real browser/device checks are still needed for changes affecting TU Wien forms or mobile behavior. Full Mozilla linting can be run with `web-ext lint --source-dir extension` after installing `web-ext`.
