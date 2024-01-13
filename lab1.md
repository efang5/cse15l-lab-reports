# Lab Report 1
## cd no argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.09.53%20PM.png?raw=true)
The working directory was user@sahara.

There is no output as cd only changes the directory and as we did not give what it was supposed to change the directory to the next directory was unchanged.

There is no error.
## cd directory argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.10.55%20PM.png?raw=true)
The working directory was user@sahara.

There is no output as cd only changes the directory and the directory for the next line was changed to user@sahara lecture1 as we told it to change the directory to lecture1.

There is no error.
## cd file argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%203.08.19%20PM.png?raw=true)
The working directory was user@sahara lecture1.

There is an output because an error occured. The error occured becuase the arguement was not a directory.

## ls no argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.29.51%20PM.png?raw=true)
The working directory was user@sahara.

lecture1 was the output that was the only thing in the working directory.

There is no error.
## ls directory argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.30.01%20PM.png?raw=true)
The working directory was user@sahara.

Hello.class  Hello.java  messages  README was the output because they are what were within lecture1.

There is no error.
## ls file argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.32.34%20PM.png?raw=true)
The working directory was user@sahara.

lecture1/messages/en-us.txt is the output as we gave is a file not a directory so it could not give us what paths are found under that directory.

There is no error.
## cat no argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.33.35%20PM.png?raw=true)
The working directory was user@sahara.

There is no output as we did not give it any inputs to combine so it caused an error where it got stuck in an endless loop.

## cat directory argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.35.35%20PM.png?raw=true)
The working directory was user@sahara.

It throws the error we gave it a directory because cat combines what we give it by grabbing what is at that location files have info to use at the location, directories don't.

## cat file argument
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-10%20at%201.35.22%20PM.png?raw=true)
The working directory was user@sahara.

Hello World! is the output as that is the text at the location of the file we told cat to access.

There is no error.
