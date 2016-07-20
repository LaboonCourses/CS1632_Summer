# CS 1632 - Software Quality Assurance
Summer Semester 2016

DUE 27 July 2016

## Deliverable 6

For this assignment, you (NOT a group) will use static analysis to improve an implementation of the Sieve of Eratosthenes.  This implementation is found in the GitHub repository:

 will consist of the following steps:

1. Use findbugs to statically analyze the Sieve.java code
2. Fix *all* of the errors found by findbugs (with the exception of "Dead store to local variables" issues)
2. Add two unit tests to the one method found by findbugs which has known functional impact.
2. Use checkstyle with the included configuration file (google_checks_modified.xml) to find any style issues with the Sieve.java code and fix them.

Example:
```
java -jar ~/checkstyle/checkstyle-7.0-all.jar -c ./google_checks_modified.xml ~/pitt/SlowLifeGUI/*.java
```

Code will be on Github (https://github.com/laboon/bug-fodder).  You may fork the repository or copy the files to your own repository, whatever you find easiest.

There are no partners for this deliverable.

The Sieve of Eratosthenes is an ancient technique used for finding all of the prime numbers from the value 1 to n.  It does so by looking through a list of numbers, and look for any multiples of that number.  If any are found, the number must be composite.  This goes up until the square root of n, because that will be the largest number that values have not been caught by previous numbers.  As an example, let's look at a small sieve, with values 1 through 20.

We start with the values [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20], and assume that all of them are prime.

By definition, 1 is considered a "unit"; that is, neither prime nor composite.  It is thus removed when performing the Sieve.

```
[2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
 T  T  T  T  T  T  T  T   T   T   T   T   T   T   T   T   T   T   T]
```


So we start at 2, and "ignore" it, marking it as prime.  We then look at the multiples of 2: 2 * 2 ( = 4), 2 * 3 ( = 6), 2 * 4 ( = 8), 2 * 5 ( = 10), etc. until we get to the maximum value (20).  Each of these multiples are then marked as composite (false).

```
[2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
 T  T  F  T  F  T  F  T   F   T   F   T   F   T   F   T   F   T   F]
```

Now let's move on to 3, and mark it as prime.  All of the multiples of 3 here (6, 9, 12, 15, and 18) are all marked as composite.  Note that some of these (e.g. 6 and 12) has already been marked as composite.

```
[2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
 T  T  F  T  F  T  F  F   F   T   F   T   F   F   F   T   F   T   F]
```

We can ignore 4; it is composite, so any multiples of it would also be composite (and had already been caught by our "2" iteration).  We could theoretically continue and check 5, but since it is greater than the square root of 20, any composite values would have already been caught by earlier iterations (the reason why is left as an exercise for the reader).

We can now see the list of all values still set to true is the list of primes:

```
[2,3,5,7,11,13,17,19]
```

We can confirm that these are indeed all of the prime numbers less or equal to 20.

There is at least one known defect in this implementation (aside from integer max overflow and performance issues).  If you see an uncaught exception, this is considered a defect!

You will use findbugs, as described in class, to find possible bugs in Sieve.java.  At least one of these bugs will cause a visible-to-the-user defect.  For the method which causes this defect, write two unit tests which test this method, including testing the equivalence class that manifested the issue.

Note that findbugs has a known issue with the "Dead store to local variable" analysis.  You may ignore any errors of this kind (you can filter them out or just mentally ignore them).

After you have modified the code, run checkstyle using the included google_checks_modified.xml configuration file on Sieve.java.  Fix all of the issues so that the style is in line with the modified Google code guidelines (these are actual Google Java style guidelines, btw, with only some small modifications by yours truly).  Before turning this in, your checkstyle run should show no issues.

Finally, upload your modified code to GitHub or GitLab for me to examine

For the write-up, include a listing of how you went about fixing the code issues found by the static analysis tools, and any issues you experienced.  This should not be more than a few paragraphs.

Include screenshots of both the findbugs and checkstyle output.

## Format
Every assignment should have a title page with:
* The name of the student
* The title "CS 1632 - DELIVERABLE 6: Static Analysis of the Sieve of Eratosthenes"
* The URL for your git repository

There is no need to print out the code.  It should be available on GitHub or a similar code-sharing site BY THE BEGINNING OF CLASS.


## Grading
* Summary - 10%
* Screenshots of Findbugs and checkstyle output - 10%
* Method fixed - 20%
* Unit tests - 25%
* All linting issues (from checkstyle and findbugs) fixed - 35%

Please feel free to email me or come to office hours to discuss any problems you have. 
 
