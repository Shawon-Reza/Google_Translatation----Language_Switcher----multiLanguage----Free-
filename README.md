# Google_Translatation----Language_Switcher----multiLanguage----Free-

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








