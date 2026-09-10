# Privacy Policy

**Last updated: September 10, 2026**

TechQuests.dev is committed to safeguarding the privacy of its users
and takes pride in offering robust privacy protections that set us
apart from other services. In an era where apps often gather extensive
personal information under the guise of being <em>“free”</em>,
TechQuests.dev stands firm in its dedication to user privacy.

This policy covers all apps published by TechQuests.dev. Where an app
has its own dedicated section below, that section describes its
specific data practices in detail — the general practices in this
section apply to any TechQuests.dev app not otherwise covered by a
dedicated section.

## General practices

### What information does TechQuests.dev collect?

By default, TechQuests.dev does not collect any information from
users. We do not employ tracking, metrics, or any other form of data
collection. The only exception involves minimal data collection
necessary to facilitate specific functionalities of the service you
choose to engage with.

For instance, when using TechQuests.dev, we may try to learn your
first name from your device to personalize your experience, such as
providing you the option to set a Player Name if applicable. Your
Player Name is flexible and can be changed at any time via the
settings menu. In cases where connectivity is necessary (e.g.,
multiplayer features), your current Player Name may be communicated to
our server solely for functional purposes. We ensure that data
temporarily stored during active sessions is deleted promptly upon
completion, typically within 30 minutes.

### How is this information used?

Any data collected by TechQuests.dev is solely for facilitating the
operations of our services. We do not retain this data beyond
necessary interaction and it is never shared with external parties or
used for any purpose other than enhancing your experience.

### What information is shared?

TechQuests.dev maintains a stringent policy that no user information
is shared with third parties under any circumstances, except as
described in an app's own dedicated section below. Our commitment to
privacy includes restricting data usage solely to support the
functionality you access directly through our services.

---

## UnKee Password Manager & UnKee Authenticator

Applies to: **UnKee Password Manager** (desktop, iOS, Android, and browser
extension) and **UnKee Authenticator** (desktop, iOS, and Android).

We built both apps around a simple principle: **your vault stays on your
device, encrypted with a password only you know.** This section explains
exactly what data each app collects, where it goes, and who else (if
anyone) sees it.

### 1. Your vault data

Both apps store your passwords / 2FA secrets in an encrypted database file
**on your own device**. That file never leaves your device unless you
explicitly turn on optional cloud sync (see below).

- **UnKee Password Manager** stores your entries in a standard **KeePass
  (.kdbx)** database file, encrypted with your master password.
- **UnKee Authenticator** stores your 2FA (TOTP) entries in its own
  encrypted vault file (Argon2id key derivation + authenticated
  ChaCha20-Poly1305 encryption), locked with your master password.

In both cases:
- **We never see your master password.** It is used only, on your device,
  to derive the encryption key for your vault.
- **We do not store a copy of your vault** unless you turn on cloud sync.
- If you forget your master password, nobody — including us — can recover
  your vault. There is no "reset password" for your vault contents.

### 2. Optional cloud sync

Cloud sync lets you back up your vault and access it from multiple
devices. **It is off by default and entirely optional.**

When you turn it on:

- **Your vault is encrypted on your device before it is uploaded.** Our
  sync server (a Cloudflare Worker) only ever stores the resulting
  encrypted, opaque file — it cannot read your vault contents, and it
  never receives your master password.
- **Sign-in uses a "magic link" sent to your email**, instead of a
  separate account password. To make that work:
  - We collect the **email address** you provide.
  - We store it **encrypted at rest**, alongside a one-way lookup hash
    used to find your account. Unlike your vault, your email address is
    **not end-to-end encrypted** — because our server has to be able to
    read it in order to email you a sign-in link, this piece of data is
    visible to us (though it is never shared for marketing, advertising,
    or any purpose other than authentication).
  - Emailing the sign-in link is handled by our email provider,
    **Resend** (resend.com), which receives your email address and the
    one-time sign-in link.
- We also store a small amount of **device metadata** needed to manage
  sync: a name you give the device (e.g. "Alice's MacBook"), the platform
  (iOS, Android, macOS, Windows, Linux, or browser extension), and
  timestamps of when it was added and last used. We temporarily use your
  **IP address** to rate-limit sign-in attempts and abuse; it is not
  stored long-term against your account.
- If you subscribe to a paid plan, **payment is handled by Polar.sh**, our
  payment processor. We never receive or store your card details —
  Polar's checkout page collects that directly.

If you delete your account, your account and devices are deactivated
immediately, and your synced vault data (and all of its history) is
**permanently deleted from our servers within 7 days**.

### 3. Biometric unlock (Face ID / Touch ID / Android biometrics)

Both apps let you unlock your vault with your device's biometric
authentication instead of typing your master password.

- **We never receive or process your fingerprint, face scan, or any other
  biometric data.** That is handled entirely by your operating system
  (Apple's Face ID / Touch ID, or Android's biometric APIs) — the app
  only ever receives a yes/no result from the OS.
- When you enable biometric unlock, your master password is stored using
  your device's OS-provided secure credential storage (e.g. macOS/iOS
  Keychain, Android Keystore), gated behind that same biometric check. It
  is not stored by us and never leaves your device.

### 4. Website/service icons (favicons)

To show a recognizable icon next to each saved login or 2FA entry, the
apps and the browser extension fetch a small icon for the site's domain
from **Google's favicon service**, and cache it locally afterward. Only
the **domain name** of the entry (e.g. "github.com") is sent for this
lookup — never your username, password, or any other vault contents.

### 5. Optional password breach check

UnKee Password Manager includes an optional security audit ("Watchtower")
that can check whether any of your saved passwords have appeared in known
data breaches. This check uses the **Have I Been Pwned** service's
privacy-preserving "k-anonymity" API: only the **first 5 characters of a
hash** of each password are sent, never the password itself or a full,
reversible hash of it. This check only runs when you use the security
audit feature.

### 6. The browser extension

The UnKee browser extension talks to the UnKee desktop app on your own
computer using the browser's native messaging API — a local connection,
not the internet. It does not make network requests to our servers. The
one exception is the same favicon lookup described above, which loads
site icons directly from Google's favicon service for display in the
extension popup.

### 7. Third parties we use

We only share data with a third party when it's necessary to provide the
feature you're using:

| Third party | What it receives | Why |
|---|---|---|
| **Resend** (resend.com) | Your email address, one-time sign-in link | Sends cloud-sync magic-link sign-in emails |
| **Polar.sh** | Your user ID and, if you choose to enter it, your email; your payment details go directly to Polar, not to us | Processes subscription payments for paid plans |
| **Google** (favicon service) | Domain names of your saved sites | Fetches website icons shown next to entries |
| **Have I Been Pwned** | First 5 characters of a password hash (only if you run a breach check) | Checks passwords against known breach data |
| **Cloudflare** | Your encrypted vault blob and account/device metadata (if cloud sync is enabled) | Hosts our sync backend (Workers, D1 database, R2 storage) |

We do **not** use any analytics, advertising, or crash-reporting SDKs in
either app — verified directly in the source code.

### 8. App permissions

**UnKee Authenticator** requests:
- **Camera** — to scan QR codes when adding a new 2FA entry
- **Biometric authentication** (Face ID / Touch ID / Android biometrics) —
  for optional vault unlock
- **Internet** — only used for cloud sync (if enabled) and fetching site
  icons

**UnKee Password Manager** requests:
- **Biometric authentication** — for optional vault unlock
- **Autofill / Credential Provider service** (Android AutofillService,
  iOS/macOS Credential Provider Extension) — to fill your saved logins and
  passkeys into other apps and websites, only when you choose an entry
- **Internet** — only used for cloud sync (if enabled), fetching site
  icons, and payment/subscription management

Neither app requests access to your contacts, location, microphone, photo
library, or SMS messages.

### 9. Your choices and rights

- **Local vault**: you fully control your vault file. You can view,
  export, back up, or permanently delete it at any time from within the
  app or directly on your file system.
- **Cloud sync data**: you can disconnect and delete a specific device
  from your account, or delete your entire cloud account (which deletes
  your synced vault, its history, and device list from our servers within
  7 days) from within the app's account settings.
- **Email address**: deleting your account deletes the associated email
  address from our systems within the same 7-day window.
- To request help with any of the above, or to ask what data we hold
  about you, contact us (see below).

### 10. Children's privacy

Neither app is directed at children, and we do not knowingly collect
personal information from children.

---

## Contact us

Should you have any questions or require further clarification about our
privacy practices, contact us at:

**privacy@techquests.dev**

We are dedicated to ensuring your privacy is protected and respected at
all times.

## Changes to this policy

We may update this policy as our apps change. We'll update the "Last
updated" date above when we do. Material changes affecting cloud sync or
third-party data sharing for a specific app will be called out in that
app or via email to its sync users.
