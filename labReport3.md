# Lab Report 3
## Part 1

A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
```
@Test
  public void testAverageWithoutLowestRepeat() {
    double[] input1 = {1, 2, 1};
    assertEquals( 1.5, ArrayExamples.averageWithoutLowest(input1), 0.001);
  }
```

An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
```
@Test
  public void testAverageWithoutLowest2() {
    double[] input1 = {1, 2};
    assertEquals( 2, ArrayExamples.averageWithoutLowest(input1), 0.001);
  }
```
The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-02-10%20at%207.31.03%20PM.png?raw=true)
The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
Before

After
```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      sum += num;
    }
    sum -= lowest;
    return sum / (arr.length - 1);
  }
```

## Part 2
