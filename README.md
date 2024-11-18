# EX.-NO-7-IMPLEMENTATION OF SHA-1
## AIM:
  To implement the SHA-I hashing technique using C program.
## ALGORITHM:
  STEP-1: Read the 256-bit key values.
  
  STEP-2: Divide into five equal-sized blocks named A, B, C, D and E.
  
  STEP-3: The blocks B, C and D are passed to the function F.
  
  STEP-4: The resultant value is permuted with block E.
  
  STEP-5: The block A is shifted right by ‘s’ times and permuted with the result 
  
  STEP-6: Then it is permuted with a weight value and then with some other key pair and taken as the first block.
  
  STEP-7: Block A is taken as the second block and the block B is shifted by ‘s’ times and taken as the third block.
  
  STEP-8: The blocks C and D are taken as the block D and E for the final output.
## PROGRAM:
~~~
#include <stdio.h>
#include <string.h>
#include <stdint.h>
#include <stdlib.h> 
#define SHA1_BLOCK_SIZE 64
#define ROTATELEFT(a,b) (((a) << (b)) | ((a) >> (32-(b))))
uint32_t A, B, C, D, E;
uint32_t F(uint32_t t, uint32_t B, uint32_t C, uint32_t D) {
if (t < 20) {
    return (B & C) | ((~B) & D);
} else if (t < 40) {
    return B ^ C ^ D;
} else if (t < 60) {
    return (B & C) | (B & D) | (C & D);
} else {
    return B ^ C ^ D;
}
}
uint32_t K(uint32_t t) {
if (t < 20) return 0x5A827999;
else if (t < 40) return 0x6ED9EBA1;
else if (t < 60) return 0x8F1BBCDC;
else return 0xCA62C1D6;
  }
void pad_message(uint8_t *message, uint64_t *message_length, uint8_t **padded_message) {
uint64_t new_length = (*message_length + 8 + SHA1_BLOCK_SIZE - 1) & ~(SHA1_BLOCK_SIZE - 1);
*padded_message = (uint8_t *)malloc(new_length);
memcpy(*padded_message, message, *message_length);
(*padded_message)[*message_length] = 0x80;  
memset((*padded_message) + *message_length + 1, 0, new_length - *message_length - 9);
uint64_t bit_length = (*message_length) * 8;  
for (int i = 0; i < 8; i++) {
    (*padded_message)[new_length - 1 - i] = (uint8_t)(bit_length >> (i * 8));
}
*message_length = new_length;
}
void sha1_hash(uint8_t *message, uint64_t message_length, uint8_t *hash) {
uint32_t H0 = 0x67452301;
uint32_t H1 = 0xEFCDAB89;
uint32_t H2 = 0x98BADCFE;
uint32_t H3 = 0x10325476;
uint32_t H4 = 0xC3D2E1F0;
uint8_t *padded_message;
pad_message(message, &message_length, &padded_message);
for (uint64_t i = 0; i < message_length; i += SHA1_BLOCK_SIZE) {
    uint32_t W[80];
    for (int t = 0; t < 16; t++) {
        W[t] = (padded_message[i + 4 * t] << 24) |
               (padded_message[i + 4 * t + 1] << 16) |
               (padded_message[i + 4 * t + 2] << 8) |
               (padded_message[i + 4 * t + 3]);
    }
    for (int t = 16; t < 80; t++) {
        W[t] = ROTATELEFT(W[t - 3] ^ W[t - 8] ^ W[t - 14] ^ W[t - 16], 1);
    }
    A = H0;
    B = H1;
    C = H2;
    D = H3;
    E = H4;
    for (int t = 0; t < 80; t++) {
        uint32_t temp = ROTATELEFT(A, 5) + F(t, B, C, D) + E + W[t] + K(t);
        E = D;
        D = C;
        C = ROTATELEFT(B, 30);
        B = A;
        A = temp;
    }
    H0 += A;
    H1 += B;
    H2 += C;
    H3 += D;
    H4 += E;
}
hash[0] = (H0 >> 24) & 0xFF;
hash[1] = (H0 >> 16) & 0xFF;
hash[2] = (H0 >> 8) & 0xFF;
hash[3] = H0 & 0xFF;
hash[4] = (H1 >> 24) & 0xFF;
hash[5] = (H1 >> 16) & 0xFF;
hash[6] = (H1 >> 8) & 0xFF;
hash[7] = H1 & 0xFF;
hash[8] = (H2 >> 24) & 0xFF;
hash[9] = (H2 >> 16) & 0xFF;
hash[10] = (H2 >> 8) & 0xFF;
hash[11] = H2 & 0xFF;
hash[12] = (H3 >> 24) & 0xFF;
hash[13] = (H3 >> 16) & 0xFF;
hash[14] = (H3 >> 8) & 0xFF;
hash[15] = H3 & 0xFF;
hash[16] = (H4 >> 24) & 0xFF;
hash[17] = (H4 >> 16) & 0xFF;
hash[18] = (H4 >> 8) & 0xFF;
hash[19] = H4 & 0xFF;
free(padded_message);
}
int main() {
uint8_t message[] = "Hello, World!";
uint64_t message_length = strlen((char *)message);
uint8_t hash[20];
sha1_hash(message, message_length, hash);
printf("SHA-1 hash: ");
for (int i = 0; i < 20; i++) {
    printf("%02x", hash[i]);
}
printf("\n");
return 0;
}
~~~ 
## OUTPUT:
![image](https://github.com/user-attachments/assets/997fa880-f36a-40f4-809b-ae2261983444)
## RESULT:
  Thus the SHA-1 hashing technique had been implemented successfully.
