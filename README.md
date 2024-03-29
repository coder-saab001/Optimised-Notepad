# Optimised-Notepad 
(Based on research paper https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.301.6716&rep=rep1&type=pdf)

This is an Optimised Notepad which auto-compresses the text-file when the file is saved. Combination of compression Algorithms (LZW compression and Huffman compression algorithms) are used to compress the text file. It was able to achieve an average compression of about 65%. The best compression was about 80%.

## Details
This project is mainly based on Huffman Compression Algorithm that is a greedy lossless compression algorithm. But to take it one step further I have used a subroutine algorithm LZW (Lempel-Ziv-Welch) Compression algorithm. This algorithm is also a lossless compression algorithm that uses a greedy approach.
Although Huffman algorithm would have been enough but to increase its efficiency and compression rate, we have used LZW as a secondary subroutine algorithm. 
So, when a user provides an input file, LZW is implemented on it firstly and then Huffman is used on it for compression.

LZW basically reduces the duplication of data in input which means that by the time data reaches Huffman it has already been reduced to a certain size. 
Then Huffman runs on the compressed input given by LZW and gives each letter/segment of input a certain code that is not a prefix of any other code. 
And at the end, the output we receive is greatly smaller than input and the combination of these two algorithms is better than both of the algorithms if used separately.

## Pseudo code for LZW algorithm
### Encoding

```
 1     Initialize table with single character strings
 2     P = first input character
 3     WHILE not end of input stream
 4          C = next input character
 5          IF P + C is in the string table
 6            P = P + C
 7          ELSE
 8            output the code for P
 9          add P + C to the string table
 10           P = C
 11         END WHILE
 12    output code for P
 ```
 ### Decoding
 
 ```
 1    Initialize table with single character strings
 2    OLD = first input code
 3    C = first character of S
 4    output translation of OLD
 5    WHILE not end of input stream
 6        NEW = next input code
 7        IF NEW is not in the string table
 8               S = translation of OLD
 9               S = S + C
 10       ELSE
 11              S = translation of NEW
 12       output S
 13       C = first character of S
 14       OLD + C to the string table
 15       OLD = NEW
 16   END WHILE
 ```
 
 ## Pseudo code for Huffman algorithm
 ### Encoding
 ```
 Function huffmanEncode(C)  

 1   n = C.size
 2   Q = priority_queue()

 3   for i = 1 to n
 4     n = node(C[i])
 5     Q.push(n)
 6   end for

 7   while Q.size() is not equal to 1
 8      Z = new node()
 9      Z.left = x = Q.pop
 10     Z.right = y = Q.pop
 11     Z.frequency = x.frequency + y.frequency
 12     Q.push(Z)
 13  end while
 14 Return Q
 ```
### Decoding
```
 Function huffmanDecode(root, S)  

 1   n = S.size
 2   current = root
 3   for i=1 to n
 4      if(s[i] == '0')
 5         current = current.left
 6      else
 7         current = current.right
 8      if(current.left == NULL and current.right == NULL)
 9         decodedString += current.data
 10        current = root
 14  return decodedString
```

## Results of test files

1. For very random 1MB test file, it was able to compress to 566KB.
   Compression Ratio: 43.4%.
2. For 2MB test file, containing latin text, it was able to compress to 471KB.
   Compression Ratio: 76.4%.
3. For 516KB of a test file (it was a log file of on of the project having some repeated text), it was able to
   compess to 113KB.
   Compression Ratio: 78.1%.

## Analysis

For commonly use files, containing relevant information the editor can achieve compression of about 70% to 75%.
For random content with no proper meaning, it can achieve compression of about 40% to 50%.

## Limitations

Since the time taken by both of the algorithms is around O(N) for compressing the content, there is efficiency issue for large test files of >=10MB. Tkinter Gui editor also has some performance issue. 
