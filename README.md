# Imperial Command Line Training

![alt text](http://img.lum.dolimg.com/v1/images/Darth-Vader_6bda9114.jpeg?region=0%2C23%2C1400%2C785&width=768)

### A Little History

Alright troopers! Today we're learning about the command line. What is it, why we need it, and how we're going to use it. The command line is also known as the Terminal, CLI, Command Prompt, Shell, etc. I'll mostly be referring to it as the Terminal and the Command Line.

Before the introduction of the graphical user interface, the only way to interact with your computer was through the Terminal. The earliest terminals (dating back to the mid 1960's) literally printed their output to a roll of paper as they interacted with the computer program. If you really want a blast from the galactic past, go look up [
punched-card data processing](https://en.wikipedia.org/wiki/Punched_card) (I heard Darth Plagueis used one way back in the day) Today the command line is still the preferred way to interact with computers for advanced users. It gives you much more control and power over your operating system.

### Command Line Basics

Alright, Let's get into it. Go ahead and open the terminal. A good shortcut for this is CMD + SPACE to pull up spotlight, and then type "terminal" and hit enter.

      CMD + SPACE

Here we can see which user is currently logged in, the name of the computer, and where you are in your computer right now. You should see a little squiggly line indicating where you are.  

      ~

(if you don't, type "cd" and hit enter)   
That little squiggle is called a tilde, and it indicates that you are at your home directory. What's my home directory you say? Lets find out! Type "ls" and hit enter.

      ls

This command "lists" all the items in your current directory. (you can think of directories as folders). You should see some directories that look fairly familiar, such as Applications, Desktop, Documents, Twilek_Dancers, Photos, and more. To get into one of these directories, we can use the "cd" command.

      cd

"cd" stands for "change directory". If we wanted to enter the "Documents" directory, we would simply type `cd Documents`. Notice that our current location has changed to "~/Documents". Let's run "ls" and see what's inside! Probably a bunch of documents. But what if we wanted to go back and see what's in Desktop instead? To navigate back, type "cd ..".

      cd ..

".." indicates going back one directory. "." indicates where you are.

    ..

    .

I like to remember it by the twin suns of Tatooine (a BACKwater planet), and the single Death Star (right where we ARE).
Make sure you put a space between "cd" and ".." or it will yell at you. Now that took us back to the "Home Directory", right where we were before. (if you want to jump to the home directory from any location, just type "cd" by itself). Now let's make a file of our own! Type "touch bantha_poodoo.txt".

      touch bantha_poodoo.txt

That may sound gross, but it's better than tasting it I'll tell you that much. When you are creating your file, make sure that your filename has no spaces in it, as the command line will interpret "bantha" and "poodoo" as two separate commands if there is a space. I think our file needs a better place to live, rather than exposed out in the cold hoth-like conditions of the home directory. Let's create a new directory for it to live in. Type "mkdir jedi".

      mkdir jedi

"mkdir" stands for "make directory" (at least that one is straightforward). Let's run "ls" again to see our new directory. But what's this! The bantha_poodoo still needs to be put in the directory "jedi". To do this, type "mv bantha_poodoo.txt jedi"

      mv bantha_poodoo.txt jedi

"mv" takes two parameters, the first one is the item to be moved, and the second is the directory it is to be moved to. Now we can see what our Jedi is full of by changing directories into jedi, and then listing what's inside.

    cd jedi

    ls

Is there anything else you can think of that Jedi are full of? Let's add them in!

    touch sour_blue_milk.txt

    touch mynock_spit.txt

now when we type "ls", we see that our "jedi" directory is full of sour_blue_milk, mynock_spit, and bantha_poodoo! Let's add a *directory* now. We'll call it "brain".

      mkdir brain

when we "cd" into this directory and list what's inside, we see it's empty, that's perfect! It's a very accurate Jedi model we've created. Let's make one last directory inside "brain" for good measure.

      mkdir medulla

"cd" into "medulla" (also empty). Now if we want to go back two directories to "jedi", we can chain our "cd" commands into one! Type "cd ../../"

      cd ../../

This will take us back as many times as you type "../". To check where you ended up, you can type "pwd".

      pwd

This command stands for "print working directory", and it shows you where you currently are. We should be in the "jedi" directory with some empty text files. Let's add something to bantha_poodo.txt by typing "open bantha_poodo.txt".

      open bantha_poodo.txt

We'll type in a common trait of Bantha Poodoo to our file: "Smelly". Now we can save and close the text editor that popped up. (If we wanted to read what's in our file without having to open up the text editor, we can type "cat bantha_poodoo.txt").

      cat bantha_poodoo.txt

This will show us the contents of a file right inside the terminal itself. Keep in mind this command is most useful for shorter files that are only a few lines long. (cat stands for concatenate, which means "link (things) together in a chain or series") Make of it what you will.

But I have a feeling that we are a little short on bantha_poodoo... if we wanted to duplicate this file, we can type "cp bantha_poodoo.txt bantha_poodoo2.txt"

      cp bantha_poodoo.txt bantha_poodoo2.txt

This "copy" command takes two parameters, the first is the file to be copied, and the second is what you want to call the copied file (it can't have the same name as the original). Now when we type "ls", we see our second bantha_poodoo is there! And if we run "cat" on the file, we see that the contents of the original file were also copied. bantha_poodoo is a perfect file to live in our jedi directory, but mynock_spit just doesn't feel descriptive enough... I think we should rename our "mynock_spit" file to "sleemo" (huttese for slimeball). To do this, we will use the "move" command. It definitely doesn't make sense, but it's just the way it is. Type "mv mynock_spit.txt sleemo.txt".

      mv mynock_spit.txt sleemo.txt

If the second parameter of the "mv" command is NOT a directory, it will rename the item to whatever you typed for the second parameter. If the second parameter is a file that already exists, it will yell at you. Now lets take a step back and admire our jedi directory by typing "ls". ...I think we made a mistake earlier... do you see it? Jedi's don't have brains at all! We should definitely remove it. To do this, we'll type "rm -r brain".

      rm -r brain

"rm" stands for remove, but the -r is a little confusing. The "-" indicates a flag, and the "r" stands for "recursively". We'll get more into recursion when we talk about Jawascript, but for now, you can think of the "-r" as a way to manipulate directories when a command without the "-r" won't work. For example, running "rm brain" will tell you "rm: brain: is a directory". So we need to use the "-r" *flag*. While we're on the topic of flags and removing files, I should probably mention to you that the command line is like Jabba the Hutt. No second chances, No forgiveness. If you tell it to do something, it'll do it, no questions asked, no undo's. So if we want the command line to be a little more forgiving, we can use the "interactive" flag, "-i".

      -i

This will make the command line interactively ask us if we want to perform destructive actions. Let's try it out. Make a new directory called "test", and then type "rm -i -r test".

      rm -i -r test

It should ask you some questions, and you can simply reply "y" or "n" to tell it to continue or cancel the operation. Man. Look at all the stuff you know now. Speaking of "man", If you want to learn more about any specific command, you can simply type "man" before the command, and you'll get a very thorough explanation of what it can do. For example, if you wanted to learn more about the "mkdir" command, you would type "man mkdir"

      man mkdir

To exit out of the man page, just hit "q".

That's it for command line basics!    
Good work troopers, and we'll see you next time for "the command line strikes back"! Hail Vader!
