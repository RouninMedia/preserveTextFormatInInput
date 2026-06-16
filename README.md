# preserveTextFormatInInput
preserveTextFormatInInput() is a short JavaScript function which maintains an obligatory prefix or suffix when the user is interacting with an &lt;input type="text"> HTML form element. 

```js

// FORMAT SOCIAL MEDIA ENTRIES ON INPUT
const preserveSocialMediaFormatInInput = (socialMediaInput, adfix, adfixType = 'prefix') => {

  socialMediaInput.addEventListener('selectionchange', (e) => {
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

  socialMediaInput.addEventListener('focus', (e) => {if (e.target.value === '') {e.target.value = adfix;}});
  socialMediaInput.addEventListener('blur', (e) => {if (e.target.value === adfix) {e.target.value = '';}});
}

preserveSocialMediaFormatInInput(appElements.artistProfileWebsiteInput, 'https://');
preserveSocialMediaFormatInInput(appElements.artistProfileFacebookInput, 'https://www.facebook.com/');
// preserveSocialMediaFormatInInput(appElements.artistProfileTumblrInput, '.tumblr.com', 'suffix');
appElements.socialMediaInputsUsingAt.forEach((socialMediaInput) => preserveSocialMediaFormatInInput(socialMediaInput, '@'));

```



'''''''''''''''
