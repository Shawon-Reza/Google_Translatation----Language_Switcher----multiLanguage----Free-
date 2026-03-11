# Google_Translatation----Language_Switcher----multiLanguage----Free-

# Google Translate Website Integration (Free + Custom Language Switcher)

A lightweight, free way to add **Google Website Translator** to a React/Vite/HTML project with:

- A clean custom dropdown language switcher (usually placed in Navbar)
- No visible Google branding/banner/watermark
- Cookie-based language persistence
- Support for 13 popular languages

> **Important Notice (2025–2026)**  
> Google officially restricts the free Website Translator widget mostly to **non-commercial / government / non-profit** use (especially COVID/academic related projects).  
> For commercial websites it is recommended to use **Google Cloud Translation API** instead.  
> Hiding the Google bar/branding via CSS may technically violate the terms of service — use at your own risk.

## Features

- Simple dropdown language selector
- Remembers user's language choice via cookie (`googtrans`)
- Hides Google Translate top banner & "Powered by Google" links
- Works with modern React / Vite / plain HTML projects
- No external npm packages required

## Supported Languages

| Code     | Language                  |
|----------|---------------------------|
| en       | English                   |
| fr       | French                    |
| es       | Spanish                   |
| pt       | Portuguese                |
| de       | German                    |
| bn       | Bengali                   |
| zh-CN    | Chinese (Simplified)      |
| zh-TW    | Chinese (Traditional)     |
| ja       | Japanese                  |
| ko       | Korean                    |
| ru       | Russian                   |
| it       | Italian                   |
| ar       | Arabic                    |

## Installation

### 1. Add Google Translate script to `index.html`

Place this code **inside `<body>`**, preferably right after your main React script:

```html
<!-- Google Translate Widget -->
<script type="text/javascript">
  function googleTranslateElementInit() {
    const mountNode = document.getElementById("google_translate_element");
    if (!mountNode || !window.google?.translate?.TranslateElement) {
      return;
    }
    new google.translate.TranslateElement(
      {
        pageLanguage: "en",                           // ← change if your default is different
        includedLanguages: "en,fr,es,pt,de,bn,zh-CN,zh-TW,ja,ko,ru,it,ar",
        layout: google.translate.TranslateElement.InlineLayout.SIMPLE
      },
      "google_translate_element"
    );
  }
</script>

<script src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>





















# Index.html
```jsx
 <!------------------------------- Google Translate --------------------------------->
  <!-------------------- Add this Codes within the body in index.html after this line: -<script type="module" src="/src/main.jsx"></script> ------------->
  <script type="text/javascript">
    function googleTranslateElementInit() {
      const mountNode = document.getElementById("google_translate_element");
      if (!mountNode || !window.google?.translate?.TranslateElement) {
        return;
      }

      new google.translate.TranslateElement(
        {
          pageLanguage: "en",
          includedLanguages: "en,fr,es,pt,de,bn,zh-CN,zh-TW,ja,ko,ru,it,ar",
          layout: google.translate.TranslateElement.InlineLayout.SIMPLE
        }, "google_translate_element"
      );
    }
  </script>
  <script src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
  ```
# LanguageSwitcher.jsx
```jsx
//======================= Place this componenet ant any plase for language change (Ususally on Navbar) ============================= 


import { useEffect, useState } from "react";

const LANGUAGES = [
  { value: "en", label: "English" },
  { value: "fr", label: "French" },
  { value: "es", label: "Spanish" },
  { value: "pt", label: "Portuguese" },
  { value: "de", label: "German" },
  { value: "bn", label: "Bengali" },
  { value: "zh-CN", label: "Chinese (Simplified)" },
  { value: "zh-TW", label: "Chinese (Traditional)" },
  { value: "ja", label: "Japanese" },
  { value: "ko", label: "Korean" },
  { value: "ru", label: "Russian" },
  { value: "it", label: "Italian" },
  { value: "ar", label: "Arabic" },
];

function LanguageSwitcher() {
  const [selectedLanguage, setSelectedLanguage] = useState("en");

  useEffect(() => {
    const match = document.cookie.match(/(?:^|;\s*)googtrans=\/[^/]+\/([^;]+)/);
    if (match?.[1]) {
      setSelectedLanguage(match[1]);
    }
  }, []);

  const handleLanguageChange = (event) => {
    const nextLanguage = event.target.value;
    setSelectedLanguage(nextLanguage);

    const cookieValue = `/auto/${nextLanguage}`;
    document.cookie = `googtrans=${cookieValue};path=/`;
    document.cookie = `googtrans=${cookieValue};path=/;domain=${window.location.hostname}`;

    window.location.assign(`${window.location.pathname}${window.location.search}`);
  };

  return (
    <div className="notranslate flex items-center gap-2" translate="no">
      <label
        htmlFor="language-switcher"
        className="text-sm font-medium text-gray-700 dark:text-gray-200"
      >
        Language
      </label>

      <select
        id="language-switcher"
        value={selectedLanguage}
        onChange={handleLanguageChange}
        className="rounded-md border border-gray-300 bg-white px-3 py-2 text-sm text-gray-800 outline-none transition focus:border-[#94B316] dark:border-gray-600 dark:bg-gray-800 dark:text-gray-100"
      >
        {LANGUAGES.map((language) => (
          <option key={language.value} value={language.value}>
            {language.label}
          </option>
        ))}
      </select>

      <div
        id="google_translate_element"
        className="pointer-events-none absolute -left-[9999px] top-auto h-px w-px overflow-hidden"
        aria-hidden="true"
      />
    </div>
  );
}

export default LanguageSwitcher;

```
# Index.css
```jsx

/* ------------- For Remove the watermark / google translation pop avobe the website------------------- */

body {
    top: 0px !important;
}

.skiptranslate {
    display: none;
}
/* Hide Google Translate floating shortcut/icon injected by the external script. */
.goog-te-gadget-icon,
.goog-logo-link,
.VIpgJd-ZVi9od-aZ2wEe-wOHMyf,
.VIpgJd-ZVi9od-aZ2wEe-OiiCO,
.goog-te-spinner-pos {
    display: none !important;
}

```








