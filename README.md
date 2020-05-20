# File-Compression-using-Huffmann-Encoding-and-Decoding
Reducing the size of the file using Huffmann Encoding and Decoding.
As we know each character is stored in a combination of 8 bits.This is known to be a Fixed Length Encoding. But this is not the optimized solution for our problem as each character is using fixed that is 8 bits for the storage.For example our document contains the word “abcbba”.As the no of characters are 7 and each char will take 8 bits to store,so total memory consumption will be 7*8=56 bits .But if we derive a concept such that the characters which are coming in high frequency should have less storage space(bits), it will help in reducing the size of the weights.

Taking the above example of string”abcbba”. The frequency of a,b,c are 2,3,1 respectively.So if we assign min no of bits in b and larger no of bits for c as compared to c we can reduce the size. Suppose we provide 10 for a, 0 for b and 100 for c. So now the size will be (2*2+1*3+3*1)=10 bits.So this technique would help us in reducing the size of the document.

The main logic arises when we see the pattern of the bits that will be generated such that there would not be any problem in the decoding of the values. As the encoded values from alphabet to binary will be 1001000010. But our system can decode it to like 100 10 0 0 0 10 that is “cabbba”. The problem can be resolved using the concept of Uniquely Decodable Codes. These uniquely decodable codes and prefix free codes are those in which no code is a prefix of another code. So binary numbers should be generated in format such that any binary number they are not prefixes of each other.

We will use a priority queue for building Huffman trees where the node with lowest frequency has highest priority.




Pseudo Code

There are mainly two major parts in Huffman Coding:-
1) Build a Huffman Tree from input character

Procedure Huffman(C):     // C is the set of n characters 
n = C.size
Q = priority_queue()
for i = 1 to n
{
    n = node(C[i])
    Q.push(n)
}

while Q.size() is not equal to 1
{
    Z = new node()
    Z.left = x = Q.pop
    Z.right = y = Q.pop
    Z.frequency = x.frequency + y.frequency
    Q.push(Z)
}
return Q

2) Traverse the Huffman Tree and assign codes to characters.
After building the tree we will extract codes as following:
We start from the root and do the following until a leaf is found.
If the current bit is 0, we move to the left node of the tree.
If the bit is 1, we move to the right node of the tree.
If during traversal, we encounter a leaf node, we print the character of that particular leaf node and then again continue the iteration of the encoded data starting from step 1
Since efficient priority queue data structures require O(log(n)) time per insertion,and a complete binary tree with n leaves has 2n-1 nodes and huffman coding tree is a complete binary tree, this algo operates in O(nlog(n)),where n is the number of characters.

Brief description of modules or work that is still left

We have successfully converted our text into Huffman codes now we have to retrieve our original text using these codes. Data retrieval is just translating the stream of prefix codes to individual byte value, usually by traversing the Huffman tree node by node as each bit is read from the input stream.
