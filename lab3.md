# Lab 3 Report

## Part 1

**1. A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown).**

JUnit Test:

```
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 1, 2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3, 2, 1 }, input1);
	}
```

Associated code:

```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

**2. An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown).**

JUnit Test:

```
  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```

Associated code:

```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

**3. The symptom, as the output of running the two tests above (provide it as a screenshot -- one test should pass, one test should fail).**

<img width="964" alt="Screenshot 2024-05-06 at 9 15 27 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/d7cc7ab9-8287-4b9f-960a-70e8cc870e93">

**4. The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown).**

Before:

```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After:

```
  static void reverseInPlace(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i++){
      newArray[i] = arr[i];
    }
    
    for (int i = 0; i < arr.length; i++) {
      arr[i] = newArray[newArray.length - i - 1];
    }
  }
```

**5. Briefly describe (2-3 sentences) why the fix addresses the issue.**

The fix for the `reverseInPlace` function involves using a temporary array to store a copy of the original array. This allows each element in the original array to be properly replaced with its corresponding element from the opposite end of the temporary array. By doing so, the issue of data being overwritten before it could be reassigned, as seen in the original code, is effectively avoided and the correct reversal is achieved.

---

## Part 2

### grep

**Recursive Search (`-R`):**

**Only Matching (`-o`):**

**Count of Matching Lines (`-c`):**

**Line Number Display (`-n`):**
