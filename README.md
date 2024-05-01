# Overview
In image steganography, a message is embedded into an image by altering the values of some pixels, which are chosen by an encryption algorithm. The recipient of the image must be aware of the same algorithm in order to known which pixels he or she must select to extract the message. The image selected for this purpose is called the cover-image and the image obtained after steganography is called the stego-image.

The idea behind image-based Steganography is very simple. Images are composed of digital data (pixels), which describes what’s inside the picture, usually the colors of all the pixels. Since we know every image is made up of pixels and every pixel contains 3-values (red, green, blue), steganography works by changing bits of useless data in regular computer files (such as graphics, sound, text, HTML) with bits of different, invisible information. This hidden information can be plain text, cipher text, or even images.

## Working
- Pixels are the building blocks of an image.
- Every pixel contains three values: (red, green, blue) also known as RGB values.
- Every RGB value ranges from 0 to 255 for 8-bit image.

### Encoding
1. Every byte of data is converted to its 8-bit binary code using ASCII values.
2. Now pixels are read from left to right in a group of 3 containing a total of 9 values (i.e. 3*3=9 RGB values). The first 8-values are used to store one character which was converted into an 8-bit binary in step 1.
3. Then the corresponding RGB value and binary data are compared, if the binary digit is 1 then the RGB value will be converted into odd else even.
4. The 9th value determines if more pixels should be read or not. If there is more data to be read, i.e. encoded or decoded, then the ninth pixel changes to even. Otherwise, if we want to stop reading pixels further, then make it odd.

Example: Suppose the message to be hidden is ‘cat‘. Since the message is of 3-bytes, therefore, pixels required to encode the data is 3 x 3 = 9. Consider a 4 x 3  image with a total 12-pixels, which are sufficient to encode the given data.
1. ASCII value of ‘C‘ is 67 whose binary equivalent is 01000011.
2. Take first 3-pixels [ (27, 64, 164), (248, 244, 194), (174, 246, 250) ] of the image to encode.
3. Now change the pixel to odd for 1 and even for 0.
4. So, the modifies pixels are [ (26, 63, 164), (248, 244, 194), (173, 245, 250) ].
5. Now repeat the same for remaining characters.

### Decoding
Decoding is getting secret information from image file. This process is called as Steganolysis.
1. To decode, three pixels are read at a time, till the last value is odd, which means the message is over. The first 8 values of RGB give the secret data while the 9th value determines whether we need to move forward or not.
2. Every 3-pixels contain a binary data. The first 8 values can be extracted by the same encoding logic. If the value is odd the binary bit is 1 else 0.
3. By concatenating these bits to a string with every three pixels we will get a byte of secret data i.e. one character.

Example:
1. First read the three pixels of the corrupted image – [ (26, 63, 164), (248, 244, 194), (173, 245, 250) ] .
2. The first value: 26, which is even, therefore the binary bit is 0. Similarly, for 63, the binary bit is 1 and for 164 it is 0.
3. This process continues until the 8th RGB value.
4. We finally get the binary value: 01000011 after concatenating all individual binary values.
5. The final binary data corresponds to decimal value 72, and in ASCII, it Prepresents the character H.