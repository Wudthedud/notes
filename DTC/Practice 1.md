### 1. Parity and Error Detection:

(a) Define even and odd parity in the context of error detection. (b) Explain how parity can detect errors with the following example:

- Binary message: 1101011 using even parity.
- What parity bit would be added? (c) Discuss a scenario where parity fails to detect errors and how this limitation can be mitigated.

Parity is the most simple type of checksum when one extra digit is added to the end of a byte to ensure data correctness. This can be done through even or odd parity. If even parity is used, the extra digit will lead the total number of 1's in the byte to result in an even number, while if odd parity is used, the total number of 1's will be an odd number. This means that if a bit is changed or flipped, the parity wouldn't match and an error can be detected. An example of this is in the binary message 1101011 which has 5 1's. To encode this with even parity, another 1 would be added to make it 6, making it even, which will result in the byte 11010111. 
A limitation of parity bit is the detection of more complex errors. For example, parity bits cannot detect multiple-digit errors, or transposition errors. This means that if a bit is swapped with another bit, such as 11010111 being changed into 11011011 in the example above, it wouldn't be able to detect it as the number of 1's haven't changed, just the position. If an even number of bits are changed, it also cannot be detected. For example, if the original 11010111 had 2 bits flipped, making it 11010001, this error cannot be detected. This is because the second bit flipping cancels out the first bit, making the system think that there was no error. This limitation can be mitigated by adding the position information of each digit within the encoding algorithm. An example of this could be multiplying the first digit by 1, the second digit by 2 etc, and then calculating whether the sum of all these results are even or odd, though this is not very efficient and would take a lot of computational power, as well as still being able to not detect many types of errors. The best way would be to use another type of checksum such as CRC if data integrity is crucial. 

### 2. Barcodes:

(a) What role do check digits play in error control within barcodes such as UPC and EAN? (b) Illustrate with an example how the check digit for a UPC-A barcode is calculated. (c) Assess the efficiency of barcode systems in preventing errors in automated retail environments.

A check digit is an additional digit added to the data, which is calculated from an algorithm. This can be seen in the use of barcodes, such as UPC-A. Firstly, each of the digits in the odd positions are multiplied by 3. The results of these are summed and then added to the sum of the other digits. Next a modulo-10 operation is performed on the total sum, and the difference from 10 should be the check digit. Barcodes are well designed for preventing errors in retail, as they are fast to scan, and compute, as well as widely used across retail industries, with almost all store products having one. As there is only 1 digit needed for the error detection of 12 digits, it has a high code rate of 92%. This means that more data can be stored in the same amount of space, ultimately leading to a total of 10^11 or 100 billion products. This means that they are well suited for automated retail environments. UPC-A is able to detect all single digit errors, and some multiple digit and transposition errors. This means that it's quite resilient and can withstand the day-to-day scanning of items, which are unlikely to have multiple errors spread across a barcode. 


### 3. QR Codes and Error Correction:

(a) Explain how QR codes use Reed-Solomon codes for error correction and how this ensures data reliability. (b) Provide a step-by-step process of encoding and decoding a simple QR code, emphasizing the error correction mechanism. (c) Compare the error correction capabilities of QR codes to traditional barcodes and discuss their impact on data reliability.

QR codes are encoded using Reed-Solomon encoding to allow for both error detection and correction. This is done through the generation of codewords using the interpolation of polynomials over finite Galois fields, leading to the generation of extra redundant error correction codewords. These are added onto the QR code, and can be adjusted based on the level of error correction required, as QR codes can be encoded with low (7%), medium (15%), quartile (25%) or high (30%) levels of error correction. This means that a high level QR code can have 1/3 of the code covered and still work. After the error correction capabilities run out, error detection works for roughly double the amount of error correction, so a quartile encoded QR code will detect an error at minimum when 50% of the QR code's data has changed. Generally, if more than the error detection capabilities of a QR code has been changed, the QR code will no longer scan as modules such as the alignment and version data will be changed, further removing the need for additional error detection capabilities. 
When encoding, QR codes turns the data into bits, for example ASCII characters are turned into their respective byte, and then these bits are applied onto the QR code matrix using a zig-zag pattern. QR codes can alternate whether 1's are black or white, to make it easier for decoding, therefore this version information is also added on. Next, the error correction codewords are calculated and encoded onto the QR code.
To decode a QR code when it is scanned, the camera reads the alignment information and version data, and then decodes each codeword(or set of bits). These are then changed into readable ASCII format for the user to read. 
Compared to traditional barcodes, QR codes are able to both detect errors and correct them, while barcodes can only detect errors. This means it greatly improves data reliability for critical systems. Since barcodes use check digits as error correction, if there is an error, the system can only realise that the calculated check digit does not match the last digit on the barcode, prompting the system to know that there is an error and to use ARQ for a rescan. Meanwhile, if an error is detected on the QR code, the Reed-Solomon encoding allows it to calculate the original data backwards, correcting the errors. 

### 4. Check Digits:

(a) Define check digits and their role in error control in systems such as credit cards or ISBNs. (b) Demonstrate the calculation of a check digit for an ISBN-10 number: 0-306-40615-X. (c) Evaluate the effectiveness of check digits in real-world applications like financial transactions and inventory management.

Check digits are digits appended to the end of the data for error detection. The check digit is usually calculated using a specific mathematical algorithm, depending on the standard being used. This is used in systems such as barcodes and credit cards to detect errors. For example, to find the check digit of the ISBN-10 number 0-306-40615-X, you first multiply the first digit by 1, the second digit by 2 etc, and then sum the results. This results in 145. Next modulo 11 and you get 2. Therefore, the check digit should be 2. 
Check digits are commonly employed in financial transactions and inventory management due to their effectiveness. Firstly, they have relatively low overhead, with ISBN-10 only having 1 check digit for 9 digits of data. This gives it a 90% code rate, which is better than something like a QR code or parity. They can also be calculated somewhat easily, as the algorithms generally involve simple arithmetic, meaning that it doesn't take much computational power to calculate. They are also effective at detecting single digit errors, some multiple digit errors, some transposition errors and some burst errors. 

### 5. Checksums:

(a) What is a checksum, and how does it contribute to error detection in digital data transmission? (b) Compare simple checksums with Cyclic Redundancy Checks (CRC) in terms of reliability and efficiency. (c) Provide an example where a checksum is used in file integrity verification, and discuss its advantages.



### 6. Reed-Solomon Codes:

(a) Explain the basic principles of Reed-Solomon codes and their application in error correction. (b) Illustrate how Reed-Solomon codes are implemented in CDs and DVDs for data recovery. (c) Analyse the strengths and weaknesses of using Reed-Solomon codes in terms of efficiency and error correction.

### 7. ARQ and FEC in Network Communication:

(a) Define Automatic Repeat reQuest (ARQ) and Forward Error Correction (FEC) in networking. (b) Provide an example of a protocol that uses ARQ (e.g., TCP) and another that uses FEC (e.g., satellite communication). (c) Discuss the trade-offs between ARQ and FEC, focusing on speed and reliability in high-latency environments.

The ARQ protocol is one of the main protocols used in network communication. When data is sent, it includes a checksum which is calculated by the system receiving the data using an algorithm. If the checksum doesn't match the calculated checksum, it sends back a negative acknowledgement (NACK) to the sender showing that there is an error in the data received, which results in the data being resent. If the calculated checksum does match the received one, it sends an acknowledgement, allowing the next packet to be sent. If no ACK is received at all, it will also resent the packet. For FEC, redundant data in the form of extra error correction is added to the packet, so that if there is an error in the packet, the system is able to rebuild the incorrect data using the error correction included. 
An example of ARQ is TCP (Transmission Control Protocol) which is widely used in the internet for processes such as websites, SSH and FTP. 

### 8. RAID Levels and Data Storage:

(a) Describe RAID levels (e.g., RAID 0, RAID 1, RAID 5) and how they implement error control mechanisms. (b) Compare RAID 0 and RAID 5 in terms of performance and data redundancy. (c) Provide a practical example of where RAID 1 would be beneficial and explain its impact on data reliability.

### 9. Error Control in Shopping Systems:

(a) How do error control mechanisms like barcodes, QR codes, and check digits help reduce errors in shopping systems? (b) Describe a scenario where error control is crucial for online transactions. (c) Discuss the importance of implementing these systems in enhancing the reliability of retail operations.

### 10. Scaling and Efficiency in Error Control:

(a) How do error control techniques adapt when scaling up for large data environments (e.g., cloud storage)? (b) Compare the efficiency of parity checks, checksums, and Reed-Solomon codes in terms of their application to streaming services. (c) Provide examples of how scaling influences the selection of error control mechanisms in data centers.

### Additional Questions:

### Part (a): New Zealand-Based Organisation

(i) Name a New Zealand-based company or organisation that utilizes error control (e.g., “My school” or a retail company). (ii) Provide two examples of how error control is implemented in this organisation. (iii) Explain how these implementations improve the organisation’s efficiency or accuracy.



### Part (b): Choose Two

- Name a specific type of barcode (e.g., UPC, EAN) and describe the algorithm used for its check digit. Explain its purpose.
- Describe how FEC ensures data integrity in high-speed satellite communications.
- Explain how redundant data is used in error control and provide a practical example.

### Part (c): Choose One

- What are some strategies for future-proofing error control mechanisms in digital communication systems?
- How do human factors influence the design and implementation of error control systems in organisations like the one mentioned in part (a)?

### Part (d): Choose One

- Compare the use of Reed-Solomon codes in QR codes with the error control method used in barcodes. Discuss the advantages and limitations of each.
- Discuss the challenges faced in internet data transmission, such as data corruption, and how error control methods address these problems. Consider the context of the organisation described in part (a).

