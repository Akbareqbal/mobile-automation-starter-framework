[README.md](https://github.com/user-attachments/files/23752865/README.md)
# RN Mobile QA Starter (Plus)

A portfolio project mirroring **Mobile Automation Engineer** daily work:
- React Native demo app (Expo) with stable testIDs.
- **Appium + Java + TestNG + Cucumber** for Android/iOS.
- **Karate** and **RestAssured** API suites.
- **Playwright** mobile‑web smoke across Chromium/Firefox/WebKit.
- **CI/CD** with GitHub Actions; Allure + Cucumber JSON artifacts.

## Quickstart
### App (React Native)
```bash
cd app
npm install
npm run android   # or: npm run ios
```

### API Tests
Karate:
```bash
cd qa/api-karate && mvn test
```
RestAssured:
```bash
cd qa/api-restassured && mvn test
```

### Mobile UI (Appium + Cucumber)
1) Build an Android APK (or iOS .app/.ipa) from `app/` and replace `PATH_TO_APK_OR_APP` in `rn_smoke.feature`.
2) Start Appium locally: `appium`
3) Run:
```bash
cd qa/mobile-appium-java
mvn -DappiumServer=http://127.0.0.1:4723/ -DdeviceName="Android Emulator" -Dplatform=android test
```

### Playwright (Mobile‑Web)
```bash
cd qa/playwright-mobileweb
npm install
npm test
# set BASE_URL to your web target if needed
```

## CI/CD
- Add repo secrets: `BROWSERSTACK_USERNAME`, `BROWSERSTACK_ACCESS_KEY`.
- Workflows:
  - `api-tests.yml` (Karate)
  - `api-restassured.yml` (RestAssured)
  - `mobile-tests.yml` (Android via BrowserStack)
  - `mobile-tests-ios.yml` (iOS via BrowserStack)
  - `playwright.yml` (Chromium/Firefox/WebKit)

## Reporting
- Cucumber JSON at `qa/mobile-appium-java/target/cucumber-report.json`
- Allure results at `qa/mobile-appium-java/target/allure-results`
- Playwright HTML report artifact in CI

## TDD/BDD workflow
- Start with failing Cucumber/Karate scenarios, implement app/API changes, make green.
- Keep Page Objects lean. Prefer accessibilityId/testID locators.
- Expand modules to mimic micro‑frontends as needed.

## Next
- Add Allure publishing in GitHub Pages or a self‑hosted report viewer
- Add iOS‑specific page objects and steps
- Expand device matrix and add retry/flaky test triage job
