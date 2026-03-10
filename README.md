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
