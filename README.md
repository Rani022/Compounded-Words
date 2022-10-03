# Compounded-Words
Word Composition Problem:
Write a program that reads a file containing a sorted list of words (one word per line, no spaces, all lower case), then identifies the longest word in the file that can be constructed by concatenating copies of shorter words also found in the file.

For example, if the file contained:

   cat
   cats
   catsdogcats
   catxdogcatsrat
   dog
   dogcatsdog
   hippopotamuses
   rat
   ratcatdogcat
The strategy used in this solution has two components: breaking the problem into smaller pieces to enable concurrency, and optimising the data to enable effective processing.

Data Optimization:
Words are sorted in descending order of word length after being read into a List<String>, starting with the longest words. As a result, when searching for the longest compound word, the algorithm prioritises processing lengthier words. As the longest compound word frequently occurs among the lengthier terms in the test set, this helps performance on the majority of test sets.
Word Length Based Indexes – Words are mapped into lists according to their length as they are read into memory. The words that are less than length X are used to generate an index after all the words have been read. These indices are used during list processing so that the algorithm can decide which words should be considered when looking for "sub-words" based on the length that is available. This reduces iterations over impractical answers by allowing the algorithm to only iterate over words that might actually fit in the available space.

Algorithm:
In order to find compound words, the basic approach is to iterate over the target words from longest to shortest, then iterate over the word list for each target word (again from longest to shortest), looking for a match if the target word "starts with" the match word. Recursively try to look for matches in the "tail" of the target word if it begins with the match word. Some words can be constructed using several combinations of subwords, thus if any combination of words includes the target word, it is added to the result set and no longer processed.but for this exercise once a word is considered a compound wordIf it can be made in more than one manner, it doesn't matter or count.
The procedure described here is recursive, however it would be fascinating to find out if it could be accomplished without recursion and how well it would perform.

Beyond concurrency, the algorithm's efficiency depends on minimising the number of match words considered at step. Although the algorithm was designed to locate the longest compound word first, a thorough search was still necessary to locate all compound words.

Alternative Algorithm Tried:
A "binary search"-type approach was also researched in addition to the algorithm that was actually presented. This algorithm accepted matches anywhere throughout the target word rather than just trying to match them at the beginning. This was then used as a pivot point and the "ends" were processed further. It was thought that this strategy would mean (on average) that the recursive checks would be sortier if a match word was in the middle because the key to efficiency was to minimise the words that were iterated for matches. i.e. Given the target term catdograt, the remaining target would be matched against all words of length 6 or less if cat was a match (according to the described methodology), however if dog was a match, two matches of length 3 or fewer would be done.
This strategy was ultimately dropped because it turned out to be less effective.







