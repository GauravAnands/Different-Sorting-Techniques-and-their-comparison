# Different-Sorting-Techniques-and-their-comparison

<b>Introduction</b></br>
Sorting is ordering a list of objects. We can distinguish two types of sorting. If the number of objects is small enough to fits into the main memory, sorting is called internal sorting. If the number of objects is so large that some of them reside on external storage during the sort, it is called external sorting. In this chapter we consider the following internal sorting algorithms<b>:-</b></br>
<ul>
  <li> Bucket sort </li>
  <li> Bubble sort </li>
  <li>Insertion sort</li>
  <li> Selection sort</li>
  <li>Heapsort</li>
  <li>Mergesort</li>
</ul> 

<b>O(n) algorithms - </b>
Bucket sort</br>
<b>O(n2) algorithms - </b>
Bubble Sort, Selection Sort, Insertion Sort.</br>
<b>O(n log n) algorithms - </b>
Mergesort</br>

<b>Sorting in Java</b></br>
In this section we discuss four different ways to sort data in Java.</br>
<b>Arrays of primitives</b></br>
An array of primitives is sorted by direct invocation of Arrays.sort method</br>

int[] a1 = {3,4,1,5,2,6};
Arrays.sort(a1);

Arrays of objects
In order to sort an array of abstract object, we have to make sure that objects are mutually comparable. The idea of comparable is extension of equals in a sence than we need to know not only that two objects are not equal but which one is larger or smaller. This is supported by the Comparable interface. This interface contains only one method with the following signature:
	public int compareTo(Object obj);
The returned value is negative, zero or positive depending on whether this object is less, equals or greater than parameter object. Note a difference between the equals() and compareTo() methods. In the following code example we design a class of playing cards that can be compared based on their values:

<pre>
class Card implements Comparable<Card>
{
   private String suit;
   private int value;

   public Card(String suit, int value)
   {
      this.suit = suit;
      this.value = value;
   }
   public int getValue()
   {
      return value;
   }
   public String getSuit()
   {
      return suit;
   }
   public int compareTo(Card x)
   {
      return getValue() - x.getValue();
   }
}
</pre>
Suppose that the Card class implements the Comparable interface, then we can sort a group of cards by envoking by Arrays.sort method.
<pre>
Card[] hand = new Card[5];
Random rand = new Random();
for (int i = 0; i ‹ 5; i++)
	hand[i] = new Card(rand.nextInt(5), rand.nextInt(12));
Arrays.sort(hand);
</pre>
It is important to recognize that if a class implements the Comparable interface than compareTo() and equals() methods must be correlated in a sense that if x.compareTo(y)==0, then x.equals(y)==true. The default equals() method compares two objects based on their reference numbers and therefore in the above code example two cards with the same value won't be equal. And a final comment, if the equals() method is overriden than the hashCode() method must also be overriden, in order to maintain the following properety: 
<pre>
if x.equals(y)==true,
then x.hashCode()==y.hashCode()
</pre>

<b>Collection of comparable objects</b></br>
Mutually comparable objects in a collection are sorted by Collections.sort method:
  <pre>
ArrayList‹Integer> a2 = new ArrayList‹Integer> (5);

Collections.sort(a2);
</pre>
<b>Comparator</b></br>
The Comparable interface does not provide a complete solution. The main problem is that the above code works only for objects that have that particular implementation of the compareTo method. Once you implemented compareTo , you don't have much flexibility. Moreover, it is not always possible to decide on a "correct" meaning for compareTo. This method can be based on many different ideas. The solution to this problem is to pass the comparison function as a parameter. Such comparison function in Java is implemented as the Comparator interface. Consider a poker hand: to do a fast evaluation you want to sort your cards either by value or by suit. The way to support these two different criterias is to create two classes SortByValue and SortBySuit that implements Comparator interface
<pre>
class SuitSort implements Comparator
{
   public int compare(Object x, Object y)
   {
      int a = ((Card) x).getSuit();
      int b = ((Card) y).getSuit();

      return a-b;
   }
}
</pre>
and then pass a comparison function into a sorting routine. In Java, you cannot pass a method; you should wrap a class around it.</br>
<pre>
Arrays.sort(hand, new SuitSort());
</pre>
This new object SuitSort is called a functor, and the style of programming is called a functional programming. The functor is a simple class which usually contains no data, but only a single method. We can design different comparison functions by simply declaring new classes, one class for each kind of functionality. An instance of this class (which implements the interface) is passed to algorithm, which in turn calls the method from the function object.

