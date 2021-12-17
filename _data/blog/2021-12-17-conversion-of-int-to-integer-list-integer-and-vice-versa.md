---
template: BlogPost
path: /java-array-conversions
date: 2021-12-17T18:48:22.497Z
title: 'Conversion of int[] to Integer[], List<Integer> and vice-versa.'
---
This has been a real pain point while solving problems involving data structures and algorithms. Here, I will collect the conversions which is easy and handy to use

**NB: >= Java 8**

### **<u>int\[] to Integer\[]</u>**

```java
int[] array = {1,2,3,4,5,6,7,8,9,10};
Integer[] boxedArray = Arrays.stream(data).boxed().toArray( Integer[]::new );
```

### **<br>**

### **<u>int\[] to List<Integer></u>**

```java
int[] array = {1,2,3,4,5,6,7,8,9,10};
List<Integer> boxedList = Arrays.stream(data).boxed().collect(Collectors.toList());
```

### **<br>**

### **<u>List<Integer> to int\[]</u>**

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

int[] primitiveArray = list.stream().mapToInt(Integer::intValue).toArray();
```

### **<br>**

### **<u>List<Integer> to Integer\[]</u>**

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

Integer[] intArray = new Integer[list.size()];
intArray = list.toArray(intArray);
```

References\
https://stackoverflow.com/questions/880581/how-to-convert-int-to-integer-in-java\
https://stackoverflow.com/questions/960431/how-to-convert-listinteger-to-int-in-java\
https://devqa.io/convert-list-to-array-in-java/
