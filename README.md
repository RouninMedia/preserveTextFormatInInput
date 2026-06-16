# preserveTextFormatInInput
`preserveTextFormatInInput()` is a short JavaScript function which maintains an obligatory prefix or suffix when the user is interacting with an `&lt;input type="text">` HTML form element.


This guarantees that the user will always submit:

 - a *URL* prefixed with `https://`; or
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



'''''''''''''''
