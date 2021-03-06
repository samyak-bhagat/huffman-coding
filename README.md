### Huffman Algorithm
Huffman coding is a lossless data compression algorithm. The idea is to assign variable-length codes to input characters, lengths of the assigned codes are based on the frequencies of corresponding characters. The most frequent character gets the smallest code and the least frequent character gets the largest code.

The variable-length codes assigned to input characters are Prefix Codes, means the codes (bit sequences) are assigned in such a way that the code assigned to one character is not the prefix of code assigned to any other character. This is how Huffman Coding makes sure that there is no ambiguity when decoding the generated bitstream. 

Let us understand prefix codes with a counter example. Let there be four characters a, b, c and d, and their corresponding variable length codes be 00, 01, 0 and 1. This coding leads to ambiguity because code assigned to c is the prefix of codes assigned to a and b. If the compressed bit stream is 0001, the de-compressed output may be “cccd” or “ccb” or “acd” or “ab”.

There are mainly two major parts in Huffman Coding

1. Build a Huffman Tree from input characters.
2. Traverse the Huffman Tree and assign codes to characters.

### Steps to build Huffman Tree

Input is an array of unique characters along with their frequency of occurrences and output is Huffman Tree. 

1. Create a leaf node for each unique character and build a min heap of all leaf    nodes (Min Heap is used as a priority queue. The value of frequency field is used to compare two nodes in min heap. Initially, the least frequent character is at root)

2. Extract two nodes with the minimum frequency from the min heap.
 
3. Create a new internal node with a frequency equal to the sum of the two nodes frequencies. Make the first extracted node as its left child and the other extracted node as its right child. Add this node to the min heap.

4. Repeat steps#2 and #3 until the heap contains only one node. The remaining node is the root node and the tree is complete.

### Traverse the Huffman Tree and assign codes to characters.
Traverse the tree formed starting from the root. Maintain an auxiliary array. While moving to the left child, write 0 to the array. While moving to the right child, write 1 to the array. Print the array when a leaf node is encountered.

### Python Implementaion of Huffman Coding

Consists **compress** and **decompress** function.

### Compress function
1. Build frequency dictionary
2. Build priority queue (using MinHeap ) 
3. Build Huffman Tree by selecting 2 min nodes and merging them 
4. Assign codes to characters (by traversing the tree from root)
5. Encode the input text(by replacing character with its code)
6. If overall length of the finall encoded bit streams is not multiple of 8, add some padding to the text
7. Store this padding information (in 8 bits) at the start of the overall encoded bit stream
8. Write the result to an output binary file

### Decompress function
1. Read binary file 
2. Read padding information. Remove the padding bit
3. Decode the bits -read the bits and repalce the valid Huffman Code bits with the character values
4. Save the decoded data into the output file


