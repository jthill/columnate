columnate
=========

minimum-width columnation of input lines, row- or column-major order

* Unfilled spots must be right of last row
* Fewer lines presumed better

In column-major order, for any number of rows, fewer columns lays out narrower.
That's not necessarily true for row-major order.

e.g. for 7 items on two lines, in column-major order the choices are:

    1 3 5 7  1 3 5 6 7  1 3 4 5 6 7  
    2 4 6    2 4        2  

and no matter the lengths of the individual items, adding a column can't shift
anything left.  So this always chooses the most balanced column count

But for row-major, we'd have

    1 2 3 4  1 2 3 4 5  1 2 3 4 5 6
    5 6 7    6 7        7

and it's easy to see that if say items 2 and 7 are much longer than items 3, 4,
5, and 6, the second layout will be shorter than the first:

    1  2222222222222222  3  4  5
    6  7777777777777777

In any width that forces 2 rows, columnate will always choose the above
row-major layout for this data.

For ordinary terminal widths this clocks in about 3x slower than /bin/ls, not
bad for an awk.  Widths much larger than that start getting slow, I don't know
whether that's awk blowing the cache or the algorithm itself.

**This is free and unencumbered software released into the public domain**  
**See file LICENSE or refer to <http://unlicense.org/>**  
