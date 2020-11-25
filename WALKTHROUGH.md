# Step-by-step Walkthrough
![Kylo Ren probing Poe Dameron's mind for the location of the map to Luke Skywalker](https://64.media.tumblr.com/9bddecbc2648faef0157b0b0a6b91225/tumblr_inline_odpjg12noZ1r7xgxi_540.gifv)

<h3>Entering the Death Star</h3>
<details>
  <summary>Hint</summary>

  carefully read the first line of `instructions-from-vader` and use the `cd` command to change directories.
</details>

<details>
  <summary>Answer</summary>

  ```shell
  cd death-star
  ```
</details>

---

<h3>Parsing the stormtrooper report log</h3>
<details>
  <summary>Hint</summary>
  
  _This line from `instructions-from-vader` is the most important for your next steps:_

  `...marked all of the places that the traitor infiltrated with the word SECURITY-BREACH in the file stormtrooper-report-log.`

  Use a combination of `pipe` (`|`), `grep`, and `cat` to get just the info you need.
</details>

<details>
  <summary>Answer</summary>

  ```shell
  cat stormtrooper-report-log | grep "SECURITY-BREACH"
  ```
</details>

---

<h3>Your first lead</h3>
<details>
  <summary>Hint</summary>
  
  Information on all troopers is laid out in the `imperial-personnel` directory.

  Again, Use a combination of `pipe` (`|`), `grep`, and `cat` to find info on a trooper.
</details>

<details>
  <summary>Answer</summary>

  ```shell
  cat imperial-personnel | grep "Salacius"
  ```
</details>

---

<h3>Finding the informant</h3>
<details>
  <summary>Hint 1</summary>
  
  Use `head` or `less` to see the beginning of the `imperial-personnel` file, which has extra information for us. (To exit `less` hit `q`)

  Also don't forget about the `-n` flag, which will give line numbers to your output.

</details>
<details>
  <summary>Hint 2</summary>
  
  We know our informant is female, so she could be either of these two:
  ```
  Salacius Sun    F       26      Plasteel Barracks, line 40
  Salacius Church F       38      Bespin Barracks, line 179
  ```

</details>

<details>
  <summary>Answer</summary>

  One of these two commands take us to the informant...

  ```shell
  cat -n barracks/Plasteel | grep 40
  ```

  ```shell
  cat -n barracks/Bespin | grep 179
  ```
</details>

---

<h3>Reading interviews</h3>
<details>
  <summary>Hint</summary>
  
  _Copy the two possible interview numbers for reference._

  Check the format of the files in the `death-star/interviews` directory, and `cat` out the contents of the pertinent interviews.

</details>

<details>
  <summary>Answer</summary>


  ```shell
  cat interviews/interview-699607
  ```

  ```shell
  cat interviews/interview-47246024
  ```
</details>

---

<h3>Needle in a plasteel stack</h3>
<details>
  <summary>Hint 1</summary>
  
  _We know the traitor is male, over 6' tall, wearing battle damaged Kaminoan armor with a TKID starting with 113 and ending in 8._

  We'll have to sort through the `armor-info` file. 

  Once again use `cat`, pipe (`|`), and `grep` to parse the data.

</details>

<details>
  <summary>Hint 2</summary>
  
  Look at the `-A` option you can add to `grep`. It allows you to show a certain number of lines from the file after each "match" in your search. 
  
  _You could also use `-B` (lines before), or `-C` (lines before and after)_

</details>

<details>
  <summary>Answer</summary>


  ```shell
  cat armor-info | grep 113 -A 6
  ```
</details>

---

<h3>Stay on target</h3>
<details>
  <summary>Hint 1</summary>
  
  Based on our hints and the output of the previous command, we know that the traitor is one of these two:

  ```
  --
  TK ID#  113Q4H8
  Make: Kamino
  Condition: Heavily Damaged
  Owner: Richard LeParmentier
  Height: 6'3"
  Weight: 165 lbs

  --
  TK ID#  113UVX8
  Make: Kamino
  Condition: Heavily Damaged
  Owner: Janthaus Staucks
  Height: 6'2"
  Weight: 195 lbs
  ```

</details>

<details>
  <summary>Hint 2</summary>
  
  Look at the `-A` option you can add to `grep`. It allows you to show a certain number of lines from the file after each "match" in your search. 
  
  _You could also use `-B` (lines before), or `-C` (lines before and after)_

</details>

<details>
  <summary>Answer</summary>


  ```shell
  cat armor-info | grep 113 -A 6
  ```
</details>

---

<h3>I have you now</h3>
<details>
  <summary>Hint 1</summary>
  
  The only thing left to do is find out what groups our two suspects are members of. 

  `cd` into the `memberships` directory.

</details>

<details>
  <summary>Hint 2</summary>
  
  You can use `cat` to print out the contents of multiple files by adding a space between them like so: `cat file1 file2 file3`.

  Use that tactic to check who is a member of all four groups that we know the traitor is a part of from the `stormtrooper-report-log` step early on.

</details>

<details>
  <summary>Answer</summary>

  ```shell
  cat Imperial_Dejarik_Club Blue_Milkaholics_Anonymous Ewotic_Ewoks Aim_Like_A_Stormtrooper_101 | grep "Janthaus Staucks"
  ```
  
  ```shell
  cat Imperial_Dejarik_Club Blue_Milkaholics_Anonymous Ewotic_Ewoks Aim_Like_A_Stormtrooper_101 | grep "Richard LeParmentier"
  ```
</details>

---

### Contact Lord Vader

![An imperial officer walks in to deliver news to Darth Vader](https://64.media.tumblr.com/tumblr_m6gn0ikWJO1r2pn76o2_500.gif)

Open `contact_vader` and follow the instructions in that file.





