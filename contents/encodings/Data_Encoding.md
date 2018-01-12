### [.encodings](encodings.md)[__Data Encoding__]

---
#### *<p align='center'> Definition </p>*
---
* All forms of content modification for the purpose of hiding intent

---
#### *<p align='center'> Caesar Cipher </p>*
---
* Formed by shifting the letters of alphabet #’s characters to the left or right

---
#### *<p align='center'> Single-Byte XOR Encoding </p>*
---
* Modifies each byte of plaintext by performing a logical XOR operation with a static byte value
* __Identifying XOR Loop__: looks for a small loop that contains the XOR function (where it is xor-ing a register and a constant or a register with another register)
* __Single-byte XOR's Weakness__: if there are many null bytes then key will be easy to figure out since XOR-ing nulls with the key reveals the key. 
* __Solutions To Single-Byte XOR Encoding's Weakness__: 
  * Null-preserving single-byte XOR encoding: if plaintext is NULL or key itself, then it will not be encoded via XOR
  * Generates the keystream used to XOR the data using a pseudorandom number generator 
    * __Blum Blum Shub PRNG__: generic form: Value<sup>i+1</sup> = (Value<sup>i</sup> * Value<sup>i</sup>) % M. M is a constant  that is the product of 2 large primes and an initial V needs to be given. Actual key being xor-ed with the data is the lowest byte of current PRNG value

---
#### *<p align='center'> Other Simple Encoding Scheme </p>*
---
* __ADD, SUB__
* __ROL, ROR__: Instructions rotate the bits within a byte right or left
* __Multibyte__: XOR key is multibyte
* __Chained or Loopback__: Use content itself as part of the key
  * the original key is applied at one side of the plaintext and the encoded output character is used as the key for the next character

---
#### *<p align='center'> Base64 </p>*
---
* Encodes binary data into character set of 64 ASCII characters
* Most common character set is MIME’s Base64, whose table consists of A-Z, a-z, and 0-9 for the first 62 values and + / for the last 2 values
* Base64 operates every 3 bytes (24 bits). For every 6 bits, it indexes the table with 64 characters. The encoded value is the character that is indexed with the 6 bits 
* One padding character may be presented at the end of the encoded string (typically =) since Base64 operates every 3 bytes
* Easy to develop a custom substitution cipher using Base64 since the only item that needs to be changed is the indexing string table of 64 characters
<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/encodings/Data_Encoding/base64_conversion.png"> 
<p align='center'><sub><strong>base64 conversion</strong></sub></p>
</div>
