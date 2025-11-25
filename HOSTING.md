# Hosting your Privacy Policy (GitHub Pages)

This document explains quick, reliable ways to host the privacy policy files in this repository so you can paste a public URL into the Google Play Console.

Recommended: GitHub Pages (serve the `docs/` folder)

1) Verify files are in `docs/`
- `docs/privacy_policy.md` (English)
- `docs/ar/privacy_policy.md` (Arabic)

2) Commit and push the files to `main`

```bash
git add docs/privacy_policy.md docs/ar/privacy_policy.md
git commit -m "Add privacy policy (EN + AR)"
git push origin main
```

3) Enable GitHub Pages for the repository
- Go to your repository on GitHub -> `Settings` -> `Pages` (or `Code and automation` -> `Pages`).
- Under `Build and deployment` select `Deploy from a branch`.
- Choose `Branch: main` and `Folder: /docs` then click `Save`.
- Wait a few minutes; the site URL will appear at the top of the Pages settings, usually:

```
https://<github-username>.github.io/<repo-name>/
```

4) How your policy pages will be reachable
- GitHub Pages will convert Markdown files in `docs/` to HTML. The English policy will be reachable at:

```
https://<github-username>.github.io/<repo-name>/privacy_policy.html
```

- The Arabic file will be reachable at:

```
https://<github-username>.github.io/<repo-name>/ar/privacy_policy.html
```

Tip: If you want a single URL that offers a language chooser, add a small `docs/index.html` that links to the two language pages. Example minimal `index.html` snippet:

```html
<!doctype html>
<html lang="en">
  <head><meta charset="utf-8"><title>Privacy Policy</title></head>
  <body>
    <h1>Privacy Policy / سياسة الخصوصية</h1>
    <ul>
      <li><a href="/privacy_policy.html">English</a></li>
      <li><a href="/ar/privacy_policy.html">العربية</a></li>
    </ul>
  </body>
</html>
```

5) Verify the public URL
- Open the Pages URL provided by GitHub and navigate to the `privacy_policy.html` page. Ensure content loads and links work.

6) Add the URL to Google Play Console
- Sign in to Google Play Console and open your app.
- Go to `Store presence` -> `Main store listing` (or `Policy` / `App content`, depending on Console UI) and find the **Privacy Policy** field.
- Paste the public HTTPS URL (for example, `https://<github-username>.github.io/<repo-name>/privacy_policy.html`) and save.

7) Update Data Safety and other Play requirements
- In Play Console, complete the **App content** / **Data safety** questionnaire accurately describing what data you collect and how you use it.

8) In-app link (recommended)
- Add a Settings or About screen item that opens the privacy policy URL using `url_launcher`:

Dart example:
```dart
import 'package:url_launcher/url_launcher.dart';

final Uri _policy = Uri.parse('https://<github-username>.github.io/<repo-name>/privacy_policy.html');

Future<void> openPrivacyPolicy() async {
  if (!await launchUrl(_policy)) throw 'Could not launch $_policy';
}
```

9) Optional: Use a custom domain
- If you have a website, host the policy at `https://yourdomain.com/privacy` and use that URL in the Play Console.

Troubleshooting
- If the Pages site shows a 404, confirm the `Branch`/`Folder` selection and that files are pushed to the chosen branch.
- If the markdown does not render as expected, consider adding a simple `index.html` or converting the Markdown to HTML locally and committing the `.html` files inside `docs/`.

If you want, I can add the `docs/index.html` chooser and commit it for you, and then provide the exact URL you'll paste into Play Console once you tell me your GitHub username and repo name (or I can infer the repo name: `moalimee_app`).
