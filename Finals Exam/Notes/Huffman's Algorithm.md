- used in transmitting data
- one of the techniques in <span style="color:#77c5fd">finding optimal prefix length code</span>
- implemented using a <mark style="background: #5478C2A6;"><font color="white">forest</font></mark> -> a collection of trees
- creates a special, shorter code for each character to save space when storing a long message

## *Steps*

1. initially, each character is in a one-node tree by itself
2. while (# of trees > 1) {
     <span style="color:#77c5fd">a.</span> select 2 trees with the smallest <span style="color:#77c5fd">possibility / frequency</span>
     <span style="color:#77c5fd">b.</span> create a bigger tree from the 2 selected trees
     <span style="color:#77c5fd">c.</span> make the sum of their probability the root of the new tree
     }
3. label the left and right subtrees <span style="color:#77c5fd">0 & 1</span> respectively

## *Example*

![[../Media/Pasted image 20251211040858.png]]
![[../Media/Pasted image 20251211043102.png]]

4. Once the single final tree is built, you start from the <mark style="background: #5478C2A6;"><font color="white">root</font></mark> (the top) and work your way down to the original characters (the <mark style="background: #5478C2A6;"><font color="white">leaves</font></mark>).
	- Label the path to the <span style="color:#77c5fd">left branch</span> with a <span style="color:#77c5fd">'0'</span>.
	- Label the path to the <span style="color:#77c5fd">right branch</span> with a <span style="color:#77c5fd">'1'</span>.
5. The Huffman Code for any character is the sequence of 0s and 1s you follow from the root down to that character.
     - <span style="color:#77c5fd">a:</span> **The longest path** on the '0' side (left branch of the root).
	 - <span style="color:#77c5fd">b:</span> **The shortest path.** This symbol must have been part of the .40 or .60 group and placed very high up in the tree (e.g., the .40 node itself).
	 - <span style="color:#77c5fd">c:</span> A medium-length path on the '0' side.
	 - <span style="color:#77c5fd">d:</span> A short path, starting with '0' (the left branch of the root).
	   
	   Note: In the context of <span style="color:#77c5fd">Huffman's Algorithm</span> and data compression, when we ask what is "longer" or "shorter," we are always referring to the <span style="color:#77c5fd">number of bits</span> in the code, which is its <span style="color:#77c5fd">length</span>. 
	   
	   So why was 'a' the longest path?
	   Look at its <span style="color:#77c5fd">probability (0.12)</span> relative to the other symbols and how the merging process occurred in the notes.
	    - <span style="color:#77c5fd">Its probability is relatively low:</span> The symbols with the lowest probabilities are 'd' (0.08), 'b' (0.10), and 'a' (0.12). These are the first ones targeted for merging.
	    - <span style="color:#77c5fd">It was absorbed deep inside a sub-tree:</span> Because 'a' was one of the lower-frequency symbols, it was pulled into a sub-tree early on. Every time that sub-tree merged with another, it added a new bit (level/depth) to 'a's code.
	      
	In short, **low probability means early merges**, and early merges mean deeper in the tree and a longer code.
6. <mark style="background: #5478C2A6;"><font color="white">Final Calculation: Average Code Length</font></mark>
   The point of this is to reduce the average length of the message.
    ![[../Media/Pasted image 20251211051247.png]]
    - For each symbol, multiply its **Probability** by the **Depth** of its final code (which is the code's length).
    - Sum up all these results.$$\text{Avg Code Length} = \sum (\text{Probability} \times \text{Code Length})$$
    - <mark style="background: #5478C2A6;"><font color="white">Result = 1.15</font></mark>
    
    This value (1.15 bits/symbol) is the average number of bits needed to represent a character using the Huffman codes, which is less than the 3 bits/symbol needed if you used a fixed-length code for 5 symbols ($\lceil\log_2 5\rceil = 3$).


