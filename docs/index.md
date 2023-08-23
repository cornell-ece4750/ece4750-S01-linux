
ECE 4750 Section 1: Linux Development Environment
==========================================================================

 - Author: Christopher Batten
 - Date: August 26, 2022
 - Distilled by Cecilio C. Tamarit (August 23, 2023) 

**Table of Contents**

 - Source the Setup Script
 - Linux Command Line
 - GitHub Account Setup
 - Git Version Control System
 - To-Do On Your Own
 - For ECE 2400 Alumni or Advanced Students

This discussion section serves as gentle introduction to the basics of
using the Linux development environment on the `ecelinux` servers
including how to log into the servers, how to work at the Linux command
line, and how to use Git version control. You should start by logging
into the `ecelinux` servers using the remote access option of your choice
based on working through the remote access tutorial for the discussion
section:

 - <https://www.csl.cornell.edu/courses/ece4750/handouts/ece4750-tut0-access.pdf>

If you are having trouble using VSCode then use PowerSell or Mac Terminal
for the discussion section.
<!--
Source the Setup Script
--------------------------------------------------------------------------

The very first thing you need to do after logging into the `ecelinux`
serfvers is source the course setup script. This will ensure your
environment is setup with everything you need for working on the
programming assignments. Enter the following command on the command line:

    % source setup-ece4750.sh

Note that you do not need to enter `%` character. In a tutorial like
this, the `%` simply indicates what you should type at the command line.
You should now see `ECE4750` in your prompt which means your environment
is setup for the course.

It can be tedious to always remember to source the course setup script.
You can also use _auto setup_ which will automatically source the course
setup for you when you log in. Note that if the environment for ECE 4750
conflicts with the environment required by a different course then you
will need to manually source the setup script when you are working on
this course. Enter the following command on the command line to use auto
setup:

    % source setup-ece4750.sh --enable-auto-setup

Now log out of the `ecelinux` server and log back in. You should see `ECE
4750` in the prompt meaning your environment is automatically setup for
the course. If at anytime you need to disable auto setup you can use the
following command:

    % source setup-ece4750.sh --disable-auto-setup

Now that we have source the course setup script we can start to explore
the Linux command line.
-->
Linux Command Line
--------------------------------------------------------------------------

We will using the `ecelinux` servers which run the Red Hat Enterprise
Linux 7 operating system for all of the programming assignments. The
heart of the Linux operating system is the Linux command line. This is a
text-based console where you can enter commands to interact with the
operating system.

### Hello World

We begin with the ubiquitous "Hello, World" example. To display the
message "Hello, World" we will use the `echo` command. The `echo` command
simply "echoes" its input to the console.

    % echo "Hello, World"

The string we provide to the echo command is called a _command line
argument_. We use command line arguments to tell commands what they
should operate on. Again, note that you do not need to enter `%`
character.

### Manual Pages

You can learn more about any Linux command by using the `man` command.
Try using this to learn more about the `echo` command.

    % man echo

You can use the up/down keys to scroll the manual one line at a time, the
space bar to scroll down one page at a time, and the `q` key to quit
viewing the manual.

### Create, View, and List Files

We can use the echo command and a feature called _command output
redirection_ to create simple text files. Command output redirection is
discussed more in the full tutorial. Command output redirection uses the
`>` operator to take the output from one command and "redirect" it to a
file. The following commands will create a new file named
`ece4750-sec01.txt` that simply contains the text "Computer
Architecture".

    % echo "Computer Architecture" > ece4750-sec01.txt

We can use the `cat` command to quickly display the contents of a file.

    % cat ece4750-sec01.txt

For larger files, `cat` will output the entire file to the console so it
may be hard to read the file as it streams past. We can use the `less`
command to show one screen-full of text at a time. You can use the
up/down keys to scroll the file one line at a time, the space bar to
scroll down one page at a time, and the `q` key to quit viewing the file.

    % less ece4750-sec01.txt

The `>` command output redirection operator will always create a brand
new file (even if the target output file already exists). You can use the
`>>` operator to append lines to the end of a file. Let's add another
line to our text file using the `>>` operator.

    % echo "Using C/C++" >> ece4750-sec01.txt
    % cat ece4750-sec01.txt

You can use the `ls` command to list the filenames of the files you have
created.

    % ls

We can provide command line options to the `ls` command to modify the
command’s behavior. For example, we can use the `-1` (i.e., a dash
followed by the number one) command line option to list one file per
line, and we can we can use the `-l` (i.e., a dash followed by the letter
l) command line option to provide a longer listing with more information
about each file.

### Create, Change, and List Directories

Obviously, having all files in a single location would be hard to manage
effectively. We can use directories (also called folders) to logically
organize our files, just like one can use physical folders to organize
physical pieces of paper. The mechanism for organizing files and
directories is called the file system. When you first log in to an
`ecelinux` machine, you will be in your home directory. This is your own
private space on the server that you can use to work on the programming
assignments and store your files. You can use the `pwd` command to print
the directory in which you are currently working, which is known as the
current working directory.

    % pwd
    /home/netid

You should see output similar to what is shown above, but instead of
`netid` it should show your actual NetID. The pwd command shows a
directory path. A directory path is a list of nested directory names; it
describes a "path" to get to a specific file or directory. So the above
path indicates that there is a toplevel directory named home that
contains a directory named `netid`. This is the directory path to your
home directory. As an aside, notice that Linux uses a forward slash (`/`)
to separate directories, while Windows uses a back slash (`\`) for the
same purpose.

We can use the `mkdir` command to make new directories. The following
command will make a new directory named `ece4750` within your home
directory.

    % mkdir ece4750

We can use the `cd` command to change our current working directory. The
following command will change the current working directory to be the
newly created `ece4750` directory, before displaying the current working
directory with the pwd command.

    % cd ece4750
    % pwd
    /home/netid/ece4750

Use the `mkdir`, `cd`, and `pwd` commands to make another directory.

    % mkdir sec01
    % cd sec01
    % pwd
    /home/netid/ece4750/sec01

We sometimes say that `sec01` is a subdirectory or a child directory of
the `ece4750` directory. We might also say that the `ece4750` directory
is the parent directory of the `sec01` directory. Use the following
command to create a new file in this child directory.

    % cd /home/netid/ece4750/sec01
    % echo "Computer Architecture" > ece4750-sec01.txt
    % mkdir dirA
    % ls

You can use the `tree` command to visualize the directory layout and
where files are located:

    % cd ~/ece4750
    % tree

Note that the tilde character (`~`) is a shortcut which always refers to
your home directory. There are a few other very useful shortcuts. You can
use a single dot (`.`) to refer to the current working directory, and you
can use a double dot (`..`) to refer to the parent directory of the
current working directory.

    % cd ~/ece4750/sec01
    % cd ..
    % cd ..
    % pwd

### Copy, Move, and Remove Files and Directories

We can use the `cp` command to copy files. The first argument is the name
of the file you want to copy, and the second argument is the new name to
give to the copy. The following commands will make two copies of the
files we created in the previous section.

    % cd ~/ece4750/sec01
    % cp ece4750-sec01.txt ece4750-sec01-a.txt
    % cp ece4750-sec01.txt ece4750-sec01-b.txt
    % ls

Instead of copying we can also move a file with the `mv` command:

    % cd ~/ece4750/sec01
    % mv ece4750-sec01.txt ece4750-sec01-c.txt
    % ls

Finally, we can use the `rm` command to remove files.

    % cd ~/ece4750/sec01
    % ls
    % rm ece4750-sec01-a.txt

We have installed a simple program called `trash` which moves files you
wish to delete into a special subdirectory of your home directory located
at `${HOME}/tmp/trash`. The following commands create a file and then
deletes it using trash.

    % cd ${HOME}
    % echo "This file will be deleted." > testing.txt
    % trash testing.txt
    % echo "This file will also be deleted." > testing.txt
    % trash testing.txt
    % ls ${HOME}/tmp/trash

If you look in `${HOME}/tmp/trash` you will see subdirectories organized
by date. Look in the subdirectory with today's date and you should two
files corresponding to the two files you deleted. We highly recommend
always using the `trash` command instead of `rm` since this avoids
accidentally deleting your work.

### Text Editors

Students are free to use any text editor they want, although we recommend
students use VS Code which will learn about next week. VS Code is both a
remote access option _and_ a text editor. If you are using PowerShell,
you can use Micro to do basic text editing. You can start Micro like
this:

    % micro ece4750-sec01-b.txt

Micro is a lightweight text-based text editor. Use _Ctrl-G_ to learn more
about the keyboard shortcuts you can use to in Micro.

When you are finished go ahead and trash the `sec01` directory to keep
things tidy.

    % trash ~/ece4750/sec01

GitHub Account Setup
--------------------------------------------------------------------------

We recommend using GitHub for centralized repository hosting. You can check
to see if you have a GitHub account on `github.com` using this link:
`https://github.com/githubid` where `githubid` is your GitHub username on
`github.com`. If the above link does not work, then you do not have an
GitHub account on `github.com`. **NOTE: We are using `github.com` not the
Cornell hosted GitHub!** You will need to create one here:

 - <https://github.com/join>

Your NetID makes a great GitHub username on `github.com`. Be sure to use
your Cornell University email address.

Once your account is setup, please make sure you set your full name so we
can know who you are on GitHub. Please also consider uploading a profile
photo to GitHub; it makes it more fun to interact on GitHub if we all
know what each other look like. Go to the following page and enter your
first and last name in the Name field, and then consider uploading a
profile photo.

 - <https://github.com/settings/profile>
<!--
Once you have a GitHub ID, please fill out the following online so the
instructors know the mapping from NetID to GitHub ID:

 - <http://www.csl.cornell.edu/courses/ece4750/githubid>
-->
Before you can begin using GitHub, you need to create an SSH key pair on
an `ecelinux` machine and upload the corresponding SSH public key to
GitHub. GitHub uses these keys for authentication. You can follow these
instructions to set it up:
 
- <https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent>

After that, you can upload your new public key to GitHub:

 - <https://github.com/settings/ssh>

Click on _New SSH Key_, and then cut-and-paste the public key you
displayed using cat into the key textbox. Give the key the title
`ece4750-github`. Then click _Add SSH key_. To test things out try the
following command:

    % ssh -T git@github.com

You may see a warning about the authenticity of the host. Don’t worry,
this is supposed to happen the first time you access GitHub using your
new key. Just enter `yes`. The GitHub server should output some text
including your GitHub ID. Verify that the GitHub ID is correct, and then
you should be all set.

Git Version Control System
--------------------------------------------------------------------------

In this course, we will be using Git as our revision control and source
code management system. Git will enable us to adopt an agile development
methodology so you (and your group) can rapidly collaborate and iterate
on the design, verification, and evaluation of the assignments.

### Fork and Clone a Repo from GitHub

Fork'ing a repo means making a copy of that repo for your own local use.
We won't actually be forking repos for the programming assignments, but
it is an easy way for you to grab some example code for the discussion
section. Go to the example repo here:

 - <https://github.com/cornell-ece4750/ece4750-sec01-linux>

Click on the "Fork" button. Wait a few seconds and then visit the new
copy of this repo in your own person GitHub workspace:

 - `https://github.com/githubid/ece4750-sec01-linux`

Where `githubid` is your GitHubID. Now let's clone your new repo to the
`ecelinux` machine.

    % cd ${HOME}/ece4750
    % git clone git@github.com:githubid/ece4750-sec01-linux sec01
    % cd sec01
    % cat README.md

Where `githubid` is your GitHubID.
If you did _not_ set up GitHub correctly (willingly or not), you may
clone a repo directly from us via HTTPS, for example:

    % git clone https://github.com/cornell-ece4750/ece4750-sec01-linux.git sec01

The caveat of this is that you won't have anywhere to push your changes to. If
you want to store your labs for posterity, we do recommend setting up GitHub.

### Adding and Committing Files to Local Repository

Now let's add some new files to the repository. Use Micro to create a
file named `warm-colors.txt` with three warm colors:

    red
    orange
    yellow

Now use your favorite text editor again to create a file named
`cool-colors.txt` with three cool colors.

    blue
    green
    purple

Now let's add these files to our repository. First use the `git status`
command to check on the status of the repository.

    % cd ${HOME}/ece4750/sec01
    % git status

You should see that git has noticed two "untracked files" which are in
the working directory but are not currently being tracked by git. Let's
"add" these two files to git's "staging" area so it now knows it should
keep track of them:

    % cd ${HOME}/ece4750/sec01
    % git add warm-colors.txt
    % git add cool-colors.txt
    % git status

The status of these two files have changed. Git reports that both of the
new files are ready to be committed. Let's go ahead and commit these
changes into your local repository.

    % cd ${HOME}/ece4750/sec01
    % git commit -m "add some colors"

Let's now use `echo` and the `>>` command output redirection operator to
add `cyan` to the end of our `cool-colors.txt` file. We can then view our
changes from the command line using `cat`, and use `git status` and then
`git commit` to try and commit our changes.

    % cd ${HOME}/ece4750/sec01
    % echo "cyan" >> cool-colors.txt
    % cat cool-colors.txt
    % git status
    % git commit -m "add cyan"

Git will report that there are no changes added to the commit. So even
though Git is tracking `cool-colors.txt` and knows it has changed, we
still must explicitly add the files we want to commit. We recommend using
the `-a` command line option with the `git commit` command to tell Git to
add any file which has changed and was previously added to the repository
before doing the commit.

    % cd ${HOME}/ece4750/sec01
    % git status
    % git commit -a -m "add cyan"

Now the changes are committed. You can use `git log` to see a log of the
commits in your local repository.

    % cd ${HOME}/ece4750/sec01
    % git log

### Pushing Files to GitHub

Note that nothing has happened on GitHub yet. GitHub does _not_ know
anything about these local changes. We need to explicitly "push" our new
commits up to GitHub like this:

    % cd ${HOME}/ece4750/sec01
    % git push

Now go to the repository page using the GitHub web interface and verify
that there are two new files.

 - `https://github.com/githubid/ece4750-sec01-linux`

### Pulling Files from GitHub

Let's try making a change to this repository through the GitHub
web interface.

 - `https://github.com/githubid/ece4750-sec01-linux`

Click on _Add file_ and then _Create new file_. Name the file
`architectures.txt` and add a list of programming languages:

    IBM 360
    MIPS32
    RISC-V RV32IM
    Intel x86
    ARM v8

Now click _Commit new file_. Verify that there is a new file in the repo
using the GitHub web interface. Now let's "pull" these new changes from
GitHub to your local repo on `ecelinux`:

    % cd ${HOME}/ece4750/sec01
    % git pull
    % cat architectures.txt

This will be the basic GitHub workflow were students first use `clone` to
get a copy of their repository, use `commit -a` to commit their code to
the local repository, and then use `pull` and `push` to synchronize their
repository with the repository on GitHub.

To-Do On Your Own
--------------------------------------------------------------------------

If you have time, add `maroon` to the `warm-colors.txt` file you created
earlier using either Micro. Save the file and then view your
changes from the command line using `cat`. Then use `git status` and `git
commit -a` to add these changes to local repository, and then use `git
push` to push these changes up to GitHub. View the changes using the
GitHub web interface.

Then try editing a file using the GitHub web interface. Click on the
`warm-colors.txt` file and then click on the pencil in the right-hand
corner to edit this text file. Add another warm color. Click _Commit
changes_. Then pull these changes to the local repository on the
`ecelinux` server and verify that your new warm color is included.

For ECE 2400 Alumni (or Advanced Students)
--------------------------------------------------------------------------

For students that took ECE 2400, they will recognize this section as
being identical to the first section in ECE 2400. We are trying to make
sure all students are able to successfully log in to the `ecelinux`
servers, setup their GitHub account correctly, and understand the basic
Git workflow. ECE 2400 students probably already know all of this. They
should still confirm they can fork and clone the example GitHub repo and
then push/pull to this repo.

ECE 2400 students may want to experiment with cross-compiling C code
(like we wrote in ECE 2400) for the RISC-V instruction set architecture
and then running the resulting binary on a RISC-V instruction set
simulator as discussed below.

### Compile a simple C program for Intel x86

Let's compile the very first program you saw in ECE 2400. First make sure
we have a directory to work in:

    % mkdir -p ${HOME}/ece4750/sec01
    % cd ${HOME}/ece4750/sec01

Then use your favorite text editor to create a file named `avg-main.c`.

    #include <stdio.h>

    int avg( int x, int y )
    {
      int sum = x + y;
      return sum / 2;
    }

    int main()
    {
      int a = 10;
      int b = 20;
      int c = avg( a, b );
      printf( "average of %d and %d is %d\n", a, b, c );
      return  0;
    }

Recall how to compile this C program into an x86 binary and execute this
binary on the `ecelinux` server.

    % cd ${HOME}/ece4750/sec01
    % gcc -Wall -o avg-main avg-main.c
    % ./avg-main

### Cross-compile a simple C program for RISC-V RV32IM

In this course, we will be using the RISC-V instruction set architecture
instead of the x86 instruction set architecture. You can use a
_cross-compiler_ to compile a C program into a RISC-V binary like this:

    % cd ${HOME}/ece4750/sec01
    % riscv32-unknown-elf-gcc -O3 -o avg-main-riscv avg-main.c

Now let's take a look at the actual RISCV instructions using
`riscv32-objdump`:

    % riscv32-objdump avg-main-riscv

See if you can find the instructions that correspond to the `avg`
function. See if you can figure out how the C code maps to these RISCV
instructions. Use the TinyRV2 instruction set architecture manual located
here:

 - <https://www.csl.cornell.edu/courses/ece4750/handouts/ece4750-tinyrv-isa.txt>

Experiment with the following variation and look at the corresponding
RISCV instructions.

    unsigned int avg( unsigned int x, unsigned int y )
    {
      unsigned int sum = x + y;
      return sum / 2;
    }

Can you explain the difference from the original version of this code?

### Execute RISC-V instructions on a simulator

CS 3410 uses a neat RISC-V simulator which works in your browser:

 - <https://www.cs.cornell.edu/courses/cs3410/2019sp/riscv/interpreter>

Try copying the RISC-V instructions for just the `avg` function into this
RISC-V interpreter. Then execute instruction step-by-step and verify they
behave as expected.


