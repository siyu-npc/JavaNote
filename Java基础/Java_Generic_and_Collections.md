## Java Generics and Collections
* List< Integer > ~~List< int >~~
The type parameters must always be bound to reference type,not primitive types.
* One subtlety of boxing and unboxing is that == is defined differently on primitive and on reference types.On type **int**,int is defined by equality of values,and on type **Integer**,it is defined by object identify.So both of the following assertions succeed using Sun's JVM:
```
List<Integer> bigs = Arrays.asList(100,200,300);
assert sumInteger(bigs) == sum(bigs);
assert sumInteger(bigs) != sumInteger(bigs);
```
* A further subtlety is that boxed values may be cached.Caching is required when boxing an **int** or **short** value between -128 and 127,a **char** value between '\u0000' and '\u007f',a **byte**,or a boolean;and caching is permitted when boxing other values.(Like Python)
* THe *foreach* loop can be applied to array and any object that implements the interface Iterable<E>,which in turn refers to the interface Iterator<E>.
* Generic Methods and Varargs
Generic methods are indicted by writing <T> at the beginning of the method signature,which declares T as a new type variable.
```
class Lists {
	public static <T> List<T> toList(T[] arr) {...}
}
```
* **vararg feature**:Packing the arguments into an array is cumbersome.The **vararg** feature permits a special,more convenient syntax for the case in which the last argument of a method is an array.To use this feature,replace **T[]** with **T...** in the method declaration.
```
class Lists {
	public static <T> List<T> toList(T... arr) {...}
}
* The type parameter to generic method is inferred,but it may also be given explicitly,as is the following examples:
```
	List<Integer> ints = Lists.<Integer>toList();
    List<Object> objs = Lists.<Object>toList(1,"two");
```
* **List<Integer>** is not a subtype of **List<Number>**,nor is **List<Number>** a subtype a subtype of **List<Integer>**;Arrays behave quite differently,with them,**Integer[]** is a subtype of **Number[]**.
* Wildcards with extends
```
interface Collection<E> {
    ...
	public boolean addAll(Collection<? extends E> c);
	...
}
```

The phrase "**? extends E**" means that it is also OK to add all members of a collection with elements of any type that is a subtype of E.

		In general, if a structure contains elements with a type of the form ? extends E, we can get elements out of the structure, but we cannot put elements into the structure. 
        
* Wildcards with super
```
public static <T> void copy(List<? super T> dst, List<? extends T> src) {
	for (int i = 0; i < src.size(); i++) {
		dst.set(i, src.get(i));
	}
}
```

The quizzical phrase "**? super T**" means that the destination list may have elements of any type that is a supertype of T.

#### The Get and Put Principle
		The Get and Put Principle: use an extends wildcard when you only get values out of a structure, use a super wildcard when you only put values into a structure, and don’t use a wildcard when you both get and put.
        public static <T> void copy(List<? super T> dest, List<? extends T> src)
        
* Wildcards Versus Type Parameters
```
interface Collection<E> {
	...
	public boolean contains(Object o);
	public boolean containsAll(Collection<?> c);
	...
}
```
 The type "**Collection<?>**" stands for:
`Collection<? extends Object>`
Extending Object is one of the most common uses of wildcards, so it makes sense to provide a short form for writing it.
#### Restrictions on Wildcards
		Wildcards may not appear at the top level in class instance creation expressions (new) in explicit type parameters in generic method calls, or in supertypes (extends and implements).
        
	```
List<?> list = new ArrayList<?>(); // compile-time error
Map<String, ? extends Number> map
= new HashMap<String, ? extends Number>(); // compile-time error
```
** Only top-level parameters in instance creation are prohibited from containing wildcards. Nested wildcards are permitted. Hence, the following is legal:**

``` 
List<List<?>> lists = new ArrayList<List<?>>();
lists.add(Arrays.asList(1,2,3));
lists.add(Arrays.asList("four","five"));
assert lists.toString().equals("[[1, 2, 3], [four, five]]");
```

		One way to remember the restriction is that the relationship between wildcards and ordinary types is similar to the relationship between interfaces and classes—wildcards and interfaces are more general, ordinary types and classes are more specific, and instance creation requires the more specific information. Consider the following three statements:
```
List<?> list = new ArrayList<Object>(); // ok
List<?> list = new List<Object>() // compile-time error
List<?> list = new ArrayList<?>() // compile-time error
```
