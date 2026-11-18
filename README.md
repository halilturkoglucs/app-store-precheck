# App Store & Google Play Precheck

A Claude Code skill that checks an iOS or Android app or game against Apple's App Review Guidelines and Google Play policy before you submit it.

Ask Claude something like "check my app before I submit it" or "will this pass App Review". It goes through your code, build settings and store listing and reports each item as PASS (with evidence), FAIL (with the fix), NOT CHECKED or NOT APPLICABLE. Then it lists the failures in the order to fix them.

## What it checks

1. The build works and is complete: release build, placeholders, live backend, public APIs, background modes
2. Notes for the reviewer: demo account, how to reach each feature and purchase
3. Store listing: accurate claims, real screenshots, name limits, banned words
4. Original work and content rights
5. Privacy: App Privacy labels, Play Data safety, privacy manifest, privacy policy, tracking consent
6. Accounts: in-app deletion, Play web deletion URL, login options
7. Purchases: in-app purchase and Play Billing, Restore Purchases, consumables, loot box odds, subscriptions
8. Ads: placement, close controls, Play full-screen ad rules
9. Age rating and kids rules
10. Permissions and notifications
11. Store account setup: agreements, EU trader status, Play closed testing, target API level

Every item names the Apple guideline or Play policy page it comes from. Store rules change often, so the skill tells Claude to re-check a rule on the official page before you rely on it.

## Install

```
/plugin marketplace add halilturkoglucs/app-store-precheck
/plugin install app-store-precheck@app-store-precheck
```

## Sources

Written in our own words on 2026-11-18 from Apple's App Review Guidelines (updated 2026-10-16), Apple developer and App Store Connect help pages, the Google Play Developer Program Policy and Play Console Help. The full list is in the skill.

## Limits

- It is a checklist, not a guarantee. Reviewers can still reject an app for reasons not listed here.
- Claude cannot see App Store Connect or Play Console unless you share screenshots or text, so console items are often NOT CHECKED.
- It does not cover macOS, tvOS, visionOS or watchOS rules beyond what they share with iOS.

Not affiliated with or endorsed by Apple Inc. or Google LLC. App Store is a trademark of Apple Inc. Google Play is a trademark of Google LLC.

## License

MIT
