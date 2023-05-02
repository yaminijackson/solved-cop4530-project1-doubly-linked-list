Download Link: https://assignmentchef.com/product/solved-cop4530-project1-doubly-linked-list
<br>
This assignment will provide practice with a doubly-linked list, along with practice on the basic concept of an iterator over a container.

Task

In your prior course, you probably saw an example of a singly-linked list. Here is a simple example of such a container, implemented as a template class:

<ul>

 <li><a href="https://www.cs.fsu.edu/~myers/deitel5c++/ch21/Fig21_03_05/">Singly-Linked List class example</a></li>

</ul>

For this assignment you will implement a templated doubly-linked list class, along with an associated iterator class for helping with generic list traversals. In a doubly-linked list, each node has a pointer to the next node AND a pointer to the previous node. The following starter files are provided for you:

<ul>

 <li><a href="https://www.cs.fsu.edu/~myers/cop4530/hw/hw1files/tnode.h">tnode.h</a> — fully defines a templated node class for use in a doubly-linked list. Note that the member data includes a data element, as well as pointers to the next and previous nodes.</li>

 <li><a href="https://www.cs.fsu.edu/~myers/cop4530/hw/hw1files/tlist.h">tlist.h</a> — provides the <strong>declarations</strong> of the template classes TList (the linked list class) and TListIterator (an associated class to help with list traversal).</li>

 <li><a href="https://www.cs.fsu.edu/~myers/cop4530/hw/hw1files/driver.cpp">driver.cpp</a> — contains some sample test calls to the linked list, but should not be considered a complete or thorough set of tests. You will need to create more test cases to fully test your class features. This driver is provided to help illustrate some of the basic class features and concepts, including the use of iterators.</li>

 <li><a href="https://www.cs.fsu.edu/~myers/cop4530/hw/hw1files/driver_output.txt">driver_output.txt</a> — contains the output from running the above sample driver program</li>

</ul>

Your job will be to finish this templated set of classes by defining each of the functions in the TList and TListIterator classes. These should be defined in a file called:

tlist.hpp

Note that there is already a #include at the bottom of tlist.h where your definition file will be brought in. This illustrates a pretty standard format for setting up a templated class.

<h2>Iterators</h2>

The small class called TListIterator is a helper class that can be used in conjunction with the linked list class. This is a common feature used in container classes like this. The purpose of an iterator is to provide a common and non-implementation-specific way of traversing a container, so that mulitple containers could potentially use common algorithms (like sorting and searching functions, for example). This will be explored more in the course. For the iterator class in this assignment, here is a brief sample use:

// suppose that L is a linked list storing ints, and it has   //   already been populated with the values 3, 6, 9, 12, 15, 18, 21   // this call would retrieve a list iterator over the container L  TListIterator&lt;int&gt; itr = L.GetIterator();   // at this point, itr currently is positioned at the first element in   // the list (the 3).   int x = itr.GetValue();             // x would now store 3  itr.Next();                         // itr has advanced to the 6  int y = itr.GetValue();             // y would now store 6  itr.Next();  itr.Next();                         // we have now advanced to the 12  int z = itr.GetValue();             // z now stores 12   itr.Previous();                     // now we have moved backwards, to the 9  int a = itr.GetValue();             // a stores 9.    etc.

This class essentially helps us walk through the linked list in a fairly easy way, with calls to Next() and Previous() to move around.

<h2>Program Details</h2>

Here are general descriptions of the two classes you are to define, along with a general description of each function’s task.

<h3>1) class TList</h3>

The member data of this class consists of pointers to the first and last nodes, a size variable, and a dummy variable of type T that can be used for error-checking situations. Specifically, some of the functions specify to return a stored data item, but if you encounter a situation like an empty list or other situation where there would not BE a valid data item, you can return a reference to the dummy object instead. This is needed because some such functions are pass-by-reference (so that the retrieved item can be modified by the caller under normal situations).

Function descriptions

<ul>

 <li><strong>Default constructor</strong> — creates an empty linked list</li>

 <li><strong>TList(T val, int num)</strong> — creates a linked list containing “num” copies of the data element “val”</li>

 <li><strong>Clear</strong> — clear out the list, resetting it to an empty list</li>

 <li><strong>Big Five</strong>

  <ul>

   <li>Destructor — appropriate clean-up of list, no memory leaks</li>

   <li>Copy constructor — deep copy</li>

   <li>Copy assignment operator — deep copy</li>

   <li>Move constructor — constructor with standard move semantics</li>

   <li>Move assignment operator — assignment with standard move semantics</li>

  </ul></li>

</ul>




<ul>

 <li><strong>Accessors</strong>

  <ul>

   <li><strong>IsEmpty</strong> — returns true if the list is empty, false otherwise</li>

   <li><strong>GetSize</strong> — returns the size (number of data elements) in the list</li>

   <li><strong>GetFirst</strong> — returns the data element in the first node (by reference)</li>

   <li><strong>GetLast</strong> — returns the data element in the last node (by reference)</li>

  </ul></li>

</ul>

Note that error situations in the last two functions would occur if the list was empty (this what the “dummy” item is for).

<ul>

 <li><strong>Endpoint insert/removes</strong>

  <ul>

   <li><strong>InsertFront</strong> — insert the data (parameter) as the first node in the list</li>

   <li><strong>InsertBack</strong> — insert the data (parameter) as the last node in the list</li>

   <li><strong>RemoveFront</strong> — remove the first element in the list. If the list is empty, just leave it empty</li>

   <li><strong>RemoveBack</strong> — remove the last element in the list. If the list is empty, just leave it empty</li>

  </ul></li>

</ul>




<ul>

 <li><strong>Iterator retrieval</strong>

  <ul>

   <li><strong>GetIterator</strong> — create and return an iterator that is positioned on the first node in the list. If list is empty, return default iterator</li>

   <li><strong>GetIteratorEnd</strong> — create and return an iterator that is positioned on the last node in the list. If list is empty, return default iterator</li>

  </ul></li>

</ul>




<ul>

 <li><strong>Insert (2 parameters)</strong>The new data element (second parameter) should be inserted into the linked list just <em>before</em> the position given by the iterator (the first parameter). If the list is empty, just insert the single item. If the iterator doesn’t refer to a node, insert the item at the end of the list.</li>

 <li><strong>Remove (1 parameter)</strong>This function should remove the data item that is given by the iterator (the parameter). The function should return an iterator to the node that is <strong>after</strong> the one that was just deleted. If the initial list was empty, there’s nothing to delete — so just leave it empty and return a default iterator.</li>

 <li><strong>Print</strong>Should print the entire list contents, front to back, separated by the delimiter given in the second parameter. This function may assume that the stored type T has an available insertion &lt;&lt; operator available for printing. Print to the stream given in the first parameter.</li>

 <li><strong>operator+</strong>This is a standalone function that should return a TList object that is the result of concatenating two TList objects together — in parameter order. See driver.cpp program for examples.</li>

</ul>

<h3>2) class TListIterator</h3>

The TListIterator class has only one member data variable — a pointer to the Node to which it currently refers (we’ll call this the current node in the function descriptions below).

<ul>

 <li><strong>Default constructor</strong> — a default iterator should just store the null pointer internally. We’ll call this the “null iterator”.</li>

 <li><strong>HasNext</strong> — returns true if there is another node <em>after</em> the current node, false otherwise</li>

 <li><strong>HasPrevious</strong> — returns true if there is another node <em>before</em> the current node, false otherwise</li>

 <li><strong>Next</strong> — advances the iterator to the next node after the current one (unless currently storing nullptr). Returns an iterator to the new position. (Or return a null iterator if there is no next node).</li>

 <li><strong>Previous</strong> — moves the iterator to the previous node before the current one (if there is one). Returns an iterator to the new position. (Or return a null iterator if there is no previous node).</li>

 <li><strong>GetData</strong> — return the <em>data item</em> at the current node. If the iterator is not pointing to a node (i.e. null pointer), you can use the “dummy” that was defined previously. Note that this is a return by reference.</li>

</ul>

Define all of the functions for these two classes in the file tlist.hpp

<h3>3) Test Program</h3>

Create a test program of your own in the file <strong>mydriver.cpp</strong>. You can use my provided driver.cpp as a general model of how to populate a linked list. Your test program should contain the following tests/illustrations at a minimum:

<ul>

 <li>Tests of all of the functions</li>

 <li>Tests that involve Linked Lists of at least two different stored types. Suggested types: int, double, char, string</li>

 <li>At least 10 tests of each of the following

  <ul>

   <li>InsertFront</li>

   <li>InsertBack</li>

   <li>RemoveFront</li>

   <li>RemoveBack</li>

   <li>Insert (iterator-based)</li>

   <li>Remove (iterator-based)</li>

  </ul></li>

</ul>

The tests for each of these should not be all in a row for any single one. I.e. for best testing, make sure that insert/remove calls of a single function type are frequently interspersed between other types. (This way, a mistake in one will often be revealed by later calls to others)

<ul>

 <li>Clear illustrations of list contents with Print before and after major sets of insert/delete tests. Make your outputs readable and easy to follow for best testing/results.</li>

 <li>At least one test that uses an iterator to traverse the list front to back</li>

 <li>At least one test that uses an iterator to traverse the list back to front</li>

</ul>

<h3>4) makefile</h3>

Create a makefile that configures a build of both my provided driver (driver.cpp) and your test program (mydriver.cpp). i.e. when you type “make” in the directory, it should compile and build both executables. Make your executables named “driver.x” and “mydriver.x”, respectively.

5) General Requirements

<ul>

 <li>Document your code appropriately so that it is readable and easy to navigate</li>

 <li>You may use standard C++ I/O libraries, as well as class libraries like string. You may <strong>NOT</strong> use any of the container class libraries from the STL</li>

 <li>If you wish to add any helper functions to the TList class, you may modify the tlist.h file for this purpose. But do NOT change any of the expected interface function prototypes or add extra member data. Any helper functions you write should be in the private section</li>

 <li>Make sure your files compile and run on linprog.cs.fsu.edu with g++, using the C++11 standard compilation flag. This is where they will be tested and graded</li>

</ul>


