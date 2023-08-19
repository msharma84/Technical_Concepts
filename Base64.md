# BASE64

Base64 is a binary-to-text encoding scheme. It's represented as printable ASCII characters where each Base64 character contains 6 bits of binary information.

## How Does Base64 Work?
In Base64, as the name suggests, there are 64 characters used to encode binary data. These characters are:
* 26 Capital letters [A-Z]
* 26 lower letters [a-z]
* 10 digits [0-9]
* 2 special characters [+ , /]

Note: There is also a 65th character (=) , which serves a special meaning and it's called a padding character.

## Why use Base64 Encoding?

### Computers work with 0s and 1s, so why bother converting this into another format?

Yes, true. Binary is the language of computers. That's exactly why we're converting it. A sequence such as 0010110 can mean many things. It can be part of an image, it can be a part of an audio file or it can be a command that deletes half of your hard drive.

This data must be processed differently, depending on what it's supposed to represent. Also, many servers don't expect raw binary data. Email servers, for example, expect textual data. All emails are encoded before the applications send them.


