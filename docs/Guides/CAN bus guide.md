In CAN (Controller Area Network) communication, each byte of data within a CAN frame is transmitted as a sequence of bits. Each bit is transmitted serially, starting with the least significant bit (LSB) and ending with the most significant bit (MSB).<br />

So, if you send a byte with the value 0b10110000, it will be transmitted over the CAN bus as follows:<br />

* Start Bit: The start bit is transmitted first (LSB).<br />
* Data Bits: The data bits are transmitted serially, starting with the LSB (bit[0] = 0) and ending with the MSB (bit[7] = 1).<br />

Therefore, in the case of your byte 0b10110000, it will be transmitted as follows:<br />

Start Bit | Data Bits (LSB first) <br />

   0       |     0  0  0  0  1  1  0  1 <br />


transmition of bytes is LSB byte first. So if we have data packet of 4 bytes; byte 3,2,1,0; byte 3 will be sent first and byte 0 last.<br />

Data is packed in arrays so that for 16 bit number, 8 MSB bits go to array index 0 and 8 LSB bits go to array index 1.<br />
When transmitting that data If you look here: https://en.wikipedia.org/wiki/CAN_bus LSB are sent first so array element with index 1 is transmitted first.<br />
So if we have number that is 32814 decimal: MSB byte[0] = 1000 0000 , LSB byte[1] = 0101 1010 <br />
It will be sent like this 0101 1010 0000 0001 <br />

Transmitting floats is following the IEEE 754 floating-point format.<br />

In IEEE 754 format, a single-precision floating-point number (float) is represented using 32 bits, with the following components:<br />

Sign bit: 1 bit, representing the sign of the number.<br />
Exponent bits: 8 bits, representing the exponent of the number.<br />
Fraction bits: 23 bits, representing the fractional part of the number.<br />
The function you provided interprets the input array of 4 bytes as a 32-bit integer and then uses a union to reinterpret those bits as a float. The bit manipulation <br />performed by shifting the bytes and combining them respects the layout of IEEE 754 floating-point numbers, assuming that the byte order of the system is big-endian.<br />

Therefore, this function can be used to convert an array of 4 bytes representing a IEEE 754 float to its equivalent floating-point value.<br />