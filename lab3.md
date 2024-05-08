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

Example 1: This command recursively searches through the `./technical` directory and all its subdirectories for the string "non-proliferating". It's useful for finding all mentions of gene expression in research files, potentially spread across multiple subdirectories.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -R "non-proliferating" ./technical

./technical/biomed/1471-2407-1-6.txt:        present in non-proliferating cells [ 11, 12]. Ki-67 is an
./technical/biomed/1471-2407-1-6.txt:        has not been detected in non-proliferating cells. During
./technical/biomed/1471-2202-3-3.txt:          proliferating PC12 cells to a non-proliferating
./technical/biomed/1471-2121-3-6.txt:          differentiated, non-proliferating cells in which events
```

Example 2: This command searches for the term "non-proliferating" across all files in ./technical, listing only the filenames that contain the term. It's useful for quickly identifying which documents mention COVID-19 without showing every occurrence.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Rl "non-proliferating" ./technical

./technical/biomed/1471-2407-1-6.txt
./technical/biomed/1471-2202-3-3.txt
./technical/biomed/1471-2121-3-6.txt
```

---

**Only Matching (`-o`):**

Example 1: This command searches for any occurrence of years between 2027 and 2029, printing only the matching parts (just the years), throughout the `technical` directory recursively. Useful for extracting specific data points like years from files.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Ro "202[7-9]" ./technical

./technical/government/Gen_Account_Office/d01591sp.txt:2029
./technical/government/Gen_Account_Office/d01591sp.txt:2029
./technical/government/Gen_Account_Office/d01591sp.txt:2029
./technical/government/Gen_Account_Office/d01591sp.txt:2029
./technical/biomed/1471-2164-2-9.txt:2028
./technical/biomed/1471-2121-3-19.txt:2029
```

Example 2: This command searches through all files in the `./technical/biomed` directory recursively for any occurrence of years from 2020 to 2029. The `-R` option enables recursive search into all subdirectories, and `-o` makes `grep` output only the matched parts, not the entire lines which is useful for extracting references to specific years within a decade, helping to identify when certain studies, experiments, or discussions were documented or referenced.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Ro "202[0-9]" ./technical/biomed
./technical/biomed/1471-2164-2-9.txt:2028
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1476-4598-2-20.txt:2021
./technical/biomed/1471-2105-3-14.txt:2020
./technical/biomed/1471-2105-3-14.txt:2020
./technical/biomed/1471-2105-3-14.txt:2020
./technical/biomed/1471-2105-3-14.txt:2020
./technical/biomed/1471-2350-3-1.txt:2021
./technical/biomed/1471-2377-3-4.txt:2021
./technical/biomed/1471-2202-2-19.txt:2020
./technical/biomed/cc350.txt:2024
./technical/biomed/1471-2121-3-19.txt:2029
./technical/biomed/gb-2002-3-9-research0049.txt:2023
./technical/biomed/1471-2202-3-10.txt:2020
./technical/biomed/1471-2156-4-9.txt:2025
```

---

**Count of Matching Lines (`-c`):**

Example 1: This command counts the lines containing the word "experiment" specifically within the `plos` subdirectory of `technical`. It helps in understanding the extent of experimental discussions in biomedical research papers.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Rc "experiment" ./technical/plos  
./technical/plos/pmed.0020273.txt:0
./technical/plos/journal.pbio.0030032.txt:0
./technical/plos/pmed.0020065.txt:0
./technical/plos/pmed.0020071.txt:0
./technical/plos/pmed.0020059.txt:0
./technical/plos/pmed.0010039.txt:0
./technical/plos/journal.pbio.0020354.txt:0
./technical/plos/pmed.0010010.txt:0
./technical/plos/journal.pbio.0020156.txt:2
./technical/plos/pmed.0020104.txt:0
./technical/plos/pmed.0020272.txt:1
./technical/plos/pmed.0020258.txt:4
./technical/plos/pmed.0020099.txt:0
./technical/plos/journal.pbio.0020140.txt:1
./technical/plos/journal.pbio.0020183.txt:3
./technical/plos/journal.pbio.0020430.txt:3
./technical/plos/journal.pbio.0020394.txt:1
./technical/plos/journal.pbio.0020431.txt:3
./technical/plos/journal.pbio.0020419.txt:0
./technical/plos/pmed.0010013.txt:0
./technical/plos/pmed.0020113.txt:0
./technical/plos/journal.pbio.0020169.txt:3
./technical/plos/pmed.0020098.txt:1
./technical/plos/journal.pbio.0020035.txt:2
./technical/plos/pmed.0020067.txt:0
./technical/plos/pmed.0020073.txt:4
./technical/plos/journal.pbio.0030024.txt:2
./technical/plos/journal.pbio.0020223.txt:0
./technical/plos/pmed.0020249.txt:48
./technical/plos/pmed.0020275.txt:0
./technical/plos/journal.pbio.0020019.txt:1
./technical/plos/pmed.0020088.txt:1
./technical/plos/journal.pbio.0020145.txt:4
./technical/plos/pmed.0020103.txt:5
./technical/plos/pmed.0020117.txt:0
./technical/plos/journal.pbio.0020353.txt:0
./technical/plos/journal.pbio.0020347.txt:0
./technical/plos/journal.pbio.0020420.txt:1
./technical/plos/journal.pbio.0020346.txt:1
./technical/plos/journal.pbio.0020187.txt:0
./technical/plos/pmed.0020116.txt:0
./technical/plos/pmed.0020102.txt:0
./technical/plos/journal.pbio.0020150.txt:4
./technical/plos/pmed.0020062.txt:0
./technical/plos/pmed.0020274.txt:0
./technical/plos/journal.pbio.0020232.txt:1
./technical/plos/journal.pbio.0030021.txt:1
./technical/plos/journal.pbio.0020224.txt:7
./technical/plos/pmed.0020048.txt:1
./technical/plos/pmed.0020060.txt:0
./technical/plos/pmed.0020074.txt:0
./technical/plos/journal.pbio.0020146.txt:0
./technical/plos/pmed.0020114.txt:0
./technical/plos/pmed.0010028.txt:3
./technical/plos/journal.pbio.0020350.txt:5
./technical/plos/journal.pbio.0020190.txt:1
./technical/plos/pmed.0010029.txt:0
./technical/plos/pmed.0020115.txt:0
./technical/plos/journal.pbio.0020147.txt:0
./technical/plos/pmed.0020075.txt:0
./technical/plos/pmed.0020061.txt:3
./technical/plos/pmed.0020210.txt:0
./technical/plos/pmed.0020238.txt:0
./technical/plos/journal.pbio.0030051.txt:1
./technical/plos/journal.pbio.0020068.txt:0
./technical/plos/journal.pbio.0020054.txt:3
./technical/plos/journal.pbio.0020040.txt:1
./technical/plos/pmed.0010066.txt:1
./technical/plos/journal.pbio.0030131.txt:0
./technical/plos/journal.pbio.0020337.txt:13
./technical/plos/pmed.0020198.txt:0
./technical/plos/pmed.0010067.txt:0
./technical/plos/journal.pbio.0020121.txt:0
./technical/plos/pmed.0020007.txt:0
./technical/plos/journal.pbio.0030050.txt:1
./technical/plos/pmed.0020239.txt:0
./technical/plos/journal.pbio.0020241.txt:5
./technical/plos/pmed.0020005.txt:0
./technical/plos/journal.pbio.0020043.txt:0
./technical/plos/pmed.0020039.txt:0
./technical/plos/pmed.0010071.txt:0
./technical/plos/journal.pbio.0030127.txt:0
./technical/plos/pmed.0010058.txt:3
./technical/plos/pmed.0010070.txt:0
./technical/plos/pmed.0010064.txt:1
./technical/plos/pmed.0020158.txt:0
./technical/plos/journal.pbio.0020042.txt:11
./technical/plos/journal.pbio.0020297.txt:7
./technical/plos/pmed.0020206.txt:0
./technical/plos/pmed.0020212.txt:0
./technical/plos/pmed.0020216.txt:0
./technical/plos/journal.pbio.0030094.txt:0
./technical/plos/journal.pbio.0020046.txt:0
./technical/plos/pmed.0020028.txt:0
./technical/plos/journal.pbio.0020052.txt:2
./technical/plos/pmed.0020148.txt:0
./technical/plos/pmed.0020160.txt:0
./technical/plos/pmed.0010048.txt:1
./technical/plos/pmed.0010060.txt:0
./technical/plos/journal.pbio.0030137.txt:1
./technical/plos/journal.pbio.0030136.txt:1
./technical/plos/pmed.0010061.txt:1
./technical/plos/pmed.0010049.txt:0
./technical/plos/pmed.0020161.txt:1
./technical/plos/journal.pbio.0020127.txt:3
./technical/plos/pmed.0020149.txt:0
./technical/plos/journal.pbio.0020133.txt:6
./technical/plos/pmed.0020015.txt:0
./technical/plos/journal.pbio.0020053.txt:1
./technical/plos/journal.pbio.0020047.txt:0
./technical/plos/pmed.0020203.txt:1
./technical/plos/journal.pbio.0030056.txt:0
./technical/plos/pmed.0020201.txt:0
./technical/plos/journal.pbio.0030097.txt:1
./technical/plos/pmed.0020017.txt:0
./technical/plos/journal.pbio.0020125.txt:1
./technical/plos/journal.pbio.0020440.txt:1
./technical/plos/pmed.0010062.txt:2
./technical/plos/pmed.0020189.txt:0
./technical/plos/pmed.0020162.txt:0
./technical/plos/pmed.0020016.txt:0
./technical/plos/pmed.0020002.txt:0
./technical/plos/pmed.0020200.txt:0
./technical/plos/pmed.0020231.txt:0
./technical/plos/journal.pbio.0020263.txt:0
./technical/plos/pmed.0020027.txt:0
./technical/plos/pmed.0020033.txt:1
./technical/plos/journal.pbio.0020101.txt:4
./technical/plos/pmed.0010047.txt:0
./technical/plos/journal.pbio.0030105.txt:1
./technical/plos/journal.pbio.0020302.txt:8
./technical/plos/pmed.0010046.txt:0
./technical/plos/pmed.0010052.txt:0
./technical/plos/pmed.0020191.txt:0
./technical/plos/journal.pbio.0020100.txt:6
./technical/plos/pmed.0020146.txt:0
./technical/plos/journal.pbio.0020262.txt:1
./technical/plos/journal.pbio.0030065.txt:1
./technical/plos/journal.pbio.0020276.txt:0
./technical/plos/pmed.0020232.txt:2
./technical/plos/pmed.0020226.txt:0
./technical/plos/pmed.0020024.txt:0
./technical/plos/pmed.0020018.txt:3
./technical/plos/pmed.0020144.txt:0
./technical/plos/pmed.0020150.txt:0
./technical/plos/journal.pbio.0020116.txt:5
./technical/plos/pmed.0020187.txt:0
./technical/plos/pmed.0010050.txt:0
./technical/plos/pmed.0010051.txt:0
./technical/plos/pmed.0020192.txt:0
./technical/plos/pmed.0010045.txt:6
./technical/plos/pmed.0020145.txt:0
./technical/plos/pmed.0020019.txt:0
./technical/plos/journal.pbio.0020063.txt:1
./technical/plos/journal.pbio.0030076.txt:1
./technical/plos/journal.pbio.0030062.txt:2
./technical/plos/pmed.0020237.txt:0
./technical/plos/journal.pbio.0020067.txt:0
./technical/plos/pmed.0020009.txt:2
./technical/plos/journal.pbio.0020073.txt:0
./technical/plos/pmed.0020035.txt:0
./technical/plos/pmed.0020021.txt:0
./technical/plos/journal.pbio.0020113.txt:0
./technical/plos/pmed.0020155.txt:0
./technical/plos/pmed.0010069.txt:1
./technical/plos/pmed.0010041.txt:0
./technical/plos/pmed.0020182.txt:1
./technical/plos/pmed.0020196.txt:0
./technical/plos/journal.pbio.0020311.txt:1
./technical/plos/journal.pbio.0030102.txt:0
./technical/plos/journal.pbio.0020310.txt:3
./technical/plos/pmed.0020197.txt:0
./technical/plos/pmed.0010068.txt:0
./technical/plos/pmed.0020140.txt:0
./technical/plos/journal.pbio.0020112.txt:0
./technical/plos/pmed.0020020.txt:0
./technical/plos/pmed.0020034.txt:1
./technical/plos/pmed.0020236.txt:0
./technical/plos/journal.pbio.0020272.txt:2
./technical/plos/pmed.0020208.txt:0
./technical/plos/journal.pbio.0020064.txt:2
./technical/plos/pmed.0020022.txt:0
./technical/plos/pmed.0020036.txt:2
./technical/plos/pmed.0010056.txt:10
./technical/plos/pmed.0020195.txt:0
./technical/plos/pmed.0010042.txt:0
./technical/plos/pmed.0020181.txt:0
./technical/plos/journal.pbio.0020306.txt:0
./technical/plos/journal.pbio.0030129.txt:0
./technical/plos/journal.pbio.0020307.txt:0
./technical/plos/pmed.0020180.txt:0
./technical/plos/pmed.0020194.txt:0
./technical/plos/pmed.0020157.txt:0
./technical/plos/journal.pbio.0020105.txt:0
./technical/plos/pmed.0020023.txt:0
./technical/plos/journal.pbio.0020071.txt:0
./technical/plos/pmed.0020235.txt:1
./technical/plos/journal.pbio.0020267.txt:2
./technical/plos/pmed.0020209.txt:0
./technical/plos/pmed.0020246.txt:0
./technical/plos/journal.pbio.0020228.txt:0
./technical/plos/journal.pbio.0020214.txt:3
./technical/plos/pmed.0020050.txt:0
./technical/plos/pmed.0020118.txt:0
./technical/plos/pmed.0010030.txt:0
./technical/plos/pmed.0010024.txt:0
./technical/plos/journal.pbio.0020348.txt:0
./technical/plos/journal.pbio.0020406.txt:0
./technical/plos/pmed.0010025.txt:2
./technical/plos/pmed.0020086.txt:0
./technical/plos/pmed.0020045.txt:6
./technical/plos/journal.pbio.0020215.txt:3
./technical/plos/pmed.0020247.txt:0
./technical/plos/pmed.0020047.txt:0
./technical/plos/journal.pbio.0020001.txt:0
./technical/plos/pmed.0020090.txt:0
./technical/plos/journal.pbio.0020161.txt:0
./technical/plos/journal.pbio.0020439.txt:5
./technical/plos/journal.pbio.0020404.txt:0
./technical/plos/pmed.0010026.txt:0
./technical/plos/journal.pbio.0020148.txt:1
./technical/plos/pmed.0020085.txt:1
./technical/plos/pmed.0020091.txt:0
./technical/plos/journal.pbio.0020028.txt:2
./technical/plos/journal.pbio.0020216.txt:1
./technical/plos/pmed.0020278.txt:1
./technical/plos/pmed.0020268.txt:0
./technical/plos/journal.pbio.0020206.txt:0
./technical/plos/journal.pbio.0020010.txt:0
./technical/plos/journal.pbio.0020164.txt:9
./technical/plos/pmed.0010022.txt:0
./technical/plos/pmed.0010036.txt:1
./technical/plos/journal.pbio.0020400.txt:1
./technical/plos/journal.pbio.0020401.txt:0
./technical/plos/pmed.0010023.txt:0
./technical/plos/pmed.0020123.txt:0
./technical/plos/pmed.0020094.txt:0
./technical/plos/journal.pbio.0020213.txt:0
./technical/plos/pmed.0020257.txt:0
./technical/plos/journal.pbio.0020013.txt:0
./technical/plos/pmed.0020055.txt:0
./technical/plos/pmed.0020082.txt:0
./technical/plos/pmed.0010021.txt:0
./technical/plos/pmed.0010034.txt:0
./technical/plos/pmed.0010008.txt:2
./technical/plos/pmed.0020120.txt:0
./technical/plos/journal.pbio.0020172.txt:3
./technical/plos/pmed.0020040.txt:0
./technical/plos/pmed.0020068.txt:1
./technical/plos/journal.pbio.0020012.txt:0
./technical/plos/pmed.0020281.txt:0
./technical/plos/pmed.0020242.txt:0
```

Example 2: This command counts the lines containing the word "Boston" specifically within the `911report` subdirectory of `technical`. This command is particularly useful for quantifying references to "Boston" in a large set of documents, which can help in assessing the focus or relevance of "Boston" within the content, such as in analytical or research settings where frequency analysis might provide insight into data trends.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Rc "Boston" ./technical/911report
./technical/911report/chapter-13.4.txt:1
./technical/911report/chapter-13.5.txt:2
./technical/911report/chapter-13.1.txt:0
./technical/911report/chapter-13.2.txt:24
./technical/911report/chapter-13.3.txt:0
./technical/911report/chapter-3.txt:0
./technical/911report/chapter-2.txt:1
./technical/911report/chapter-1.txt:36
./technical/911report/chapter-5.txt:0
./technical/911report/chapter-6.txt:4
./technical/911report/chapter-7.txt:6
./technical/911report/chapter-9.txt:0
./technical/911report/chapter-8.txt:1
./technical/911report/preface.txt:0
./technical/911report/chapter-12.txt:0
./technical/911report/chapter-10.txt:0
./technical/911report/chapter-11.txt:0
```

---

**Line Number Display (`-n`):**

Example 1: This command searches for the term "results" in the `plos` subdirectory of `technical`, showing line numbers with the matches. This is useful for editors or researchers who need to review where results are discussed in documents.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Rn "results" ./technical/plos
./technical/plos/pmed.0020059.txt:87:          files, invokes the SaTScan software [36], and reads the results back into SAS for
./technical/plos/pmed.0020059.txt:371:          and diarrhea, the results for the last week of November are listed in Tables 2 and 3. For
./technical/plos/journal.pbio.0020354.txt:111:        in North American birds, with results that contrast strongly with those of Hebert et al. as
./technical/plos/journal.pbio.0020354.txt:163:        whether the results for North American birds can be extrapolated to the tropics, where DNA
./technical/plos/pmed.0020104.txt:26:        The overall results suggest that average BMI and cholesterol increase with national
./technical/plos/pmed.0020272.txt:7:        and editors work together to minimize the reporting of false results. However, even if one
./technical/plos/pmed.0020272.txt:43:        Research progress depends on dissemination of results, and journal articles are the most
./technical/plos/pmed.0020272.txt:48:        publication of research results needs to be open-minded, rigorous, and honest in designing
./technical/plos/pmed.0020272.txt:49:        experiments, analyzing results, reporting findings, peer-reviewing manuscripts, providing
./technical/plos/pmed.0020272.txt:52:        chances of producing true results. He also gives some corollaries that allow readers to get
./technical/plos/pmed.0020272.txt:66:        Too often editors and reviewers reward only the cleanest results and the most
./technical/plos/pmed.0020272.txt:76:        Besides selecting papers and influencing how results are reported, we use the synopses and
./technical/plos/pmed.0020258.txt:37:        Where do these results leave the design of HIV trials? To begin with, the results should
./technical/plos/journal.pbio.0020140.txt:36:        important results. The authors lesioned discrete parts of the prefrontal cortex in
./technical/plos/journal.pbio.0020140.txt:48:        auditory differentiation task. These results strongly suggested a differential role for the
./technical/plos/journal.pbio.0020140.txt:68:        These interesting but nonconclusive results in humans spurred us on to use neuroimaging
./technical/plos/journal.pbio.0020140.txt:119:        This result confirmed and extended the results from Iversen and Mishkin's original
./technical/plos/journal.pbio.0020140.txt:124:        results are not conclusive and raise many new issues. It is, for instance, not presently
./technical/plos/pmed.0010013.txt:104:        experience and proven results very heavily, which may stifle innovation and likely serves
./technical/plos/pmed.0020113.txt:46:        its results widely publicized. According to Steve Morgan, “Anecdotal evidence suggests that
./technical/plos/journal.pbio.0020169.txt:71:        subunits results in inside-out activation. They showed that replacement of the
./technical/plos/pmed.0020098.txt:49:        thrombolytic mechanisms, but significant blockage usually results as the clot is scarred
./technical/plos/journal.pbio.0020035.txt:51:        the latter is lost and a chain of four carbon atoms results (Figure 1A). Further rounds of
./technical/plos/journal.pbio.0020035.txt:60:        removed by a series of three steps (Figure 1B), any of which may be omitted. This results
./technical/plos/pmed.0020073.txt:241:          Collectively, these results demonstrate that tumors from all three patients contain 
./technical/plos/pmed.0020073.txt:286:          Patient 3 showed results analogous to those of patient 2. A tumor-rich pre-treatment
./technical/plos/pmed.0020073.txt:303:          155 tumors (data not shown; see Discussion). Collectively, our results suggest that the
./technical/plos/pmed.0020073.txt:315:          results imply that alternative mechanisms of acquired drug resistance exist.
./technical/plos/pmed.0020073.txt:426:          ratios (Figure 4A and 4B). Similar results were obtained using erlotinib against
./technical/plos/pmed.0020073.txt:428:          containing the T790M mutation (Figure 4C). These results suggest that the T790M mutation
./technical/plos/pmed.0020073.txt:450:          KRAS (Figure 5). Very similar results were obtained with erlotinib
./technical/plos/pmed.0020073.txt:471:        kinase inhibitors [1,2,3]. Our results further demonstrate that an analogous mechanism of
./technical/plos/pmed.0020073.txt:523:        T790M mutation were smaller than originally anticipated. These results differ from those of
./technical/plos/pmed.0020249.txt:95:          of the susceptibility to infection. This assumption will be relaxed below.) The results
./technical/plos/pmed.0020249.txt:129:          The results of these Bernoulli trials can again be written as a vector 
./technical/plos/pmed.0020249.txt:166:          before. The results of these repeated Bernoulli trials can be written as two vectors, 
./technical/plos/pmed.0020249.txt:210:          the results of these repeated Bernoulli trials can be written as two vectors, 
./technical/plos/pmed.0020249.txt:375:          of virtual experiments that yielded significant results (significance level α =
./technical/plos/journal.pbio.0020019.txt:71:        by an environmental change, but can be produced by a gene ‘knockout’. These results may go
./technical/plos/journal.pbio.0020019.txt:74:        whether it is possible to verify these results experimentally. Bergman and Siegal (2003)
./technical/plos/journal.pbio.0020019.txt:84:        Given the results of Bergman and Siegal (2003), it should be possible to find gene
./technical/plos/journal.pbio.0020145.txt:220:        results. Free access to research literature enhances student learning and helps produce the
./technical/plos/pmed.0020103.txt:41:          lines were from distinct donors and karyotypically normal. They gave comparable results,
./technical/plos/pmed.0020103.txt:106:          morphometric techniques [15]. To obtain representative results, all quantification of
./technical/plos/pmed.0020103.txt:299:          expression at stage 4. Comparable results were obtained with three independently derived
./technical/plos/pmed.0020103.txt:405:        neural stem cells [42]. These results were also unexpected because endothelial cells and
./technical/plos/journal.pbio.0020353.txt:11:        have begun to take an interest in the question of who can and can't read the results of the
./technical/plos/journal.pbio.0020353.txt:26:        results of publicly funded research would not be mandates for scientists to submit work
./technical/plos/journal.pbio.0020353.txt:37:        articles. Making funding for research contingent on the results of the work being
./technical/plos/journal.pbio.0020353.txt:56:        medical nonsense from the Web for free, but citizens must pay to see the results of
./technical/plos/journal.pbio.0020353.txt:71:        public access to research results seems methodical, inclusive, and likely to prove
./technical/plos/journal.pbio.0020347.txt:158:        Tanksley and McCouch 1997). This phenomenon is known as transgressive variation and results
./technical/plos/journal.pbio.0020420.txt:164:        often results in hybridization (reviews in Rhymer and Simberloff 1996; Mooney and Cleland
./technical/plos/pmed.0020116.txt:34:        the relationship between dengue incidence and El Niño in Thailand. Their results, based on
./technical/plos/journal.pbio.0020150.txt:113:        press after he announced his results, and his experiment led directly to speculation that
./technical/plos/journal.pbio.0020150.txt:161:        that it works, you can create tests that will produce results—I can see how it could be
./technical/plos/journal.pbio.0020232.txt:24:        reproducing Spallanzani's intriguing results (Newth 1958).
./technical/plos/journal.pbio.0020232.txt:91:        deficiency. Nevertheless, results from several recent studies have converged on a set of
./technical/plos/journal.pbio.0020232.txt:148:        well as myotubes. These results suggest that the combination of ectopic 
./technical/plos/journal.pbio.0020232.txt:170:        results suggest that 
./technical/plos/journal.pbio.0030021.txt:120:        role (Saccone et al. 1998). Similar results have also been found for the housefly, 
./technical/plos/journal.pbio.0020224.txt:17:        inconsistencies in the grafting results that pointed to subtleties important for both
./technical/plos/journal.pbio.0020224.txt:75:        scions. We soon realized that our results were influenced by the developmental stage of our
./technical/plos/pmed.0020074.txt:37:        resistance mutation. Similarly, the results by Pao and colleagues should help researchers
./technical/plos/journal.pbio.0020146.txt:60:        2000). Similar results have been obtained with other types of odors.
./technical/plos/journal.pbio.0020146.txt:64:        These results indicate that humans are not poor smellers (a condition technically called
./technical/plos/pmed.0020114.txt:38:        Do the results mean co-artemether should be introduced as a first-line treatment for
./technical/plos/pmed.0010028.txt:38:        cells from healthy donors with heteroclitic peptides results in expansion of cells with a
./technical/plos/journal.pbio.0020350.txt:86:        together with some results from optimal-foraging theory, outlined here, could unlock the
./technical/plos/journal.pbio.0020350.txt:98:        same in both patches. (For a general analysis, with the same qualitative results, see
./technical/plos/journal.pbio.0020350.txt:173:        birds being more efficient than bees at exploiting red flowers, and the results would be
./technical/plos/pmed.0020115.txt:18:        some remarkable results with around 84% of patients remaining insulin-free after one year
./technical/plos/pmed.0020115.txt:39:        Of course, results in mice do not mean that such treatments would automatically work in
./technical/plos/pmed.0020061.txt:38:        toxicity to the fetal nervous system that results from the mother's exposure to toxins
./technical/plos/journal.pbio.0030051.txt:65:        disagreements, the convergence of results in areas of attention and language seem to me
./technical/plos/journal.pbio.0020054.txt:203:        Brady doesn't expect immediate results in terms of reducing acreage burned. “Canada and
./technical/plos/pmed.0010066.txt:254:        the likelihood of nodal metastases in vivo. These results are highly relevant in cancer
./technical/plos/pmed.0010066.txt:283:        detection of liver metastases [28]. Third, our results are significant because the
./technical/plos/journal.pbio.0030131.txt:37:        Of course, a study with results this unexpected also raises a number of intriguing
./technical/plos/journal.pbio.0020337.txt:71:        stimuli of the same frequency. Gold and Pumphrey showed that their results could only be
./technical/plos/journal.pbio.0020337.txt:87:        second experiment gave comparable results. However, their resonance interpretation has been
./technical/plos/journal.pbio.0020337.txt:91:        results remain persuasive.
./technical/plos/pmed.0020198.txt:52:        As with related studies, these results suggest that smoking cessation should be a more
./technical/plos/pmed.0010067.txt:28:        validated it in a group of 34 patients. The results are encouraging: the analysis showed a
./technical/plos/pmed.0020007.txt:120:        function—but the results are very specific to the skills that are trained, and it is as yet
./technical/plos/journal.pbio.0030050.txt:198:        but our results open up new and exciting vistas”, particularly since many of the
./technical/plos/pmed.0020239.txt:45:        from an influenza outbreak. Their results suggested that within a strict management
./technical/plos/journal.pbio.0020241.txt:15:        results in autoimmune reactions that often lead to clinical disease. In spite of massive
./technical/plos/journal.pbio.0020241.txt:96:        More problematic is the interpretation of results obtained with knockout models. A gene
./technical/plos/pmed.0020039.txt:174:        The results of Salomon and colleagues' model need to be
./technical/plos/pmed.0010058.txt:180:        the results can be appropriately attributed to the agent itself.
./technical/plos/pmed.0010058.txt:189:        unfortunately these results are not universal. Researchers must continue to look for ways
./technical/plos/pmed.0010070.txt:13:        Luis Montaner and colleagues now report results from a randomized trial of 42
./technical/plos/pmed.0010064.txt:145:          0.05 was used to define statistical significance. Unless otherwise stated, results are
./technical/plos/pmed.0020158.txt:7:        researchers who believed that the results of the global research enterprise should be a
./technical/plos/journal.pbio.0020042.txt:88:        short report describing the approaches that have been tried, with the results of its
./technical/plos/journal.pbio.0020042.txt:115:        results would significantly increase our functional knowledge of the genes within the
./technical/plos/pmed.0020212.txt:10:        qualify the ultimate clinical and scientific validity of the results. However, the recent
./technical/plos/pmed.0020212.txt:51:        influences. These results are only broadly informative, as they provide no information
./technical/plos/journal.pbio.0030094.txt:48:        Saccharomyces cerevisiae , since mutation results in the
./technical/plos/journal.pbio.0030094.txt:134:        Several results suggest that transcription and cohesin binding are incompatible. In 
./technical/plos/journal.pbio.0030094.txt:146:        results in chromosome missegregation and cell death [13]. Cohesin is found at the
./technical/plos/journal.pbio.0020046.txt:106:        many other studies on sensory–motor reaction times yielded inconsistent results (Andrews et
./technical/plos/pmed.0020160.txt:235:        Analyses using pack-years were also done (not shown); the results were unchanged using
./technical/plos/pmed.0020160.txt:237:        cardiovascular disease (not shown); results were again unchanged and measures of
./technical/plos/pmed.0020160.txt:285:        exposure as measured by pack-years. Our results, while based on more complete modeling,
./technical/plos/pmed.0020160.txt:327:        comprehensive manner. Our results suggest that policy-makers faced with escalating
./technical/plos/pmed.0010060.txt:7:        of clinical trial results [1,2]. The debate has intensified since New York State Attorney
./technical/plos/pmed.0010060.txt:12:        trials results have been to register all clinical trials and to make their results publicly
./technical/plos/pmed.0010060.txt:31:        In this essay, I argue that a highly valuable but underused registry and results
./technical/plos/pmed.0010060.txt:97:        I therefore suggest that we increase access to the clinical trials registry and results
./technical/plos/pmed.0010060.txt:121:        results database are restricted to those trials aimed at supporting US marketing approval
./technical/plos/pmed.0010060.txt:145:        await the creation of a clinical trials registry and results database that is truly
./technical/plos/pmed.0010061.txt:52:        the results less applicable to a general population.
./technical/plos/pmed.0010049.txt:21:        metabolic abnormalities have so far been inconclusive. These results prompted some of the
./technical/plos/pmed.0010049.txt:22:        scientists in the field who had jumped on the resistin bandwagon after the initial results
./technical/plos/journal.pbio.0020127.txt:33:        times and attempt to integrate recent results from different species into a common
./technical/plos/journal.pbio.0020133.txt:38:        that are recognized today. In one type, silencing results from a block in mRNA synthesis
./technical/plos/journal.pbio.0020133.txt:39:        (transcriptional gene silencing [TGS]); in the second type, silencing results from mRNA
./technical/plos/journal.pbio.0030056.txt:35:        (PCR); replication of results from a second, independent extract; and, for really new or
./technical/plos/journal.pbio.0030056.txt:36:        unexpected results, replication of results by an independent research group.
./technical/plos/journal.pbio.0030056.txt:116:        this tiny hominid have not produced results. “We have made attempts with Stegodon molars,”
./technical/plos/journal.pbio.0030056.txt:145:        do not adhere to all the criteria, and also enable the publication of erroneous results
./technical/plos/pmed.0020017.txt:37:        erlotinib. Our results suggest that a determination of mutational status for both 
./technical/plos/pmed.0020017.txt:163:        These results have important clinical implications. First, they extend previous data
./technical/plos/journal.pbio.0020440.txt:227:        correcting the results will be a very long process. If they're not right, they'll have done
./technical/plos/pmed.0010062.txt:244:        circumstances. Our results validate the association of decreased leptin with decreased
./technical/plos/pmed.0010062.txt:312:        sleep restriction also corroborates our results [18,19]. The robustness of our findings and
./technical/plos/pmed.0010062.txt:314:        statistically significant results are unlikely to be a reflection of the number of analyses
./technical/plos/pmed.0010062.txt:351:        Our results demonstrate an important relationship between sleep and metabolic hormones.
./technical/plos/pmed.0020162.txt:48:        measures may influence their results.
./technical/plos/pmed.0020162.txt:63:        interpretation of results for monozygotic twins, including patterns of within-pair
./technical/plos/pmed.0020162.txt:64:        variability, aided by comparison to results to same-sex dizygotic twins.
./technical/plos/pmed.0020162.txt:230:        dizygotic than the monozygotic twin pairs (Tables 3 and 4). Similar results were obtained
./technical/plos/pmed.0020162.txt:241:        socioeconomic position, with results sensitive to choice of socioeconomic measure. Although
./technical/plos/pmed.0020162.txt:246:        not evident for analyses using data on educational attainment. Together, these results,
./technical/plos/pmed.0020162.txt:258:        results, has not to our knowledge previously been reported. Given that low educational
./technical/plos/pmed.0020162.txt:260:        [16â€“18], our results lend tentative support to the hypothesis that
./technical/plos/pmed.0020162.txt:278:        generalizability (but not internal validity) of results. Most studies assessing the impact
./technical/plos/pmed.0020162.txt:296:        Overall, results of this study are in accord with other research suggesting that
./technical/plos/pmed.0020162.txt:305:        important concerns raised about likely unmeasured confounders affecting results of prior
./technical/plos/pmed.0020162.txt:308:        results to nontwins could be hampered if twins differ systematically from nontwins on
./technical/plos/pmed.0020016.txt:49:        and potential risks of large-scale treatment roll-out. The results of this analysis will be
./technical/plos/pmed.0020016.txt:89:          results; second, multiple simulations were undertaken by sampling values from each of the
./technical/plos/pmed.0020016.txt:191:        results, lowering the number of new infections in 2020 by only 2% compared to the scenario
./technical/plos/pmed.0020016.txt:199:        produce results that scale as expected, with reductions in annual incidence of 34% to 64%
./technical/plos/pmed.0020016.txt:317:          resources. The results from our analyses show how potential synergies between prevention
./technical/plos/pmed.0020002.txt:100:        duration and often results in less than complete resolution of disease; relapse is common
./technical/plos/pmed.0020200.txt:14:        The major difficulty in getting clear results on this question is that it is virtually
./technical/plos/pmed.0020200.txt:28:        In total, 268 people died. When the results were analyzed, the surprising finding was
./technical/plos/pmed.0020200.txt:35:        there is no doubt that these results seem counterintuitive. Some readers may take away the
./technical/plos/pmed.0020200.txt:38:        results is that by the time adults are overweight, the health benefits of losing weight are
./technical/plos/pmed.0020200.txt:47:        composed of oppositely operating effects with net results reflecting the balance between
./technical/plos/pmed.0020231.txt:9:        yeast [2]—and although they are not yet definitive, results from ongoing longevity studies
./technical/plos/pmed.0020231.txt:50:        could affect the results.
./technical/plos/pmed.0020231.txt:55:        longevity in rodents. The results from these studies have been contradictory, with some
./technical/plos/pmed.0020231.txt:95:        and the results by Mair et al. [8] should not be extrapolated to mammals in general. But if
./technical/plos/pmed.0020033.txt:49:        peripheral blood of patients with MS [12,13,14]. While these results supported looking at
./technical/plos/pmed.0020033.txt:90:        results were not tested on an independent dataset, as is frequently requested [22], the
./technical/plos/pmed.0010047.txt:38:        “It is absolutely crucial that results like these are published, since the failures, as
./technical/plos/pmed.0010047.txt:44:        second-guess the results of field trials. This is partly because we do not have any good
./technical/plos/journal.pbio.0020302.txt:64:        lava, even carbon dioxide or sulfur dioxide. Recently, results from the Mars Exploration
./technical/plos/journal.pbio.0020302.txt:79:        Gas Chromatograph Mass Spectrometer for characterizing organic molecules. The results were
./technical/plos/journal.pbio.0020302.txt:86:        If considered alone, the Labeled Release results would be a plausible indication for
./technical/plos/journal.pbio.0020302.txt:90:        argument against a biological interpretation of the Viking results (Klein 1999; but cf.
./technical/plos/journal.pbio.0020302.txt:96:        negative results of the Viking biology experiments, the surface of Mars also appears to be
./technical/plos/pmed.0010046.txt:41:        practices and provides a place where the results from all registered trials can be
./technical/plos/pmed.0010046.txt:54:        of better tools to help clinicians apply trial results to their practice. For trial data to
./technical/plos/journal.pbio.0020100.txt:52:        global function that matches the results obtained in cell culture experiments. In summary,
./technical/plos/pmed.0020146.txt:11:        BMC Medicine 2: e13). They now report results from a second systematic
./technical/plos/journal.pbio.0030065.txt:117:        [19]), which suggests that such methods produce useful results.
./technical/plos/journal.pbio.0030065.txt:127:        contained relevant experimental results about 
./technical/plos/journal.pbio.0020276.txt:100:        protein-cleaving cascade that results in the production of toxic intermediates and melanin
./technical/plos/pmed.0020018.txt:59:        α shedding. These results raise the possibility that the apparent
./technical/plos/pmed.0020018.txt:213:          results are taken together with independent work on regulated shedding of transforming
./technical/plos/pmed.0020018.txt:291:          α without altering levels of holoAPP. Based on this series of results,
./technical/plos/pmed.0020018.txt:299:          ROCK1, as well as the results employing either FTI-1 or arachidonate, we concluded that
./technical/plos/pmed.0020018.txt:306:          results of Y-27632 and DN ROCK1.
./technical/plos/pmed.0020018.txt:374:        of APP may be the eventual generation of AICD. Our results suggest that Rho/ROCK signaling
./technical/plos/pmed.0020018.txt:421:        these results suggest the existence of a reciprocal relationship between
./technical/plos/pmed.0020018.txt:438:        apparently occurs on the plasma membrane. These results suggest that a tightly
./technical/plos/pmed.0020018.txt:456:        Preliminary results from a pilot proof-of-concept using atorvastatin in a human clinical
./technical/plos/pmed.0020018.txt:468:        The results reported here point to several areas for additional investigation. As
./technical/plos/pmed.0020144.txt:49:        precision with which the final epidemic size can be predicted. Kendall's results can be
./technical/plos/journal.pbio.0020116.txt:118:        reproduced in additional laboratories for any reliable interpretation of the results
./technical/plos/journal.pbio.0020116.txt:120:        Thus, in the reported results, the possible significance of the reported isolation and
./technical/plos/journal.pbio.0020116.txt:124:        preliminary and incomplete. If results with any isolated and characterized adult stem cells
./technical/plos/pmed.0020187.txt:36:        September 2004, when the results of the placebo-controlled APPROVe study were made public
./technical/plos/pmed.0010045.txt:227:          results show that NF-κB activation is necessary and sufficient for resistin induction by
./technical/plos/pmed.0020145.txt:21:        “We are keenly awaiting the results from several ongoing trials. In the meantime, our
./technical/plos/pmed.0020237.txt:43:        they suggest that these results indicate that although drug development of antivirals is an
./technical/plos/journal.pbio.0020067.txt:79:        unit. This report contained Franklin's results that the phosphates were on the outside and
./technical/plos/pmed.0020009.txt:66:        results, whether positive, negative, or neutral. Anyone subjectively evaluating patient
./technical/plos/pmed.0020009.txt:127:        Public accountability and scientific integrity require that all research results emanating
./technical/plos/pmed.0020009.txt:165:        data analysis, and publication of results. The IRB system should be strengthened in its
./technical/plos/journal.pbio.0020073.txt:89:        2 undergoes a substantial conformational change, which results in a
./technical/plos/journal.pbio.0020073.txt:90:        single “extended” helix. This conformational change results in a linear mechanical motion,
./technical/plos/pmed.0020021.txt:30:        These results need to be validated in larger and prospective trials that use
./technical/plos/pmed.0020155.txt:11:        misunderstanding of our novel quantitative analyses and our important results. Hence, they
./technical/plos/pmed.0020155.txt:12:        misunderstood the significance of the health-policy implications of our results. Thus, we
./technical/plos/pmed.0020155.txt:27:        Secondly, Capron and Reis [2] misunderstood our important results. They stated that
./technical/plos/pmed.0020155.txt:32:        agree that if these had been our results, they would have been trivial and obvious.
./technical/plos/pmed.0020155.txt:33:        However, Capron and Reis [2] did not discuss our actual results: we determined how to
./technical/plos/pmed.0020155.txt:41:        a catchment area of 40–60 km. Thus, our results demonstrate (to our knowledge for the first
./technical/plos/pmed.0020155.txt:49:        necessary size of the catchment area, and our results have identified that there is an
./technical/plos/pmed.0020155.txt:56:        equity. Taken together, our quantitative results are novel and controversial, providing
./technical/plos/pmed.0010069.txt:40:        even here, the sample size becomes an issue, with the most convincing results seen in the
./technical/plos/pmed.0010041.txt:32:        the drugs. These trials gave disappointing results, up to and including the emergence of
./technical/plos/pmed.0010041.txt:84:        efficacy results in treated chronic infection. As such, practice guidelines should continue
./technical/plos/pmed.0020182.txt:207:          adults and six infants. Three adults did not have flow cytometry results available,
./technical/plos/pmed.0020182.txt:216:          results directly to parallel samples processed by flow cytometry using
./technical/plos/pmed.0020182.txt:255:        results show a linear correlation between the number of cells in the sample and the
./technical/plos/pmed.0020182.txt:312:        FACSCalibur. The time from blood collection to complete analysis and results reporting
./technical/plos/pmed.0020182.txt:314:        did not have valid flow cytometry results available, leaving 61 adults and six infants for
./technical/plos/pmed.0020182.txt:328:        We compared results from our microchip assay with results available from flow cytometry,
./technical/plos/pmed.0020182.txt:333:        cells/Î¼l) by flow cytometry, results show a good correlation between absolute
./technical/plos/pmed.0020182.txt:338:        Several of the results from participants at the higher end of absolute CD4 counts fall
./technical/plos/pmed.0020182.txt:362:        both adult and pediatric CD4 results can be obtained.
./technical/plos/pmed.0020182.txt:375:        Our results provide proof of principle that low-cost microfluidic structures combined
./technical/plos/pmed.0020182.txt:382:        ideal for resource-scarce settings. As our results show, this method may be less accurate
./technical/plos/pmed.0020182.txt:399:        The results presented here were obtained with a stationary, tabletop monitoring system
./technical/plos/pmed.0020182.txt:429:        microchip CD4 assay is extremely rapid. CD4 results in the prototype system described here
./technical/plos/pmed.0020182.txt:431:        microfluidic device with push-button operation, results should be available in less than 10
./technical/plos/pmed.0020196.txt:34:        under development. Thomas Geisbert and colleagues now report promising results with a
./technical/plos/pmed.0020196.txt:40:        These are encouraging results, but future larger studies will need to assess the
./technical/plos/journal.pbio.0030102.txt:94:        the surface sediments oxidize methane with sulfate, which results in very high sulfide
./technical/plos/pmed.0010068.txt:7:        This could explain results of previous studies that have shown a link between short sleep
./technical/plos/pmed.0020034.txt:69:        allergen and the results strongly suggested that exposure in the child's own house was the
./technical/plos/pmed.0020236.txt:57:        conditions of varied transmission intensity. Nevertheless, based on the results of this
./technical/plos/pmed.0020208.txt:49:        results freely and publicly available, and with our belief that transparency in the conduct
./technical/plos/journal.pbio.0020064.txt:45:        The olfaction results also enticed researchers from other disciplines into the taste
./technical/plos/pmed.0020022.txt:32:        Taken together, these results suggest that statins influence APP processing, at least in
./technical/plos/pmed.0010056.txt:170:        previously unpublished results. One low cost/high value option would be for companies that
./technical/plos/pmed.0020181.txt:9:        These results are closely consistent with observational data linking weight gain to
./technical/plos/pmed.0020181.txt:68:        in the intent-to-lose group to that intention. These findings render the results
./technical/plos/pmed.0020181.txt:88:        that range. The results from Kaprio et al, although they raise questions about the effects
./technical/plos/journal.pbio.0020307.txt:64:        (Mangeat et al. 2003). APOBEC3G-induced deamination at this stage results in monotonous
./technical/plos/journal.pbio.0020307.txt:69:        eradication, the most likely scenario is that G3A hypermutation results in the generation
./technical/plos/journal.pbio.0020307.txt:92:        results in their destruction; the rate of mutation becomes so high that no genome can
./technical/plos/journal.pbio.0020307.txt:100:        2003). The results produced to date are highly encouraging, particularly when these
./technical/plos/journal.pbio.0020267.txt:146:        More general studies of adult autistic neuroanatomy have given conflicting results—most
./technical/plos/journal.pbio.0020267.txt:196:        The team's results show that autistic children can learn these skills from intense
./technical/plos/pmed.0020209.txt:78:            culture of secrecy at drug companies too often results in claims that are closer to
./technical/plos/pmed.0020246.txt:329:        also results in differential treatment practices that may contribute to stigmatization of
./technical/plos/journal.pbio.0020214.txt:89:        results of such research normally cannot be published. This is a serious problem,
./technical/plos/journal.pbio.0020214.txt:153:        these days, very decent results are often published in Russianlanguage journals, the best
./technical/plos/pmed.0020050.txt:259:        and/or the number of HCFs is increased (Figure 4). Our results show that the number of HCFs
./technical/plos/pmed.0020050.txt:261:        used, then even a (small) catchment radius of 20 km results in the ideal median proportion
./technical/plos/pmed.0020050.txt:297:        17 HCFs. However, our results clearly show that in order to achieve an optimal equitable
./technical/plos/pmed.0020118.txt:24:        they regularly consider leaving medicine altogether. Contrast these results with those of a
./technical/plos/journal.pbio.0020348.txt:45:        pathway, which results in lactate accumulation and in turn limits anaerobic exercise. Thus,
./technical/plos/journal.pbio.0020348.txt:75:        In this regard, the results of Fink et al. (1977) are important. These researchers
./technical/plos/journal.pbio.0020348.txt:192:        al. 2003) and obesity (Wang et al. 2004). The results of these studies have clinical
./technical/plos/pmed.0020045.txt:250:          PTECs. Together with our in vivo observations, these results suggest that hyperglycemia
./technical/plos/pmed.0020045.txt:269:          effect (Figure 4A). These results were confirmed by DNA laddering assay (data not
./technical/plos/pmed.0020045.txt:364:        upstream mechanism of FFA and CD36 interaction, our results demonstrate very rapid
./technical/plos/pmed.0020047.txt:39:        publication of results—or to intimidate the researchers. Thus, sponsors whose interests
./technical/plos/pmed.0020047.txt:40:        could be hurt by publication of certain possible results must never be in a position to cut
./technical/plos/journal.pbio.0020439.txt:190:        increases the importance of theoretical understanding of the results of computation.
./technical/plos/journal.pbio.0020439.txt:192:        and to bridge the enormous gap between computational results and insight or
./technical/plos/journal.pbio.0020404.txt:107:        results were highly significant. “As far as I know this is the first clinical study to use
./technical/plos/pmed.0010026.txt:68:        These results emphasize how difficult it is to translate findings, such as the spectacular
./technical/plos/pmed.0010026.txt:69:        results obtained by the vaccination of TCR transgenic mice with heteroclitic peptides [12],
./technical/plos/pmed.0020091.txt:40:        What do these results mean for clinical applications? As well as identifying tumors that
./technical/plos/journal.pbio.0020028.txt:51:        to cleave specific target RNA molecules (see Figure 1). “The initial results with hepatitis
./technical/plos/journal.pbio.0020028.txt:61:        results seemed to support the theory: antisense drugs effectively reduced tumor sizes in
./technical/plos/journal.pbio.0020028.txt:63:        results were largely due to an increase in production of interferons by the immune system
./technical/plos/journal.pbio.0020028.txt:84:        promising results in the treatment of malignant melanoma.
./technical/plos/journal.pbio.0020216.txt:123:        from 10% to 20% results in twice the difference in dance rate that an increase from 50% to
./technical/plos/journal.pbio.0020206.txt:67:        outcomes of ‘unequal crossing over’, which results from homologous recombination between
./technical/plos/journal.pbio.0020206.txt:171:        If duplication results in the formation of a novel function as a result of interaction
./technical/plos/journal.pbio.0020164.txt:161:        cell behaviors), test specifically for bistability, correlate results with the patterns
./technical/plos/pmed.0010022.txt:51:        Interpretation of results is an essential part of a medical journal's job. Although we
./technical/plos/pmed.0010036.txt:21:        above 5,000 copies for three determinations separated by a week each. The early results of
./technical/plos/pmed.0010036.txt:26:        size of the cohort to 14 patients. Our results indicate that, although the majority of
./technical/plos/pmed.0010036.txt:241:          factor was considered. These results indicate that periods of relative control of viremia
./technical/plos/pmed.0010036.txt:381:        during the second STI but then failed to control during the third STI), the results are not
./technical/plos/pmed.0010036.txt:440:        disappointing results thus far [9], but the availability of new and more potent immunogens
./technical/plos/pmed.0010036.txt:443:        will enhance CD8+ T cell function requires additional studies. Some promising results have
./technical/plos/journal.pbio.0020401.txt:155:        function. Given that there are some differences in these results, further clarification of
./technical/plos/pmed.0010023.txt:28:        relate it to clinical symptoms and intestinal biopsy results. All patients were on a
./technical/plos/pmed.0020123.txt:274:        comparability of the current results to previous reports.
./technical/plos/pmed.0020257.txt:25:        facilities. Many of the survey's results are worrying. Nine percent of professionals
./technical/plos/pmed.0020055.txt:6:        “Publishing results in traditional paper based way in a journal hides too much
./technical/plos/pmed.0020055.txt:22:        deciding how to assess the data presented. The results from several high-profile papers
./technical/plos/pmed.0020055.txt:44:        concluded, “rapid identification and neutralization of spurious results is essential to
./technical/plos/pmed.0020055.txt:56:        Ruschhaupt and others have shown, disclosure of results and data is not enough, since there
./technical/plos/pmed.0020055.txt:60:        entire analysis quickly and, hence, assess the robustness of the results. Some authors have
./technical/plos/pmed.0010021.txt:40:        entrapped in liposomes [4]. Although some mildly encouraging results were achieved, it was
./technical/plos/pmed.0010021.txt:79:          results.
./technical/plos/pmed.0010021.txt:85:          the size of the liver. The results were clear (Figure 2) [9]. Even a dose of only 15
./technical/plos/pmed.0010021.txt:95:          regimen provides results superior to those achieved with smaller doses. The only support
./technical/plos/pmed.0010008.txt:221:          control participants or those with emphysema (data not shown). Similar results were
./technical/plos/pmed.0020040.txt:92:          Recent laboratory tests produced the following results: a HbA1c of 8.1%, a fasting
./technical/plos/pmed.0020040.txt:98:            is preferred because it has lower rates of false-positive and false-negative results
./technical/plos/pmed.0020040.txt:101:            results. The elevated ratio of microalbumin in the urine signifies early nephropathy
./technical/plos/pmed.0020040.txt:190:        Intensive therapy in patients with type 2 diabetes results in a decreased risk of
./technical/plos/journal.pbio.0020012.txt:55:        promising results in 
./technical/plos/journal.pbio.0020012.txt:57:        Sinclair. “So we're very encouraged by that.” Publication of these results is imminent. The
./technical/plos/journal.pbio.0020012.txt:62:        results by mid-2004 and those for Alzheimer's by the end of the year. Harvard and BIOMOL
./technical/plos/journal.pbio.0020012.txt:140:        longer. Before the results appeared, there was a “very negative attitude” towards ageing
./technical/plos/journal.pbio.0020012.txt:147:        the results, published in July, derive directly from her early work on 
./technical/plos/journal.pbio.0020012.txt:169:        of ageing.” Complementary results in flies and mammals persuade her to be more explicit.
./technical/plos/pmed.0020281.txt:19:        misrepresented pharmaceuticals; clinical research trial results that have been sequestered
```

Example 2: This command displays each line that contains the term "Boston", along with the line number and file path where each occurrence is found. This is particularly useful for quickly locating references to "Boston" across multiple documents in a structured report or a collection of files, which can aid in research or analysis, especially in contexts like reviewing detailed reports or data logs.

```
kavi@Kavis-MacBook-Pro-325 docsearch % grep -Rn "Boston" ./technical/911report
./technical/911report/chapter-13.4.txt:957:            4. Judith Miller, "Holy Warriors: Dissecting aTerror Plot from Boston to Amman," New
./technical/911report/chapter-13.5.txt:448:                14139; Boston electronic communication). The communications were recovered from
./technical/911report/chapter-13.5.txt:2484:                country-from St. Louis to Los Angeles to Orlando to Washington Dulles, and to Boston
./technical/911report/chapter-13.2.txt:62:                of why Atta and Omari drove to Portland, Maine, from Boston on the morning of
./technical/911report/chapter-13.2.txt:65:                check in again in Boston. Michael Touhey interview (May 27, 2004). Whatever their
./technical/911report/chapter-13.2.txt:66:                reason, the Portland Jetport was the nearest airport to Boston with a 9/11 flight
./technical/911report/chapter-13.2.txt:71:                Airport and Washington Dulles International Airport), Boston's Logan International
./technical/911report/chapter-13.2.txt:87:                Sense of Alarm; Airlines Foiled Police Logan Probe," Boston Globe, Oct. 17, 2001, p.
./technical/911report/chapter-13.2.txt:257:            32. See FAA recording, Boston Air Route Traffic Control Center, position 46R, at 8:25
./technical/911report/chapter-13.2.txt:263:                Michael Woodward, supervisor at the Boston office, hearing that a problem had been
./technical/911report/chapter-13.2.txt:266:                departed Boston and the gate area was quiet. He further realized that Flight 12 had
./technical/911report/chapter-13.2.txt:420:            65. FAA audio file, Boston Center, position 46R, 8:24:38 and 8:24:56; Peter Zalewski
./technical/911report/chapter-13.2.txt:436:                Herndon Command Center, position 15, 9:19. At 9:07, Boston Air Traffic Control
./technical/911report/chapter-13.2.txt:438:                pilots of all commercial aircraft to secure their cockpits. While Boston Center sent
./technical/911report/chapter-13.2.txt:444:                United 175, it was a transcontinental flight departing Boston's Logan Airport.
./technical/911report/chapter-13.2.txt:590:            95. FAA Boston Center site visit (Sept. 22-24, 2003).
./technical/911report/chapter-13.2.txt:631:                hearing the threatening communication from the cockpit, he doubts Boston Center
./technical/911report/chapter-13.2.txt:660:                11,2001,"Apr. 19, 2002, p. 2; FAA record, Boston Center daily record of facility
./technical/911report/chapter-13.2.txt:691:                According to Joseph Cooper from Boston Center, "I coordinated with Huntress
./technical/911report/chapter-13.2.txt:703:            120. FAA audio file, Boston Center, position 31R; NEADS audio file, Mission Crew
./technical/911report/chapter-13.2.txt:716:                were told by Boston Center that the second tower had been struck. At 9:12:54, the
./technical/911report/chapter-13.2.txt:717:                Otis fighters told their Boston Center controller that they needed to establish a
./technical/911report/chapter-13.2.txt:719:                FAA audio files, Boston Center, position 31R. This series of communications explains
./technical/911report/chapter-13.2.txt:739:                from [Boston Center] indicating a possible hijack, most of the controller's
./technical/911report/chapter-13.2.txt:774:            132. Ibid., 9:03; FAA audio file, Herndon Command Center, Cleveland/Boston position,
./technical/911report/chapter-13.2.txt:777:            133. FAA Audio File, Herndon Command Center, Boston Center position, line 5115,
./technical/911report/chapter-13.2.txt:962:                possibly from aircraft crash. Also, hijacking of American Flight 11 from Boston to
./technical/911report/chapter-2.txt:465:            Other cities with branches of al Khifa included Atlanta, Boston, Chicago, Pittsburgh,
./technical/911report/chapter-1.txt:14:    Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.
./technical/911report/chapter-1.txt:16:    When he checked in for his flight to Boston, Atta was selected by a computerized prescreening system known as CAPPS (Computer Assisted Passenger Prescreening System), created to identify passengers who should be subject to special security measures. Under security rules in place at the time, the only consequence of Atta's selection by CAPPS was that his checked bags were held off the plane until it was confirmed that he had boarded the aircraft. This did not hinder Atta's plans.
./technical/911report/chapter-1.txt:18:    Atta and Omari arrived in Boston at 6:45. Seven minutes later, Atta apparently took a call from Marwan al Shehhi, a longtime colleague who was at another terminal at Logan Airport. They spoke for three minutes.
./technical/911report/chapter-1.txt:34:    While Atta had been selected by CAPPS in Portland, three members of his hijacking team-Suqami, Wail al Shehri, and Waleed al Shehri-were selected in Boston. Their selection affected only the handling of their checked bags, not their screening at the checkpoint. All five men cleared the checkpoint and made their way to the gate for American 11. Atta, Omari, and Suqami took their seats in business class (seats 8D, 8G, and 10B, respectively). The Shehri brothers had adjacent seats in row 2 (Wail in 2A, Waleed in 2B), in the firstclass cabin. They boarded American 11 between 7:31 and 7:40. The aircraft pushed back from the gate at 7:40.
./technical/911report/chapter-1.txt:38:    Washington Dulles: American 77. Hundreds of miles southwest of Boston, at Dulles International Airport in the Virginia suburbs of Washington, D.C., five more men were preparing to take their early morning flight. At 7:15, a pair of them, Khalid al Mihdhar and Majed Moqed, checked in at the American Airlines ticket counter for Flight 77, bound for Los Angeles. Within the next 20 minutes, they would be followed by Hani Hanjour and two brothers, Nawaf al Hazmi and Salem al Hazmi.
./technical/911report/chapter-1.txt:56:    The four men passed through the security checkpoint, owned by United Airlines and operated under contract by Argenbright Security. Like the checkpoints in Boston, it lacked closed-circuit television surveillance so there is no documentary evidence to indicate when the hijackers passed through the checkpoint, what alarms may have been triggered, or what security procedures were administered. The FAA interviewed the screeners later; none recalled anything unusual or suspicious.
./technical/911report/chapter-1.txt:62:    They were planning to hijack these planes and turn them into large guided missiles, loaded with up to 11,400 gallons of jet fuel. By 8:00 A.M. on the morning of Tuesday, September 11,2001, they had defeated all the security layers that America's civil aviation security system then had in place to prevent a hijacking. The Hijacking of American 11 American Airlines Flight 11 provided nonstop service from Boston to Los Angeles. On September 11, Captain John Ogonowski and First Officer Thomas McGuinness piloted the Boeing 767. It carried its full capacity of nine flight attendants. Eighty-one passengers boarded the flight with them (including the five terrorists).22 The plane took off at 7:59. Just before 8:14, it had climbed to 26,000 feet, not quite its initial assigned cruising altitude of 29,000 feet. All communications and flight profile data were normal. About this time the "Fasten Seatbelt" sign would usually have been turned off and the flight attendants would have begun preparing for cabin service.
./technical/911report/chapter-1.txt:64:    At that same time, American 11 had its last routine communication with the ground when it acknowledged navigational instructions from the FAA's air traffic control (ATC) center in Boston. Sixteen seconds after that transmission, ATC instructed the aircraft's pilots to climb to 35,000 feet. That message and all subsequent attempts to contact the flight were not acknowledged. From this and other evidence, we believe the hijacking began at 8:14 or shortly thereafter.
./technical/911report/chapter-1.txt:78:    At 8:21, one of the American employees receiving Ong's call in North Carolina, Nydia Gonzalez, alerted the American Airlines operations center in Fort Worth, Texas, reaching Craig Marquis, the manager on duty. Marquis soon realized this was an emergency and instructed the airline's dispatcher responsible for the flight to contact the cockpit. At 8:23, the dispatcher tried unsuccessfully to contact the aircraft. Six minutes later, the air traffic control specialist in American's operations center contacted the FAA's Boston Air Traffic Control Center about the flight. The center was already aware of the problem.
./technical/911report/chapter-1.txt:80:    Boston Center knew of a problem on the flight in part because just before 8:25 the hijackers had attempted to communicate with the passengers. The microphone was keyed, and immediately one of the hijackers said, "Nobody move. Everything will be okay. If you try to make any moves, you'll endanger yourself and the airplane. Just stay quiet." Air traffic controllers heard the transmission; Ong did not. The hijackers probably did not know how to operate the cockpit radio communication system correctly, and thus inadvertently broadcast their message over the air traffic control channel instead of the cabin public-address channel. Also at 8:25, and again at 8:29, Amy Sweeney got through to the American Flight Services Office in Boston but was cut off after she reported someone was hurt aboard the flight. Three minutes later, Sweeney was reconnected to the office and began relaying updates to the manager, Michael Woodward.
./technical/911report/chapter-1.txt:108:    At 8:52, in Easton, Connecticut, a man named Lee Hanson received a phone call from his son Peter, a passenger on United 175. His son told him: "I think they've taken over the cockpit-An attendant has been stabbed- and someone else up front may have been killed. The plane is making strange moves. Call United Airlines-Tell them it's Flight 175, Boston to LA." Lee Hanson then called the Easton Police Department and relayed what he had heard.
./technical/911report/chapter-1.txt:154:    At the same time, Boston Center realized that a message transmitted just before 8:25 by the hijacker pilot of American 11 included the phrase, "We have some planes."
./technical/911report/chapter-1.txt:158:    United 175 was hijacked between 8:42 and 8:46, and awareness of that hijacking began to spread after 8:51. American 77 was hijacked between 8:51 and 8:54. By 9:00, FAA and airline officials began to comprehend that attackers were going after multiple aircraft. American Airlines' nationwide ground stop between 9:05 and 9:10 was followed by a United Airlines ground stop. FAA controllers at Boston Center, which had tracked the first two hijackings, requested at 9:07 that Herndon Command Center "get messages to airborne aircraft to increase security for the cockpit." There is no evidence that Herndon took such action. Boston Center immediately began speculating about other aircraft that might be in danger, leading them to worry about a transcontinental flight-Delta 1989-that in fact was not hijacked. At 9:19, the FAA's New England regional office called Herndon and asked that Cleveland Center advise Delta 1989 to use extra cockpit security.
./technical/911report/chapter-1.txt:220:    FAA Control Centers often receive information and make operational decisions independently of one another. On 9/11, the four hijacked aircraft were monitored mainly by the centers in Boston, New York, Cleveland, and Indianapolis. Each center thus had part of the knowledge of what was going on across the system. What Boston knew was not necessarily known by centers in New York, Cleveland, or Indianapolis, or for that matter by the Command Center in Herndon or by FAA headquarters in Washington.
./technical/911report/chapter-1.txt:266:FAA Awareness. Although the Boston Center air traffic controller realized at an early stage that there was something wrong with American 11, he did not immediately interpret the plane's failure to respond as a sign that it had been hijacked. At 8:14, when the flight failed to heed his instruction to climb to 35,000 feet, the controller repeatedly tried to raise the flight. He reached out to the pilot on the emergency frequency. Though there was no response, he kept trying to contact the aircraft.
./technical/911report/chapter-1.txt:276:    The controller told us that he then knew it was a hijacking. He alerted his supervisor, who assigned another controller to assist him. He redoubled his efforts to ascertain the flight's altitude. Because the controller didn't understand the initial transmission, the manager of Boston Center instructed his quality assurance specialist to "pull the tape" of the radio transmission, listen to it closely, and report back.
./technical/911report/chapter-1.txt:278:    Between 8:25 and 8:32, in accordance with the FAA protocol, Boston Center managers started notifying their chain of command that American 11 had been hijacked. At 8:28, Boston Center called the Command Center in Herndon to advise that it believed American 11 had been hijacked and was heading toward New York Center's airspace.
./technical/911report/chapter-1.txt:282:    The Herndon Command Center immediately established a teleconference between Boston, New York, and Cleveland Centers so that Boston Center could help the others understand what was happening.
./technical/911report/chapter-1.txt:284:    At 8:34, the Boston Center controller received a third transmission from American 11:
./technical/911report/chapter-1.txt:290:Military Notification and Response. Boston Center did not follow the protocol in seeking military assistance through the prescribed chain of command. In addition to notifications within the FAA, Boston Center took the initiative, at 8:34, to contact the military through the FAA's Cape Cod facility. The center also tried to contact a former alert site in Atlantic City, unaware it had been phased out. At 8:37:52, Boston Center reached NEADS. This was the first notification received by the military-at any level-that American 11 had been hijacked:
./technical/911report/chapter-1.txt:292:    FAA: Hi. Boston Center TMU [Traffic Management Unit], we have a problem here. We have a hijacked aircraft headed towards New York, and we need you guys to, we need someone to scramble some F-16s or something up there, help us out.
./technical/911report/chapter-1.txt:316:    UAL 175: Yeah. We figured we'd wait to go to your center. Ah, we heard a suspicious transmission on our departure out of Boston, ah, with someone, ah, it sounded like someone keyed the mikes and said ah everyone ah stay in your seats.
./technical/911report/chapter-1.txt:356:    Meanwhile, a manager from Boston Center reported that they had deciphered what they had heard in one of the first hijacker transmissions from American 11: Boston Center: Hey . . . you still there?
./technical/911report/chapter-1.txt:360:    Boston Center: . . . as far as the tape, Bobby seemed to think the guy said that "we have planes." Now, I don't know if it was because it was the accent, or if there's more than one, but I'm gonna, I'm gonna reconfirm that for you, and I'll get back to you real quick. Okay? New England Region: Appreciate it.
./technical/911report/chapter-1.txt:364:    Boston Center: Planes, as in plural.
./technical/911report/chapter-1.txt:366:    Boston Center: It sounds like, we're talking to New York, that there's another one aimed at the World Trade Center.
./technical/911report/chapter-1.txt:370:    Boston Center: A second one just hit the Trade Center.
./technical/911report/chapter-1.txt:374:    Boston Center immediately advised the New England Region that it was going to stop all departures at airports under its control. At 9:05, Boston Center confirmed for both the FAA Command Center and the New England Region that the hijackers aboard American 11 said "we have planes." At the same time, New York Center declared "ATC zero"-meaning that aircraft were not permitted to depart from, arrive at, or travel through New York Center's airspace until further notice.
./technical/911report/chapter-1.txt:376:    Within minutes of the second impact, Boston Center instructed its controllers to inform all aircraft in its airspace of the events in New York and to advise aircraft to heighten cockpit security. Boston Center asked the Herndon Command Center to issue a similar cockpit security alert nationwide. We have found no evidence to suggest that the Command Center acted on this request or issued any type of cockpit security alert.
./technical/911report/chapter-1.txt:404:    By 9:25, FAA's Herndon Command Center and FAA headquarters knew two aircraft had crashed into the World Trade Center. They knew American 77 was lost. At least some FAA officials in Boston Center and the New England Region knew that a hijacker on board American 11 had said "we have some planes." Concerns over the safety of other aircraft began to mount. A manager at the Herndon Command Center asked FAA headquarters if they wanted to order a "nationwide ground stop." While this was being discussed by executives at FAA headquarters, the Command Center ordered one at 9:25.
./technical/911report/chapter-1.txt:412:    At 9:21, NEADS received a report from the FAA: FAA: Military, Boston Center. I just had a report that American 11 is still in the air, and it's on its way towards-heading towards Washington. NEADS: Okay. American 11 is still in the air?
./technical/911report/chapter-1.txt:434:    The mention of a "third aircraft" was not a reference to American 77. There was confusion at that moment in the FAA. Two planes had struck the World Trade Center, and Boston Center had heard from FAA headquarters in Washington that American 11 was still airborne. We have been unable to identify the source of this mistaken FAA information.
./technical/911report/chapter-1.txt:440:    At the suggestion of the Boston Center's military liaison, NEADS contacted the FAA's Washington Center to ask about American 11. In the course of the conversation, a Washington Center manager informed NEADS:"We're looking- we also lost American 77." The time was 9:34. This was the first notice to the military that American 77 was missing, and it had come by chance. If NEADS had not placed that call, the NEADS air defenders would have received no information whatsoever that the flight was even missing, although the FAA had been searching for it. No one at FAA headquarters ever asked for military assistance with American 77.
./technical/911report/chapter-1.txt:442:    At 9:36, the FAA's Boston Center called NEADS and relayed the discovery about an unidentified aircraft closing in on Washington:"Latest report. Aircraft VFR [visual flight rules] six miles southeast of the White House. . . . Six, southwest. Six, southwest of the White House, deviating away." This startling news prompted the mission crew commander at NEADS to take immediate control of the airspace to clear a flight path for the Langley fighters:"Okay, we're going to turn it . . . crank it up. . . . Run them to the White House." He then discovered, to his surprise, that the Langley fighters were not headed north toward the Baltimore area as instructed, but east over the ocean." I don't care how many windows you break," he said." Damn it. . . . Okay. Push them back."
./technical/911report/chapter-1.txt:448:    Right after the Pentagon was hit, NEADS learned of another possible hijacked aircraft. It was an aircraft that in fact had not been hijacked at all. After the second World Trade Center crash, Boston Center managers recognized that both aircraft were transcontinental 767 jetliners that had departed Logan Airport. Remembering the "we have some planes" remark, Boston Center guessed that Delta 1989 might also be hijacked. Boston Center called NEADS at 9:41 and identified Delta 1989, a 767 jet that had left Logan Airport for Las Vegas, as a possible hijack. NEADS warned the FAA's Cleveland Center to watch Delta 1989. The Command Center and FAA headquarters watched it too. During the course of the morning, there were multiple erroneous reports of hijacked aircraft. The report of American 11 heading south was the first; Delta 1989 was the second.
./technical/911report/chapter-1.txt:598:    We found no evidence that, at this critical time, NORAD's top commanders, in Florida or Cheyenne Mountain, coordinated with their counterparts at FAA headquarters to improve awareness and organize a common response. Lower-level officials improvised-for example, the FAA's Boston Center bypassed the chain of command and directly contacted NEADS after the first hijacking. But the highest-level Defense Department officials relied on the NMCC's air threat conference, in which the FAA did not participate for the first 48 minutes.
./technical/911report/chapter-6.txt:43:                United States, worked as a cabdriver in Boston, and sent money back to his fellow
./technical/911report/chapter-6.txt:44:                plotters. After Abu Hoshar's release, Hijazi shuttled between Boston and Jordan
./technical/911report/chapter-6.txt:55:                Finally, back in Amman from Boston, Hijazi gradually accumulated bomb-making
./technical/911report/chapter-6.txt:219:                that Hijazi had lived in California and driven a cab in Boston and that Deek was a
./technical/911report/chapter-7.txt:1050:            On July 30, Shehri traveled alone from Fort Lauderdale to Boston. He flew to San
./technical/911report/chapter-7.txt:1060:                Los Angeles in early June. Atta flew from Boston to Las Vegas via San Francisco at
./technical/911report/chapter-7.txt:1563:                September 9, he flew from Baltimore to Boston. By then, Shehhi had arrived there,
./technical/911report/chapter-7.txt:1567:                to Boston to connect to American Airlines Flight 11. The two spent their last night
./technical/911report/chapter-7.txt:1570:                hotel in Newton, Massachusetts, just outside of Boston.
./technical/911report/chapter-7.txt:1573:                their last hours at two Boston hotels.
./technical/911report/chapter-8.txt:76:                attacks on London, Boston, and New York. Attorney General John Ashcroft was briefed
```
