# Cleancode 

<a id="orgac0ad97"></a>

## meaningful name

-   shorter name better
-   no confusions, don't name 'List' if it is not a list
-   pronounceable names
-   search-able names, not too common
-   no prefixes like m\_
-   class method should have verb
-   don't add extra context


<a id="org10e8095"></a>

## functions

-   small function 
    -   one line in if-else block, this should be a function
-   do one thing 
    -   means steps on one level consists of one thing
    -   one level of abstraction per function
-   replace switch with polymorphism
-   don't be afraid of using long descriptive name
-   less function arguments 
    -   transform function should return the value after transformation
    -   flag argument is UGLY
    -   be aware of dyadic function.
    -   wrap arguments by using objects
    -   argument list
    -   verb + noun function name
-   no side effects, no hidden things
-   in general, output argument should be avoided
-   separate command & query 
    -   error code vs try-catch
-   duplication may be evil in software
-   no continue, break, never go to
-   functions are verb, classes are noun


<a id="org67518f4"></a>

## comments

-   comments are always failure
-   TRUTH SHOULD BE IN CODE


<a id="org08ee8f3"></a>

## formatting

-   variable declaration, local variables should be declared on the top of the function
-   functions caller should be above callee
-   example

    public class CodeAnalyzer implements JavaFileAnalysis {  
      private int lineCount;  
      private int maxLineWidth;  
      private int widestLineNumber;  
      private LineWidthHistogram lineWidthHistogram;  
      private int totalChars;  
    
      public CodeAnalyzer() {    
        lineWidthHistogram = new LineWidthHistogram();  
      }  
    
      public static List<File> findJavaFiles(File parentDirectory) {    
        List<File> files = new ArrayList<File>();    
        findJavaFiles(parentDirectory, files);    
        return files;  
      }
    }

-   instance variables should be declared at the top of the class 
    -   in c++ on bottom
    -   java on top

-   white spaces
-   expand the indent , not in one-line


<a id="orgeadb412"></a>

## objects and data structure

-   object or data structure: 2 approaches 
    -   data structure: expose data, no function.
-   OO code makes easy to add new classes without changing methods
-   procedural code makes it hard to add new data structure, easy to add functions
-   hybrids are worst
-   data transfer object. 
    -   active record, a special form of DTO. having public ( or bean accessed) variables
        and navigational methods like save/find


<a id="org2850871"></a>

## unit tests

-   Note taken on <span class="timestamp-wrapper"><span class="timestamp">[2016-08-17 Wed 00:23] </span></span>   
    IMO, it's very hard to do real test-driven development. but that doesn't means unit test is unnecessary,
    on the contrary, good unit test is helpful. But I also don't think it's good to write unit-test after production 
    code, that is integration test.

-   laws of TDD:
    -   write failing unit test.
-   test and production code are written together
-   having dirty test = having no test
-   test code is as important as the production one
-   readability is very important !
-   build - operate - check pattern, test should have 3 parts, create utility function to make
    code clean.
-   one assert per test
-   single concept per test
-   FIRST rule
    -   fast
    -   independent on each other
    -   repeatable in any environment
    -   self-validating: fail or pass, not a log line
    -   timely: should be written before the production code that makes them pass
-   do not test private methods
-   no need to test all conner cases, test is used to help develop


<a id="orgdb5bf3a"></a>

## classes

-   classes should be small 
    -   a brief class description should be less than 25 words
    -   avoid Processor, Manager
    -   SRP, single responsibility principle
-   in class cohesion should be high
-   use derived classes to replace a single class. SQL generator example
-   class should be open to extension but close to modification
-   minimize coupling. stock exchange example, never depend on concrete class.
    -   write a stock exchange interface, write a testable dummy concrete class


<a id="org617186f"></a>

## systems


<a id="orgc178796"></a>

## test-driven development

-   all about discipline
-   because code rots


<a id="orge7f2408"></a>

## notes from wangyin's art of programming ##


<a id="org3f6d977"></a>

### elegant code. ###

-   tree structure, always have if else block


<a id="orgd31b9d6"></a>

### modulize code ###

-   the function should be less than 50 lines (one page )
-   create utility functions
-   one purpose function 
    -   no "generic" functions
    -   preFoo(); foo() { preFoo();  &#x2026; }

-   avoid using global variable/ member variable to pass info
    -   they don't have IN-OUT pipeline structure


<a id="org90baca8"></a>

### readable code ###

-   meaningful function/variables
-   local variable close to where it's used
-   temp local variable should be short
-   don't reuse local variable, do not be afraid of defining new ones
-   use middle variable.(this contradicts with some coding style)


<a id="orgc725ae5"></a>

### write "simple" code ###

-   avoid using ++i/&#x2013;i
-   NEVER omit {}
-   use ()
-   avoid continue; break;
    -   move break to the while condition
    -   !  continue condition


<a id="orgc752ff1"></a>

### write straight forward code ###

-   avoid using action1() || action2() || action3()
    instead, using multiple if


<a id="org76ad8ff"></a>

### use if-else, avoid using control-flow as else. ###

-   in this case, note that if-else may SHARE common code !
-   I think we could use control flow in the case above


<a id="org032cf68"></a>

### error handling ###

-   when catching error, stop using generic "Exception"
-   try-catch block should be short and neat


<a id="orgfc6d7e3"></a>

### null pointer ###

-   avoid using NULL pointer
    -   not initialization
    -   not return
-   stop catching NullPointerException
-   check null immediately after its possible occurrence


<a id="org8b0aebe"></a>

### stop over-engineering ###

