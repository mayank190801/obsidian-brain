![[Screenshot 2024-09-14 at 5.02.36 PM.png]]

![[Screenshot 2024-09-14 at 5.02.55 PM.png]]


![[Screenshot 2024-09-14 at 5.07.38 PM.png]]


### Iterable and Iterator 
- if you want to use (for x : generic list) on the object of your class 
- You have to make it implement iterable and then you have to make a class and implement interator it! 

```
public class Test {

    public static void main(String[] args) {
        Marks<Integer> m = new Marks<>(5);
        m.add(23);

        Iterator<Integer> iterator = m.iterator();
    }


    public class Marks<T> implements Iterable<T>{
        public T[] arr;
        public int size;

        public Marks(int size){
            arr = (T[])new Object[size];
        }

        public void add(T ele){
            arr[size ++] = ele;
        }

        public int size(){
            return size;
        }

        @Override
        public Iterator<T> iterator() {
            return new MarksIterator(this);
        }

        private class MarksIterator implements Iterator<T> {
            private Marks<T> mark;
            private int index = 0;
            public MarksIterator(Marks<T> mark){
                this.mark = mark;
            }

            @Override
            public boolean hasNext() {
                return index < mark.size();
            }

            @Override
            public T next() {
                return mark.arr[index ++];
            }
        }

    }
}
```
### Core Interfaces  : 

#### Collection Interface 
- boolean containsAll()
- boolean addAll()
- boolean removeAll()
- boolean retainAll()
- void clear() 

#### List Interface 
- Lists are collections that maintain their elements in order and can contain duplicates 
- Elements are in order 
- Each element is position based (starting from index 0)

Methods 
- E get(int index)
- E set(int index, E element)
- void add(int index, E element)
- boolean addAll(int index, Collection)
- E remove(int index)

Implementation 
- ArrayList
- LinkedList
- Vector 

##### ArrayList
- It is a dynamic array 
- Internally uses normally with default capacity, when capacity is reached then it creates a new array with double the size! 
- Now the old array will not be in use and the garbage collected in the next garbage collection

##### Vector 
- legacy class which implement List interface
- dynamic in nature 
- unlike ArrayList class ~ it is thread-safe in nature, meaning concurrent calls will not sacrifice the integrity 
- Slight performance penalty due to Synchronisation 

##### LinkedList 
- uses a doubly linked list 
- Insertions and deletions are very efficient 

### ArrayList Vs LinkedList
- position based access has constant time performance for ArrayList and vector class
- When frequent insertions and deletions occurs inside a list, a LinkedList can be worth considering 
- ArrayList is better at appending to and removing at the end, iteration, and random access. It also uses way less memory (LinkedList uses about 5 times as much).
- LinkedList can also be used as queue because it implement Queue interface as well 

![[Screenshot 2024-09-14 at 5.58.49 PM.png]]


######  Always code against the interface 
```

ArrayList

List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

list.set(1, 100);

- Creating array from ArrayList

Integer[] arr = alist.toArray(new Integer[0]);

- You can pass any sort of collection in the constructor and it will 
create the list for you with those elements. 

List<Integer> alist = new ArrayList<>(list);

- This add all the elements from list to alist 

alist.addAll(list);
alist.indexOf(3);
alist.lastIndexOf(5);

- Below you are not creating a new arraylist, you just referencing to the alist only but with reference from 1st index to 4th index 
- Basically shallow copy

List<Integer> blist = alist.subList(1, 5);
blist.set(1, 100);   //updates both the arraylists 

LinkedList 

List<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(3);

- This returns you the iterator object which is mentioned in below docs

ListIterator iterator = list.listIterator();
sout(iterator.next()) - prints current and takes pointer to next
sout(iterator.next()) 
sout(iterator.previous()) - move to previous and prints current

```

#####  Why using Integer and not int? 
- Because int, float, double are primitive types 
- And generic types requires reference types  (Integer, Double, Float are just wrapper classes)

![[Screenshot 2024-09-14 at 6.15.32 PM.png]]

- Basically bidirectional iterator for list 
- Extends Iterator interface and allows the list to be traversed in either direction using next() and prev()


#### Queue 
- The queue interface extends the Collection interface with the following methods : 
- boolean add();
- boolean offer();  ~ does not throw any kind of exception 
- E poll();
- E remove();
- E peek();
- E element();

##### Deque
- It allows for double ended queue, elements can be inserted and removed from the back and front 

Adding Elements
- offerFirst();
- offerLast();
- addFirst();
- push(); (same as above)
- addLast();

Removing Elements 
- pollFirst();
- pollLast();
- pop();
- removeFirst();
- removeLast();

Examine 
- peekFirst();
- peekLast();
- getFirst();
- getLast();

###### Just use ArrayDeque for both Queue and Stack (it provides pretty cool features)
- You can use LinkedList for queue but just learn one no??? (get better at one implementation)
- ArrayDeque is faster than LinkedList: Due to its array-based implementation 

```
Queue  //FIFO

Queue<Integer> que = new ArrayDeque<>();  //more efficient in terms of space
Queue<Integer> que = new LinkedList<>();

que.add(1);
que.poll();
que.peek();
que.isEmpty();

Stack  //LIFO

Stack<Integer> stack = new Stack<>()      // stack extends vector class 

stack.add();
stack.pop();
stack.peek();
stack.isEmpty();

Deque<Integer> stack = new ArrayDeque<>(); //preffered
Deque<Integer> stack = new LinkedList<>();
ArrayDeque<Integer> stack = new ArrayDeque<>();

stack.addFirst();
stack.addLast();
stack.pollFirst();
stack.pollLast();

```


##### Priority Queue
- It works on priority. Based on priority heap, if same priority the other item will be chosen randomly. 
- Traversal using iterator does not work (NOT A GOOD IDEA TO USE IT)

``` 
PriorityQueue<Integer> pq = new PriorityQueue();
pq.add(3);

//traverse the pq for top 2 elements

List<Integer> ls = new ArrayList<>();
int indx = 0;
while(!pq.isEmpty()){
	if(indx == 2) break;
	ls.add(pq.poll());
	indx++
}
sout(ls);
sout(pq);

public class StudentMarks implements Comparable<StudentMarks>{
	int a;
	int b;
	
	StudentMarks(int a, int b){
		this.a = a;
		this.b = b;
	}

	@Override
	public int compare(StudentMarks o){
		return this.a - o.a;
	}	
}

- Now it work, because Comparable interface was implemented  

way 1 
PriorityQueue<StudentMarks> pq = new PriorityQueue<>();

way 2
PriorityQueue<StudentMarks> pq = new PriorityQueue<>(Collections.reverseOrder());

way 3
PriorityQueue<StudentMarks> pq = new PriorityQueue<>((a,b) -> a.a - b.a);

way 4 (best use case)
PriorityQueue<StudentMarks> pq = new PriorityQueue<>((a,b) -> {
	return a.a - b.a;
});

```


#### Sets

![[Screenshot 2024-09-15 at 12.03.30 PM.png]]

- containsAll
- addAll
- removeAll
- retainAll
- clear

```
Set<Integer> set = new HashSet<>();
set.add(1);
set.add(2);
set.add(3);
set.add(2);

set.remove(2);
set.clear(); 

set1.retainAll(set2);  // intersection of two sets (updates set1 only)
set1.removeAll(set2);  // remove all elements common (updates set1 only)
set1.addAll(set2);     

- Below is not guarenteed to return any sorted order
for(int x : set1){
	sout(x);
}

- what about custom class ? 

public class StudentMarks implements Comparable<StudentMarks>{
	int a;
	int b;
	
	StudentMarks(int a, int b){
		this.a = a;
		this.b = b;
	}

	@Override
	public int compare(StudentMarks o){
		return this.a - o.a;
	}	

	@Override
	public int hashCode(){
		//implement this because it tells which bucket the data might be stored
	}

	@Override 
	public int equals(Object obj){
		//how to know if two obj are equals, write code for that
	}
}

```

- LinkedHashSet can also be used 
- It provides the insertion order to be maintained (pretty cool, don't know about the usecase)
- Slight performance issues 


### Sorted Set Interface
- extends Set interface for providing sorted sets functionality 
- Balanced binary search tree is used 
- Using iterator or for loop returns elements in sorted order 
- E first();
- E last();

### NavigableSet Interface 

![[Screenshot 2024-09-15 at 12.14.47 PM.png]]

```

NavigableSet<Student> set = new TreeSet<>((s1, s2) -> s1.getMarks() - s2.getMarks());

set.ceiling();  //greater than or equal to
set.floor();    //smaller than or equal to 
set.higher();   //strictly greater
set.lower();    //strictly smaller 

set.pollFirst();   //remvoe first
set.pollLast();    //remove last 

- 4 ways of doing this 

Set<Integer> set1 = new TreeSet<>();  
SortedSet<Integer> set4 = new TreeSet<>();  
NavigableSet<Integer> set3 = new TreeSet<>();
TreeSet<Integer> set2 = new TreeSet<>();  

```

![[Screenshot 2024-09-15 at 12.32.08 PM.png]]
### Map 
- mapping defines key to values pair 
- does not allow duplicated keys (keys are unique)
- Both the keys and values must be objects with primitive values.
- mapping can be viewed as a collection ~ a key, a value, a set value of collection

Methods 
- put(k, v)
- get(k)
- remove(k)
- containsKey(k)
- containsValue(v)
- size()
- isEmpty()

![[Screenshot 2024-09-15 at 12.37.22 PM.png]]

![[Screenshot 2024-09-15 at 12.38.47 PM.png]]

##### Implementation of Maps 
- HashMap and HashTable are unordered maps.
- LinkedHashMap are ordered maps.
- TreeMap implements are sorted maps.
- HashMap is not thread-safe and permits one null key. 
- HashTable is thread-safe and permits non-null keys and values only  (comes with a performance penalty).
- LinkedHashMap can maintain its element access order, (last recently used or most recently used)
- Ordering mode can be specificed in the constructor of LinkedHashMap class (LRU cache)
- Both HashMap and LinkedHashMap are comparable performance 
- Operation for searching key ~ constant
- Operation for searching value ~ linear 
- Adding, removing and finding entries in a LinkedHashMap are slightly slower 

``` 

Map<String, Integer> map = new HashMap<>();  
map.put("mayank", 1);  
map.put("singh", 2);  
map.put("random", 3);  
  
map.get("mayank");  
map.getOrDefault("singh", 0);  
map.containsKey("random2");  
map.remove("singh");  
  
map.putIfAbsent("random222", 1);  
  
Set<Map.Entry<String, Integer>> collection = map.entrySet();  
for(Map.Entry<String, Integer> entry : collection){  
System.out.println(entry.getKey() + " " + entry.getKey());  
}  
  
Set<String> keys = map.keySet();  
for(String key : keys){  
System.out.println(key + " " + map.get(key));  
}

```

#### SortedMap 
![[Screenshot 2024-09-15 at 1.10.32 PM.png]]
![[Screenshot 2024-09-15 at 1.11.16 PM.png]]
![[Screenshot 2024-09-15 at 1.18.38 PM.png]]
![[Screenshot 2024-09-15 at 1.19.40 PM.png]]

```

NavigableMap<Integer, String> nmap = new TreeMap<>((a, b) -> b - a);  
nmap.put(1, "random");  
nmap.put(4, "mayank");  
nmap.put(8, "gamer");  
  
System.out.println(nmap);  
Set<Integer> keySet = nmap.keySet();  
nmap.ceilingKey(3);  
nmap.floorKey(5);  
  
nmap.pollFirstEntry();  
nmap.pollLastEntry();  
  
nmap.ceilingEntry(4).getKey();

```

### Extra

```

Integer[] arr = new Integer[]{1,2,3,4,5,6};
Arrays.sort(arr);
Collections.sort(list);
Collections.sort(list, Collections.reverseOrder());
List<Integer> list = Arrays.asList(arr)
List<Integer> list = Arrays.asList(1,2,3,4,5,6);

```

Question to test your theory on 
- Q1 - What would happen if you sort the subList only? How will that affect the bigger list?? 
- Q2 - Check if this is the correct way of doing it - Integer[] arr = alist.toArray(new Integer[0]);
- Q3 - how to use pair as a key in map?? (maybe implement hashCode, equals and comparator )