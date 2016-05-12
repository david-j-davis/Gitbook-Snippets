#SVG
---

####Data URI (base64) images
- For sag cross browser, don’t simply pop in the <svg> after the data: - this works on all major browsers except Firefox.
- ex. background: url('data:image/svg+xml;utf8,...
- Here’s a base64 [encoder:](http://www.mobilefish.com/services/base64/base64.php)
- Here’s a url [encoder/decoder:](http://meyerweb.com/eric/tools/dencoder/) to create a url escaped string from the <svg>

- Step: create svg
- Step: run terminal svgo
- If using background image sag as data uri, run it through the above encoder
- Place in the code as ex. background: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http...

References:

- [https://css-tricks.com/probably-dont-base64-svg/](https://css-tricks.com/probably-dont-base64-svg/)
- [https://css-tricks.com/data-uris/](https://css-tricks.com/data-uris/)
