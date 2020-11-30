# Introduction to the Command Line

![A computer terminal being used by an Imperial Officer from Star Wars](https://motherboard-images.vice.com/content-images/contentimage/33251/1462385247931989.png)

> This guide will go through what the the command line interface (`CLI`) is, why we need it, and how we're going to use it! 

---

You'll often hear the `command line` referred to in different ways:

`terminal`
`CLI`
`command prompt`
`shell`

Here we'll refer to it as the `terminal` and `CLI` (command line interface).

---

## A Little Background

<img src="https://i.stack.imgur.com/voqT3.jpg" alt="An image of an old punch card machine" width="500px">

Before the introduction of the graphical user interface (screens with a mouse pointer), the only way to interact with your computer was through the `terminal`. [The earliest terminals](https://en.wikipedia.org/wiki/Punched_card) (dating back to the mid 1960's) literally punched out the user's program (hand-written and then transcribed) onto to a card. The terminal has evolved exponentially since then, but it is still text-based, and it is still the most efficient way to communicate with our machines.

---

## CLI Basics

Alright, Let's get into it. Go ahead and open the terminal. A good shortcut for this is `cmd + space` to pull up the Mac spotlight, and then type "terminal" and hit enter.

![Screenshot of the terminal listing our current location as "~"](https://i.imgur.com/U3CIEw1.png)
> _As a sandtrooper I'm naturally on Tatooine_

In your terminal, you'll see some information; which user is currently logged in, the name of the computer, and where you are in your computer right now. (there might be some slight variation, and this output is configurable). You should see a little squiggly line toward the end.  

```shell
~
```

_(if you don't, type `cd` and hit enter)_

That little squiggle is called a `tilde`, and it indicates that you are at your home directory (_you'll see it on the key above `tab` on your keyboard_). 

> What's my home directory you say? Lets find out! 

Type `ls` and hit enter.

```shell
ls
```

This command "lists" all the items in your current `directory`. (you can think of directories as folders). You should see some directories that look fairly familiar, such as Applications, Desktop, Documents, and Photos. To get into one of these directories, we can use the `cd` command.

```shell
cd
```

`cd` stands for "change directory". Let's get into the "Documents" directory.

```shell
cd Documents 
```

Notice that our current directory has changed to `~/Documents`. 

![Screen Shot of the terminal listing our current location as "~/Documents"](https://i.imgur.com/nDeauCk.png)

Let's "list" what's inside.

```shell
ls
```

Probably some directories (folders), and files, each will be displayed differently. Directories are usually indicated by a color of some sort, and files are usually plain. 

But for now, let's go back to the Desktop directory. To navigate back, type `cd ..`

```shell
cd ..
```

`..` indicates going back one directory. _A single `.` indicates right here where you are_

```shell
..
```
```shell
.
```

---

![Luke Skywalker looking at the horizon at dusk of the desert planet Tatooine. Two suns are setting in the desolate landscape](https://i.imgur.com/Tyf5DEP.jpg)
> I like to remember it by the twin suns of Tatooine, a BACKwater planet.

---

Make sure you put a space between `cd` and `..` or the terminal will yell at you. 

Now that took us back to the home directory `~`, right where we were before. (if you want to jump to the home directory from any location, just type `cd` by itself). 

Now let's make a file of our own! Type `touch luke-skywalker.txt`.

```shell
touch luke-skywalker.txt
```

> `touch` is a command used to create files! You have a lot of power with `touch`, because you can add any extension you like to files you create, such power!

_When you are creating your file, make sure that your filename has no spaces in it, as the command line will interpret "luke" and "skywalker" as two separate files to create if there is a space_

---

![Luke Skywalker laying in the snow of Hoth, nearly dead.](https://i.ytimg.com/vi/PIGeIdrS-d8/maxresdefault.jpg)

I think our file needs a better place to live, rather than exposed out in the hoth-like conditions of the home directory. Let's create a _new_ directory for our file to live in. Type `mkdir tauntaun`.

```shell
mkdir tauntaun
```

`mkdir` stands for "make directory". Let's run `ls` again to list our new directory.

![Screen Shot of terminal after running the "ls" command, showing the file "luke-skywalker.txt" and the directory "tauntaun"](https://i.imgur.com/Ds0mKE0.png)

Luke is looking a little _chilly_ though, so let's help him out and put him _inside_ the tauntan.

![Han Solo cutting open a tauntaun with a lightsaber](https://img.buzzfeed.com/buzzfeed-static/static/2017-12/8/19/asset/buzzfeed-prod-fastlane-02/anigif_sub-buzz-13450-1512778264-6.gif?output-quality=auto&output-format=auto&downsize=360:*)

```shell
mv luke-skywalker.txt tauntaun
```

`mv` takes two `operands` (parameters), the first one is the item to be moved, and the second is the `directory` it is to be moved to.

Let's run `ls` again to see what changed.

![Screen Shot of terminal after running the "ls" command, showing the directory "tauntaun"](https://i.imgur.com/6YGsNzk.png)

`luke-skywalker.txt` is gone, which is expected, but let's check and make sure he's _inside_ the `tauntaun` directory.

---

```shell
cd tauntaun
```
```shell
ls
```
Now you should see `luke-skywalker.txt` inside there!!

![Toy figure of tauntaun with luke skywalker inside](https://2warpstoneptune.files.wordpress.com/2015/03/esb-tauntaun-1980-1.jpg)

Is there anything else you can think of that Tauntauns are full of? Let's add them in!

```shell
touch guts.txt
```
```shell
touch bad-smells.txt
```

![Screen Shot of running the command "touch guts.txt" inside the tauntaun directory](https://i.imgur.com/tmV5L4P.png)
> When we run this command, it creates that file _inside_ the tauntaun directory because our current location _is inside of it_.

now when we type `ls`, we see that our "tauntaun" directory is full of guts, bad smells, and Luke Skywalker! 

![Screen Shot of tauntaun directory with the files "bad-smells.txt", "guts.txt", and "luke-skywalker.txt"](https://i.imgur.com/ayrzn8x.png)

Let's make a *directory* now. We'll call it "stomach".

```shell
mkdir stomach
```

Now enter that directory with the `cd` command

```shell
cd stomach
```

Inside the stomach, let's make another file, this time with a different file extension just to mix it up.

```shell
touch hoth-hog.html
```

Let's run `ls` and make sure everything is where we want it to be.

![Screen Shot of the file hoth-hog.html inside ~/hoth/tauntaun/stomach](https://i.imgur.com/togz4nn.png)

Looks good!

---

At this point, we are _inside_ the stomach of the tauntaun. but what if we wanted to go back __multiple__ directories?

We can do that with the by chaining our `..` operand. To go back two directories, we would say

```shell
cd ../../
```

> This will take us out of the `stomach` directory, and _also_ out of the `tauntaun` directory. (_A single `../` would have just taken us out of the `stomach` directory._)

![Han Solo saying "Ah! I thought they smelled bad on the outside!" After stuffing Luke Skywalker inside the guts of his dead Tauntaun](https://64.media.tumblr.com/7d9bdd2d4a983d0fd9e7e7e074d0263f/tumblr_nss88fitrs1s27326o8_r1_250.gif)

---

## Useful CLI commands

### Print working directory (where you currently are)

```shell
pwd
```

`pwd` allows you to check where you are currently located in your system.

It stands for "print working directory", and it shows you where you currently are. It will print out the `path` of where you are all the way back to the _root_ directory (`/`).

> `~` = _home directory_
> `/` = _root directory_

---

### Print file contents

```shell
cat
```

`cat` shows us the contents of a file right inside the terminal itself. Keep in mind this command is most useful for shorter files that are only a few lines long. (cat stands for concatenate, which means "link (things) together in a chain or series").

Here's an example of what the `cat` command prints out for a small html file.

![Screenshot of output from cat command, a small html file printed to the terminal after running the "cat" command](https://i.imgur.com/shjJczG.png)

---

### Search

```shell
grep
```

The `grep` command searches any given input, selecting lines that match, and printing out what did match! Let's look at a simple example:

```shell
echo "I am a test string I created just now" | grep "created"
```
![Screen Shot of a string saying "I am a test string I created just now" | grep "created", and then an output from the terminal with the word "created" highlighted.](https://i.imgur.com/FnuA8mm.png)
_you can ignore `echo`, it simply outputs your input. It "echoes" what you type and is useful for examples._

See how grep highlighted our search criteria?

To fully understand how this is working, see `pipe` (`|`) in the next example and give it a go yourself.

---

### Pipe output

```shell
|
```

By using `pipe` (`|`), you can take the _output_ of any command, and pass it into another command. 

There are many things this could be used for, but a common one you can focus on now is using it in conjunction with `grep` to search for things. If you wanted to search the contents of a file, you could output it's contents using `cat`, and then search with `grep` using a pipe. 

> `name-list.txt` is a simple list of names. We can output them using the `cat` command

![Screen Shot of a list of names after running the "cat name-list.txt" command](https://i.imgur.com/HkshsST.png)

Now if we take that output and __pipe__ it _to_ `grep`, we can search it's output.

```shell
cat name-list.txt | grep "Han Solo"
```
![Screen Shot of the command cat name-list.txt | grep "Han Solo". The output shows only the line with Han Solo's name on it.](https://i.imgur.com/3ofQ1mL.png)

`grep` only gives output if it finds a match for what you passed it! In this case, it gave us the line with our search criteria: `Han Solo`.

_If we wanted to see lines __around__ our match, we could use a `flag` of `-C`:_
```shell
cat name-list.txt | grep "Ahsoka Tano" -C 2
```
![Screen Shot of the use of the -C flag at the end of our grep search to see lines above and below our results.](https://i.imgur.com/0zv0rAC.png)
See our highlighted result? But it __also__ gave us 2 lines above and below when we used the `-C` flag. 

> `-C` gives lines before and after match
> `-B` gives lines before match
> `-A` gives lines after match

_Remember that `|` can be used with __anything__ that gives output. (`grep` is just an example)_

---

### File Preview

```shell
head
```

Using the `head` command on a file will give you only the first few lines of the file. This can be helpful if you need to see a header, license, or just to check the structure of a document.

---

### Line Numbers

```shell
-n
```

If you want to see your output numbered by line, you can use the `-n` flag. Any command that gives output can be used with the `-n` flag. Here's an example using `cat` on our `names-list.txt` file.

![Screen Shot of file output but with a numbered list on the left-hand side of the results](https://i.imgur.com/Z7fRj59.png)

---

### Copy

```shell
cp
```

`copy` takes two parameters, the first is the file to be copied, and the second is what you want to call the copied file (_it can't have the same name as the original_). 

ex: `cp file1.txt file1-copy.txt` - this will create a copy of `file1.txt` named `file1-copy.txt` in the same directory you are currently in.

---

### Delete (remove)

For files:
```shell
rm
```

For directories:
```shell
rm -r
```

`rm` stands for remove, but the `-r` can be a little confusing. The `-` indicates a flag, and the `r` stands for "recursively". We'll get more into recursion later, but for now, you can think of `-r` as a __way to manipulate directories when a command without `-r` won't work__.

For example, running `rm tauntaun` will tell you `rm: tauntaun: is a directory`. So we need to use the `-r` *flag*. 

> _Quick note on deleting and modifying files: When you give CLI commands, there is usually no confirmation and no "undo's". If we want the command line to be a little more forgiving, we can use the "interactive" flag, "-i"._

---

### Interactive (confirm commands)

```shell
-i
```

`-i` will make the command line interactively ask us if we want to perform destructive actions.

```shell
rm -i -r hoth-hog.html
```

Using the `-i` flag will force you to confirm certain actions, and you can simply reply `y` or `n` to continue or cancel the operation.

---

### Manual (help pages)

```shell
man
```

`man` stands for manual, and is used in conjunction with other commands. If you want to learn more about any specific command, you can simply type `man` before it, and you'll get a very thorough explanation of what it can do. For example, if you wanted to learn more about the `mkdir` command, you would type `man mkdir`.

```shell
man mkdir
```

To __exit__ the man page, hit `q`.

---

### Homework

![Darth Vader cutting down rebels with his lightsaber in the hallway of a rebel ship.](https://thumbs.gfycat.com/InsidiousRecentFlies-small.gif)

* Download this repo to your local machine.
  * Click the green `code` button at the top of this page

    ![Screen Shot of button saying "Code" from GitHub.](https://i.imgur.com/5iEoUgp.png)
  * In the dropdown menu that appears, click "Download ZIP", and save the file on your computer. (Somewhere you can conveniently access it.)

    ![Screen Shot of button saying "Download Zip"](https://i.imgur.com/wAcWmrB.png)
* Use the terminal to navigate to the newly downloaded `directory`.
  * The name of the folder will be `command-line-master`. `master` just means what _branch_ of the code you have.

    ![Screen Shot 2020-11-30 at 8.42.15 AM](https://i.imgur.com/yjlXIej.png)
* `cd` into the `rebel-traitor-hunt` directory 
* Use the `cat` command to read the contents of the file `instructions-from-vader` to get started!

##### Tips:
* Keep this webpage open for referencing commands you'll need, and for brushing up on the lesson as you go along.
* For extra help, [open up the walkthrough file](https://github.com/mikelbrierly/command-line/blob/master/WALKTHROUGH.md). It has detailed hints, and the commands to run if you still need that extra push.

---

> _If you want to learn more about the command line, or find more commands, MDN has a wealth of information, and goes into a lot of detail explaining what you can accomplish with this tool. [For more reading, this is a good starting point.](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line)_
