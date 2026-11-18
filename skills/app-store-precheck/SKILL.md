---
name: app-store-precheck
description: Check an iOS or Android app or game against Apple App Review Guidelines and Google Play policy before you submit it. Covers completeness, metadata, privacy labels and Data safety, tracking consent, in-app purchases, ads, accounts, kids, permissions and store account setup. Use for "check before submission", "will this pass review", "App Store compliance", "Play Store policy check", or before a TestFlight external, App Store or Play production release.
---

# App Store and Google Play precheck

Goal: find the problems a store reviewer would find, before you submit.

Look at three things: the code and build, the store console (App Store Connect or Play Console), and the store listing.
Give every item one result:

- PASS: say how you verified it (file and line, screen, console page).
- FAIL: say what to change.
- NOT CHECKED: say why (no access, needs a device, needs the owner).
- NOT APPLICABLE: say why (for example, the app has no accounts).

Never mark PASS without looking. If you cannot see the console, ask the user for a screenshot or mark NOT CHECKED.

## Sources and freshness

This checklist was written on 2026-11-18 from these official pages:

- Apple App Review Guidelines, https://developer.apple.com/app-store/review/guidelines/ (last updated 2026-10-16)
- Apple App Privacy details, https://developer.apple.com/app-store/app-privacy-details/
- Apple account deletion, https://developer.apple.com/support/offering-account-deletion-in-your-app/
- App Store Connect Help: app information, age ratings, in-app purchase submission, EU Digital Services Act trader requirements
- Google Play Developer Program Policy, https://play.google/developer-content-policy/
- Play Console Help: Data safety (answer/10787469), User Data (answer/9888076), Payments (answer/9858738), Ads (answer/9857753), Metadata (answer/9898842), testing for new personal accounts (answer/14151465)

Store rules change often. Before you base a decision on a guideline number, limit or date, open the official page and check it. Say in the report which items you re-checked. Guideline numbers below are Apple's unless marked "Play".

This skill is not affiliated with or endorsed by Apple or Google.

## 1. Build works and is complete

- Test the release build on a real device, on the oldest and newest OS version you support. Debug-only testing is not enough. (2.1)
- Remove placeholder text and art, debug menus, test buttons and test currency from the release build. (2.1)
- Every link and button works, including the support URL and privacy policy URL. (2.1)
- The backend is live and stays live during review. (2.1)
- Only public APIs are used. (2.5.1)
- No unnecessary battery drain, heat or background work. Each background mode matches a real feature. (2.4.2, 2.5.4)
- No hidden, dormant or remotely enabled features that the reviewer cannot see. (2.5.19)
- Widgets, extensions and notifications relate to the app's own content. (2.5.16)

## 2. Notes for the reviewer

- Write specific review notes for each new or non-obvious feature, and say how to reach it. Generic notes get rejected. (2.1, 2.3.1)
- If the app has a login, give a working demo account. If it uses a demo mode instead, get Apple's approval first. (2.1)
- Make every in-app purchase reachable and working for the reviewer, or explain in the notes why it is not. (2.1)
- Explain features a reviewer might miss: widgets, Live Activities, Siri or Shortcuts, rewards.
- Keep the developer contact details current. (1.5)

## 3. Store listing

- The name, subtitle, description and screenshots match what the app really does. No false or inflated claims. (2.3; Play: Metadata)
- Screenshots show the app in use, not only a splash, title or login screen. (2.3.3)
- If featured items need extra purchases, the listing says so. (2.3.2)
- No prices in the metadata. No other mobile platforms or app stores in the app or its metadata. (2.3.7, 2.3.10)
- Name length: Apple name 2 to 30 characters, Apple subtitle up to 30, Play title up to 30. (2.3.7; App Store Connect app information; Play Metadata)
- Play title, icon and developer name: no ranking or performance words ("#1", "Popular"), no prices or promotions, no Play program names, no emoji, and no ALL CAPS unless it is the brand. (Play: Metadata)
- Icons and screenshots are suitable for all ages. (2.3.8)
- The words "For Kids" or "For Children" appear only for apps in Apple's Kids category. (2.3.8)

## 4. Original work

- The app is your own idea, with no look-alike name, icon or UI of another app or developer. (4.1)
- One bundle ID per app. No near-identical variants of an app you already have. (4.3)
- Rights are cleared for third-party fonts, music, sounds, art and trademarks.

## 5. Privacy and data

- Apple App Privacy labels and the Play Data safety form match what the app **and every SDK** collect. Typical SDK data: device or advertising ID, coarse location, diagnostics, usage. (App Privacy details; Play: Data safety)
- Play: the Data safety form is filled in even if the app collects nothing. It states whether users can ask for data deletion. (Play: Data safety)
- A privacy policy is linked in the console and inside the app. It covers what is collected, why, who gets it, how long it is kept, and how to delete it. (5.1.1(i); Play: User Data)
- iOS privacy manifest: the app has `PrivacyInfo.xcprivacy`, declares an allowed reason for each required-reason API it uses, and its SDKs ship their own manifests. Check the current list of required-reason APIs on Apple's privacy manifest documentation; do not rely on memory.
- Ask consent before collecting data. Collect only what the feature needs. The app still works when the user says no. (5.1.1(ii)-(iv))
- Paid features never depend on granting data access. (5.1.1(ii))
- Tracking needs App Tracking Transparency permission first. Push, location or tracking permission is never required to use the app or to get a reward. (5.1.2(i))
- Sharing personal data with a third-party AI service needs the user's explicit permission. (5.1.2(i))
- In the EU and UK, a consent prompt for personalised ads appears before those ads load, and users can change their choice later. Check the requirements of your ads SDK and current local law.

## 6. Accounts and sign-in

Mark NOT APPLICABLE if the app has no accounts.

- Users can start account deletion inside the app, including guest accounts. Deactivation is not deletion. (5.1.1(v); Apple account deletion page)
- Play: deletion is also possible from a web page, and that URL is entered in Play Console. (Play: User Data)
- Deletion removes the account and its personal data. Data kept for legal reasons is disclosed. (Apple account deletion; Play: User Data)
- Deletion does not force the user to phone, email or chat with support (Apple, non-regulated apps).
- Sign in with Apple accounts: the app revokes the token through Apple's REST API on deletion.
- Subscribers are told that billing continues through the store until they cancel.
- If a third-party or social login sets up the main account, an equivalent option is also offered that limits data to name and email, lets the user hide their email, and does not collect activity for ads without consent. (4.8)

## 7. Purchases

- Digital goods, features, currency, remove-ads and subscriptions use Apple in-app purchase and Google Play Billing. No links or buttons that send users to another payment method, unless a regional program allows it and you are enrolled. (3.1.1; Play: Payments)
- Restorable purchases (non-consumables, subscriptions) have a working Restore Purchases control. (3.1.1)
- Prices come from StoreKit or Play Billing at runtime and match the purchase sheet. No hard-coded prices. (Play: Payments)
- Consumables are granted exactly once, also after a crash or interrupted purchase. Finish or acknowledge each transaction only after the item is granted.
- Purchased credits do not expire. (3.1.1)
- Random paid items (loot boxes) show their odds before purchase. (3.1.1; Play: Payments)
- In-app currency is never used for real-money gaming. (5.3.3)
- Subscriptions last at least 7 days, work on all of the user's devices, and say clearly what the price includes. (3.1.2)
- App Store Connect: the first in-app purchase of each type is submitted together with a new app version. (App Store Connect Help: submit an in-app purchase)
- A "remove ads" purchase really removes the ads in the review build.

## 8. Ads

Mark NOT APPLICABLE if the app has no ads.

- Apple: ads only in the main app, not in widgets, extensions, notifications or App Clips. (2.5.18)
- Ads suit the app's age rating. No targeted ads based on sensitive data such as health or children's data. (2.5.18)
- Interstitials are clearly ads, have a visible close control and are not deceptive. Users can report an inappropriate ad. (2.5.18)
- No fake clicks or inflated impressions. (3.2.2)
- Play: no full-screen ad before the splash screen, or unexpectedly at the start of a level or task. A full-screen ad can be closed within 15 seconds, unless the user chose to watch it (rewarded) or it does not interrupt (for example, after a score screen). (Play: Ads)
- Play: no ad triggered by the home or back button, no fake close buttons, no ads that mimic system UI. (Play: Ads)
- Rewarded ads say what the reward is before the ad, and give it after.

## 9. Age rating and kids

- The age rating questionnaire is answered honestly. Apple's current ratings are 4+, 9+, 13+, 16+ and 18+ (on OS 26 and later), and the questionnaire asks about in-app controls and social features. (2.3.6; App Store Connect age ratings)
- Apple Kids category: no links out of the app, no purchases and no other distractions unless behind a parental gate. No third-party ads or analytics, apart from Apple's narrow exceptions. No personal data sent to third parties. (1.3, 5.1.4)
- Play apps aimed at children: the target audience and content are declared in Play Console, and only SDKs approved for child-directed use are included. Read the current Play Families policy before you submit.

## 10. Permissions and notifications

- Each permission purpose string names the real feature that needs it. (5.1.1(ii))
- Permissions are asked at the moment the feature needs them, not all at launch.
- Push notifications are not required for core features. Promotional pushes need opt-in. (4.5.4)
- Live Activities and other system features are not used for spam or ads. (4.5.3)

## 11. Store account and release setup

- Apple: the developer account is active. The Paid Apps agreement, banking and tax are complete if the app sells anything.
- Apple: EU Digital Services Act trader status is declared in App Store Connect. This is required even if you do not distribute in the EU. Traders must provide contact and payment details. (App Store Connect Help: DSA trader requirements)
- Play: the account's developer verification and payments profile are complete. Check Play Console for any trader-status prompt.
- Play: new personal developer accounts (created after 2023-11-13) must run a closed test with at least 12 testers opted in for 14 days in a row before applying for production. (Play Console Help answer/14151465)
- Play: the app meets the current target API level requirement. Check the requirement page in Play Console Help for this year's level.
- The app is not offered in countries where it must not be, and region-specific rules (for example, gambling licences) are met. (5.3.4)

## Report

1. A table with the columns: area, item, result, evidence or fix.
2. The FAIL items in the order to fix them, most likely rejection first.
3. The NOT CHECKED items, with what the user must check by hand.
4. The items you re-checked against the official page, with the page and date.

If the project has a plan or release notes file, offer to add the result to it with today's date.
