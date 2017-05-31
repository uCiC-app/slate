# Thumbor 

## Overview

uCiC has a set of image processing servers available to serve modified versions of images to clients based on their specific needs using the [Thumbor](https://thumbor.readthedocs.io/en/latest/index.html) library . The most practical usage of this allows clients to request a pixel-specific sizing of an image which the server will resize and/or crop on the fly for the client. This reduces the bandwidth the client consumes to load the image, which in turn improves performance.

## Usage

The thumbor server is used by generating a new URL to request the image from based on the original image URL, the client's desired image specifications and the URL of the thumbor server.

For example, given the original image URL
`https://media.ucic.vc/media/23585E7D-D7DB-45A6-8877-889668CA1762/display.jpg`

Say the client only has 150x200 pixels to display the image in. We create a new URL to request it as

`https://thumbor.ucic.vc/{Security_Hash}/150x200/https://media.ucic.vc/media/23585E7D-D7DB-45A6-8877-889668CA1762/display.jpg`

where `https://thumbor.ucic.vc` is the uCiC Thumbor server address.

The Security_Hash is generated as follows:
Take the entire trailing end of the url (including requesting parameters and the original URL) and create a HMAC-SHA-1 hash using the private security key and encode the output to URL-safe Base64 (Standard Base64 encoding, but replace any `/` with `_` and any `+` with `-`).

`150x200/https://media.ucic.vc/media/23585E7D-D7DB-45A6-8877-889668CA1762/display.jpg`

Hashes to `0541B60037A4FE5A464468FC44E3F0F710C8933F`.  
Which then encodes to `BUG2ADek/lpGRGj8ROPw9xDIkz8=` in standard Base 64.  
Which then converts to `BUG2ADek_lpGRGj8ROPw9xDIkz8=` in URL-safe Base 64.  

Thus, the final url to request the image from becomes

`https://thumbor.ucic.vc/BUG2ADek_lpGRGj8ROPw9xDIkz8=/150x200/https://media.ucic.vc/media/23585E7D-D7DB-45A6-8877-889668CA1762/display.jpg`



##Smart Cropping

Thumbor supports a specialized kind of image cropping where it employs feature detection to identify the "most interesting" part of an image and crop towards that, rather than the default centre. To use this, simply include the `/smart` url component following the desired resolution. **Make sure that this is included before creating the security hash** for the request.

Original Image `https://i.imgur.com/eVdqKNZ.jpg`

Desired spec URL `/150x150/smart/https://i.imgur.com/eVdqKNZ.jpg`

URL-Safe Base64 Encode of SHA-1 Hash `en5sXMhgAzBCPRRdJt2uXKFWZF0=`

Final URL `https://thumbor.ucic.vc/en5sXMhgAzBCPRRdJt2uXKFWZF0=/150x150/smart/https://i.imgur.com/eVdqKNZ.jpg`