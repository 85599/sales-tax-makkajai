[![Build Status](https://www.travis-ci.org/Arci/sales-taxes.svg?branch=master)](https://www.travis-ci.org/Arci/sales-taxes)

# Sales Taxes Makkajai
Basic sales tax is applicable at a rate of 10% on all goods, except books, food, and medical products that are exempt. Import duty is an additional sales tax applicable on all imported goods at a rate of 5%, with no exemptions.

When I purchase items I receive a receipt which lists the name of all the items and their price (including tax), finishing with the total cost of the items, and the total amounts of sales taxes paid. The rounding rules for sales tax are that for a tax rate of n%, a shelf price of p contains (np/100 rounded up to the nearest 0.05) amount of sales tax.

# Assumptions

## Input format
The input format is intended as the one outlined in the examples so I suppose a file in that format should be given to the program for parsing before any processing.

The implemented parser (`TextualBasketParser`) implements the interface `BasketParser` that accept an `InputStream` and returns the parsed basket as a POJO so that more parsers can be added if needed.

Within the `data/` directory are provided the three baskets stated in the problem description.

## Output format
The output format is intended as the one in the examples so I suppose the user wants the ability to output it to a file.

The implemented writer (`TextualReceiptWriter`) implements the interface `ReceiptWriter` that accept a `Receipt` and returns a string representation of it so that more parsers can be added if needed.

## Products categories
I suppose that a file containing the categories of the various products is supplied at startup, the file is such that:
- is a CSV with two columns: 
    - *product*, that is the product name (possibly without the _imported_ verb)
    - *category*, that is the category to which it belongs

Moreover I assumed the following:
- each product has one and only one category
- if a product cannot be found within categories it's supposed to be eligible for the basic sales tax
- categories can be held in memory. A `HashMap` has been used to store them, otherwise they should be saved persistently on a DB or the file read by chunk

Within the `data/` directory is provided an example of the categories CSV file.

# Build the application
The application can be build with Maven:

```
mvn clean instal
```

# Run the application
The application is written in Java using Oracle's JDK11:

```
java -jar SalesTaxes 
    -c "/path/to/categories.csv" 
    -b "/path/to/basket.txt" 
    -e "food","books","medical" 
    -o "/path/to/result.txt"
```

Giving no arguments the help is printed:

```
usage: SalesTaxes
 -c,--categories <arg>   the categories file path
 -b,--basket <arg>       the shopping basket file path
 -e,--exclude <arg>      categories excluded from base tax
 -o,--output <arg>       the file to which output the receipt
```

# Solutions

The test `SalesTaxesProblemsTest` contains three test cases for the three problem stated in the problem description.

## Assumption 
- in problem #1 output a wrongly placed space character has been removed between "book" and ":"
- problem #3 the last product differ from input to output, "box of *imported* chocolates" and "*imported* box of chocolates" respectively, the former has been chosen

## License
The **SalesTaxProblem-Makkajai** is licensed under the terms of the [MIT license](LICENSE) and is available for free.

## Links
-   [Issue tracker](https://github.com/85599/sales-tax-makkajai/issues)
-   [Source code](https://github.com/85599/sales-tax-makkajai)

## Authors
* **Khushal Jain** - [Khushal Jain](https://github.com/85599/)


## Acknowledgments
* Hat tip to anyone whose code was used.
* Myself :P

<br><br>
<p align="center">
  Made with ?????? by <a href="https://github.com/85599">85599</a>
</p>

![wave](http://cdn.thekrishna.in/img/common/border.png)

