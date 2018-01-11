### [.encodings](encodings.md)[__String Encoding__]

---
#### *<p align='center'> ASCII </p>*
---
* String encoding that maps a byte to an English character, a special character, or a number
  * [ASCII Table](http://www.asciitable.com/)
  * Out of the 128 characters defined in ASCII, only 95 of them are human-readable
  * ASCII used 7 bits only, but the extra bit is still not enough to encode all the other languages

---
#### *<p align='center'> Unicode </p>*
---
* Various encoding schemes were invented but none covered every languages until Unicode came along
  * [Unicode Character Table](https://unicode-table.com/en/#control-character)
  * Unicode is a large table mapping every character to a unique numbers (code point) 
  * First 256 code points maps 1:1 to ASCII  
  * Different UTF encodings (e.g. UTF-8, UTF-16) use different amount of bytes to encode those code points

---
#### *<p align='center'> Cause Of Garbled Text </p>*
---
* Reading a byte sequence using the wrong encoding scheme
