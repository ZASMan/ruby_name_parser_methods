# Simple Ruby Name Parser

Note: I don't claim that this is a super efficient way to do things, instead I want to share this as a simple example of array/string manipulation for beginners.

This had a specific use case in which I had a CSV spreadsheet of several hundredvalues where every name was in a cell in the format of 'Last, First Middle' or even 'Last, First Middle1 Middle2'. To match up with my data model structure, I needed to extract a first, middle, and last name.
After using Ruby's CSV class to pull the raw name data, I used the following simple methods to extract the names.

