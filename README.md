Download Link: https://assignmentchef.com/product/solved-csc332-task3-exec-family-of-functions
<br>
This handout describes the <strong>exec</strong>​ family​ of functions, for executing a command. You can use these functions to make a child process execute a new program after it has been forked. The functions in this family differ in how you specify the arguments, but they all do the same thing. They are declared in the header file <strong>‘unistd.h’</strong>​ <strong>.</strong>​  <strong>execv (char *filename, char *const argv[])  </strong>

The <sup>execv </sup>​              function executes the file named by filename as a new process image. The ​         <sup>argv</sup>​       argument is an array of null-terminated strings that is used to provide a value for the argv argument to the main function of the program to be executed. The last element of this array must be a null pointer.

<h1>execvp (char *filename, char *const argv[])</h1>

The <sup>execvp </sup>​            function is similar to ​      <sup>execv</sup>​    ​, except that it searches the directories listed in the PATH environment variable to find the full file name of a file from filename if filename does not contain a slash. This function is useful for executing system utility programs, because it looks for them in the places that the user has chosen. <strong>Shells use </strong>​      <sup>execvp </sup>​                <strong>to run the commands </strong>​ that users type.​   <strong>execl (char *filename, const char *arg0, …)  </strong>

This is similar to <sup>execv</sup>​        , but the ​           <sup>argv </sup>​     strings are specified individually instead of as an array. A null​    pointer must be passed as the last such argument.

<h1>execlp (char *filename, const char *arg0, …)</h1>

This function is like <sup>execl</sup>​   , except that it performs the same file name searching as the ​      <sup>execvp</sup>​ function.

<strong>Example 1: </strong>Using execv(…) command​

Note: This version will not search the path, so the full name of the executable file must be given. Parameters to main() are passed in a single array of character pointers.

#include &lt;stdio.h&gt; #include &lt;unistd.h&gt;

int main (int argc, char *argv[]) {

execv (“/bin/echo”, &amp;argv[0]); printf (“EXECV Failed
”);

/* The above line will be printed only on error and not otherwise */

}




Sample Output

$ gcc execv_ex1.c -o execv_ex1 $ ./execv_ex1 Hello World!

Hello World!

<strong>Example 2: </strong>Using execvp(…) command​

Note: This version searches the path, so the full name of the executable need not be given. Pa- rameters to main() are passed in a single array of character pointers. This is the form used inside a shell!

#include &lt;stdio.h&gt; #include &lt;unistd.h&gt;

int main (int argc, char *argv[]) {     execvp (“echo”, &amp;argv[0]); printf (“EXECVP Failed
”);

/* The above line will be printed only on error and not otherwise */  }

Sample Output

$ gcc execvp_ex2.c -o execvp_ex2  $ ./execvp_ex2 Hello World!

Hello World!

<h1>Instructions</h1>

<ul>

 <li>Read man page of ​ <sup>exec </sup>​     system call: ​      <sup>man exec</sup>​            , to know the syntax of all the four variants in detail​</li>

 <li>Compile and execute the examples 1 and 2 to get a feel on how these system call works before you​ start working on task 3.</li>

</ul>










<strong>TASK </strong>

<strong>3 </strong>

<strong>DUE: </strong>​<strong>March</strong>​<strong>. </strong>​<strong>5</strong>​<strong>, 2020, 11:59 PM – 25 Points  </strong>

<h1>Part 1</h1>

Write a program where a child is created to execute command that tells you the date and time in

Unix. Use ​execl(…). Note: you need to specify the full path of the file name that gives you date and​          time information. Announce the successful forking of child process by displaying its PID.

<h1>Part 2</h1>

Write a program where a child is created to execute a command that shows all files (including hidden files) in a directory with information such as permissions, owner, size, and when last modified. Use ​execvp(…).​ Announce the successful forking of child process by displaying its PID.

<h1>Part 3</h1>

<strong>[Step 1] Process_P1.c:  </strong>

Create two files namely, ​destination1.txt and ​  ​destination2.txt with read, write and execute​     permissions.

<strong>[Step 2] Process_P2.c:  </strong>

Copy the contents of ​source.txt<sup>  </sup>​ into <sup>​     </sup>​destination1.txt and ​    ​destination2.txt as per the following​     procedure:

<ol>

 <li>Read the next 100 characters from ​source.txt​, and write to ​destination1.txt</li>

</ol>

2​ . Then the next 50 characters are read from ​source.txt and written in ​ ​destination2.txt.

Once you’re done with the successful creation of executables for the above two steps do the following:

Write a C program and call it ​Parent_Process.c. Execute the files as per the following procedure using​     execv system call. Use ​           ​sleep system calls to introduce delays.​

<h1>[Step 3]</h1>

Fork a child process, say ​Child 1 and execute ​   ​Process_P1. This will create two destination files​           according to Step 1. <strong> </strong>

<h1>[Step 4]</h1>

After ​Child 1 finishes its execution, fork another child process, say ​         ​Child 2 and execute ​    ​Process_P2 that accomplishes the procedure described in Step 2.