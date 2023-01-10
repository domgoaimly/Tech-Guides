The idea behind Base64 is very simple.

Consider sending a message in binary. This transmission can be considered as composed by 8 bit characters so it is base256: each byte is a symbol from 0 to 255.

The problem with this coding is that it cannot be attached to emails and similar channels as some characters have special meaning.

Therefore instead of using 8 bit digits, the Base64 code uses 6 bit words, i.e. 64 combinations, but maps these 64 digits to ASCII characters from ‘A’ (meaning 0) to ‘/’ meaning 63.

The advantage is that to use only legal ASCII characters, that are perfectly compatible with any channel, but to minimize the waste. In fact on 7 bit per byte channels, only one bit is lost, on 8 bit per byte only two bits are lost.

[Base64 - Wikipedia](https://en.wikipedia.org/wiki/Base64)

The idea of base64 encoding is to avoid binary data for protocols based on text. Outside this situation, it's I think always a bad idea.

Data Encoding
Every data Encoding and Decoding can be used duo various reasons, which came up with benefits and downsides.

like:

Error-detection encodings : which can detect errors but increase data usage.
Encryption encodings: turns data to cipher which intruder wont decipher.
There are a lot of Encoding Algorithms which Alter Data in Which has some usefullness to do that.

but with

Base64 Encoding, its encode every 6-bit data into one character (8-bit) . 3 Byte to 4 Byte but it only includes alphanumeric(62 distinc) and 2 signs.

its benefits is it Dose not have special chars and signs

Base64 Purpose
it make possible to transfer Any Data with Channels Which Prohibits us to have:

special chars like ' " / \  ...
non-printable Ascii like \0 \n \r \t \a
8-bit Ascii codes (ascii with 1 MSB )
binary files usually includes any data which if turns in ascii can be any 8-bit character.

in some protocols and application there are I/O Interfaces Which Does only accepts a handful of chars (alphanumeric with a few of signs).

duo to:

prevent to code injection (ex: SQL injection or any prgramming-language-syntax-like characters ; )

or just some character has already has a meaning in their protocol (ex: in URI QueryString character & has a meaning and cannot be in any QueryString Value)

or maybe the input is not intended to accept non-alphanumerical values. (ex: it should accept only Human Names)

The only concern is the request body size. If all your images are small, like a few M, then you should be fine.

My server is asp.net core, its maxAllowedContentLength value is 30000000, which is approximately 28.6MB. When the image size is over this, the request failed with error "request body too large".

I think node.js should have similar setting, make sure to adjust it to meet your need.

Please note that when the request size is too big, the possibility of request timeout increases accordingly due to the network traffic. This will be an issue especially for the requests from phones.

Base64 increases the size of the data transferred by 33%.

8


'Why not just use binary upload with multipart headers on the http request?' indeed why not ;)

Base64 image representation can be directly placed within html to render an image.

Binary takes up less space. And benefits from greater network effects and standardization. E.g. if you want to use amazon simple secure storage S3 you have to store a binary file. You can't store a string you would need a key/value store e.g. redis.

Pros

Avoidance of binary data for protocols based on text, and independance from external files.
Avoidance of delimiter collision.
Cons

Time and space increased complexity; for space it's 33–36% (33% by the encoding itself, up to 3% more by the inserted line breaks).
API response payloads are larger/too large.
User Experience is negatively impacted, unless one invoke some lazy loading.
By including all image data together in one API response, the app must receive all data before drawing anything on screen. This means users will see on-screen loading states for longer and the app will appear sluggish as users wait.

This is however mitigated with Axios and some lazy loader such as react-lazyload or lazyload or so.

CDN caching is harder. Contrary to image files, the Base64 strings inside an API response cannot be delivered via a CDN cache. The whole API response must be delivered by CDN. (cf., Don’t use Base64 encoded images on mobile and Why "optimizing" your images with Base64 is almost always a bad idea)
Image caching on the device is no longer possible.
Content management becomes harder on server side. Most content management tools handle images as binary files. But then when managing in binary, there is the time overhead of encoding/decoding.
No security gain and overhead in engineering to mitigate (Sanitizing, Input Validation, Escaping). Example of XSS attack: Preventing XSS with Base64 encoding: The False sense of web application security
The developers of that site might have opted to make the website appear more secure by having cryptic URLs and whatnot. However, that doesn't mean this is security by obscurity.

If their website is vulnerable to SQL injection and they try to hide that by encoding the URLs, then it's security by obscurity. If their website is well secured against SQL injection; XSS; CSRF; etc., and they deiced to encode the URLs like that, then it's just plain stupidity.

It does not help with text encoded images such as svg (Probably Don’t Base64 SVG)

Data URIs aren't supported on IE6 or IE7, nor on Opera before 7.2 (Which browsers support data URIs and since which version?)

References

https://en.wikipedia.org/wiki/Base64

https://en.wikipedia.org/wiki/Delimiter#Delimiter_collision

SO: What is base 64 encoding used for?

https://medium.com/snapp-mobile/dont-use-base64-encoded-images-on-mobile-13ddeac89d7c

https://css-tricks.com/probably-dont-base64-svg/

https://security.stackexchange.com/questions/46362/purpose-of-using-base64-encoded-urls

https://bunnycdn.com/blog/why-optimizing-your-images-with-base64-is-almost-always-a-bad-idea/

https://www.davidbcalhoun.com/2011/when-to-base64-encode-images-and-when-not-to/

