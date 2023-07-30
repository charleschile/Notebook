# CS61B Week 2

## Lecture 3.1

### 1. testing and selection sort

programmar believe their code works because of tests they write themselves 

先写test程序

### Ad Hoc Testing

在java里面，==比较的是存储的address

```java
public class TestSort {
    public static void testSort() {
        String[] input = {"i", "have", "an", "egg"};
        String[] expected = {"an", "egg", "have", "i"};
        Sort.sort();
        if (!java.util.Arrays.equals(input, expected)) {
            System.out.println("Error! There seems to be a problem with Sort.sort.");
        }
        for (int i = 0; i < input.length; i++) {
            if (!input[i].equals(expected[i])) {
                System.out.println("Mismach in position " + i + ", expected: " + expected[i] + ", but got: " + input[i]);
            }
        }
    }
    public static void main(String[] args) {
        testSort();
    }
}

```

### JUnit Testing

```java
public class TestSort {
    public static void testSort() {
        String[] input = {"i", "have", "an", "egg"};
        String[] expected = {"an", "egg", "have", "i"};
        Sort.sort();
        org.junit.Assert.assertArrayEquals(expected, input);

    }
    public static void main(String[] args) {
        testSort();
    }
}

```



And the information we would get is:

```bash
Exception in thread "main" arrays first differed at element [0]; expected:<[an]> but was:<[i]>
	at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
	at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
	at org.junit.Assert.internalArrayEquals(Assert.java:534)
	at org.junit.Assert.assertArrayEquals(Assert.java:285)
	at org.junit.Assert.assertArrayEquals(Assert.java:300)
	at TestSort.testSort(TestSort.java:6)
	at TestSort.main(TestSort.java:10)
Caused by: org.junit.ComparisonFailure: expected:<[an]> but was:<[i]>
	at org.junit.Assert.assertEquals(Assert.java:117)
	at org.junit.Assert.assertEquals(Assert.java:146)
	at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
	at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
	... 6 more
```



### Selection Sort （选择排序）

 









## Lecture 2.1

## Lecture 2.2

