# preserveTextFormatInInput
`preserveTextFormatInInput()` is a short JavaScript function which persists a required prefix or suffix when the user is adding text to certain HTML form elements including `<input type="text">` and `<input type="url">`.


This guarantees that the user will always submit:

 - a *URL* prefixed with `https://`
 - a *tumblr* handle prefixed with `@`

 etc.

 ________

```js

// FORMAT SOCIAL MEDIA ENTRIES ON INPUT
const preserveTextFormatInInput = (socialMediaInput, adfix, adfixType = 'prefix') => {

  textInput.addEventListener('selectionchange', (e) => {
    if (e.target.value.length <= adfix.length) {e.target.value = adfix;}

    const currentCaretPosition = socialMediaInput.selectionStart;

    switch (adfixType) {
      case ('prefix'):
        const lowestCaretPosition = (adfix.length);
        if (currentCaretPosition < lowestCaretPosition) {
          e.target.setSelectionRange(lowestCaretPosition, lowestCaretPosition);
        }
      break;
      
      case ('suffix'):
      const highestCaretPosition = (e.target.value.length - adfix.length);
      if (currentCaretPosition > highestCaretPosition) {
        e.target.setSelectionRange(highestCaretPosition, highestCaretPosition);
      }
      break;
    }
  });

  textInput.addEventListener('focus', (e) => {if (e.target.value === '') {e.target.value = adfix;}});
  textInput.addEventListener('blur', (e) => {if (e.target.value === adfix) {e.target.value = '';}});
}

preserveTextFormatInInput(appElements.artistProfileWebsiteInput, 'https://');
preserveTextFormatInInput(appElements.artistProfileFacebookInput, 'https://www.facebook.com/');
preserveTextFormatInInput(appElements.artistProfileTumblrInput, '.tumblr.com', 'suffix');
appElements.socialMediaInputsUsingAt.forEach((socialMediaInput) => preserveTextFormatInInput(socialMediaInput, '@'));

```

## Quick Explanation

This line:

```if (e.target.value.length <= adfix.length) {e.target.value = adfix;}```

ensures that any attempt to remove the adfix from the `<input>` will persist the adfix in the `<input>`.


These lines:

```
textInput.addEventListener('focus', (e) => {if (e.target.value === '') {e.target.value = adfix;}});
textInput.addEventListener('blur', (e) => {if (e.target.value === adfix) {e.target.value = '';}});
```

ensures both that

1. if the user focuses on an empty form element then the `<input>` will immediately be populated with the adfix
2. if the user abandons a form element containing only the adfix, then the adfix will be removed, leaving an empty `<input>`


'''''''''''''''
