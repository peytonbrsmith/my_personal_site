---
title: "📚 C Static and Dynamic Libraries"
description: "A blog about Static and Dynamic libraries in C."
lead: "The Dynamics of Libraries in C"
date: 2020-12-14
lastmod: 2021-11-06
draft: false
weight: 50
images: []
contributors: ["Peyton Smith"]
---




When dealing with c programs you'll probably come across two kinds of libraries: **Static** and **Dynamic**.

### _Why_ would you use libraries?

When working on a team, or even by yourself, the size and scope of a project can exponentially increase over time. This is especially true in software development as the length, complexity, and quantity of functions and programs continue to increase throughout a project's lifetime. Libraries help mitigate the issues and annoyances associated with the movement of large and/or bountiful functions. They group and contain existing functions into a single archive that can be used elsewhere or by someone else without having to be messy or send numerous files.

### How do Libraries work?

For now we'll go over the use, workings, and creation of only **Static Libraries.**

Static Libraries act as an archive of the object files generated from c files. You can obtain these files by using the **-c** option when compiling c files with the **gcc** command (GNU Compiler Collection) as seen in the example below:

	gcc -Wall -pedantic -Werror -Wextra -c *.c

Once the archive has been created (to be discussed below) all of the functions included are given symbols and addresses in an organized **index.** This index occasionally needs to be updated (or created) using the command **ranlib** with the name of the archive file to be indexed preceding said command as shown here:

	ranlib archive.a

	You can list the contents of an archive using **nm:**

	nm <archive.a>

	and you'll see a list of objects like:

	** OUTPUT **

	0-isupper.o:
	0000000000000000 T _isupper

An up-to-date index can be linked with the main function of a program during compilation and will be integrated before creating the executable.

### How do you create Static Libraries?

Static Libraries are archive files and can be created with the program **ar** (archive). It can also be used to update/modify existing archives, list the archive contents, etc.

The command can be run successfully by following the prototype:

	ar -rc lib<YourArchiveName>.a <.o file(s)>


The options **-rc** mean that existing functions are updated/replaced (**r**) and if the archive does not already exist, create it (**c**).

The name of your archive needs to be prefixed with lib (though this is omitted when linking with the main program) and end with the extension .a (for archive and also is omitted during linking).

### _How_ do you use Static Libraries?

Once you've created the archive full of all the function objects that you want, you can link it to your main program during its compilation. For an example, when using GCC:

	gcc main.c -L -l<archivename without lib or .a> -o <name of executable>

The **-L** option tells the compiler to look for library files, the **-l** option specifies the library files to be _linked_, and the **-o** option specifies the name of the outputted executable.

You should now have an executable that has successfully linked your main program with the pre-generated object files of your other programs!

Unless you are after raw speed, Static Libraries are just not as friendly to work with because they have one major disadvantage. After creating a static library, any updates to the code within the library remain unavailable to your program until you recompile the program with the updated library. This is okay if you are sharing/moving around a library of solid code that is not going to be updated often, but wouldn't that get extremely tiresome if you had to constantly update your library and re-compile your program? This is where Dynamic Libraries come in handy, and to start creating one on a Linux machine, you will want to use a variation of this command:

	gcc <filenames of your c files> -c -fPIC

	using *.c in place of any filenames with tell BASH to
	expand that single "*.c" argument into as many arguments
	as there are files that end in ".c" in the current
	working directory.

GCC, or the GNU Compiler Collection, is our preferred C compiler here at Holberton School and using the _-c_ option I can specify to only have the object files for the source code generated, and to stop before any linking or further stage of compilation. With the addition of the _-fPIC_ flag I can specify that this code will be _Position Independent Code,_ which means that the machine code generated will not be tied to any particular address in memory, allowing it to be shared between programs and processes much more easily and without having to have multiple copies of the same code taking up extra memory/space. With these PIC object files we can finally create the library using:

	gcc <you object files> -shared -o <lib+nameoflibrary>.so

When GCC encounters object files it knows to compile them into a library, but the type of library will need to be specified with a flag. In our case we want to use the -shared flag to tell the compiler that we want to have created a _Dynamic_ library.

Now you have the library, _woo-hoo!_ You can check its contents (symbols of our object code) using:

	nm <library file>

	or its shared library dependencies using:

	ldd <library file>

	Luckily, linking this library with your C program is the exact same as with Static Libraries! Use this command:

	gcc <your c files> -L -l <archivename without lib or .a> -o <nameofexecutable>

The **-L** option tells the compiler to look for library files within your library folders. The folders GCC looks for library files in can be specified in the environment variable _LD_LIBRARY_PATH_. The **-l** option specifies the library files to be _linked_, and the **-o** option specifies the name of the outputted executable.

Ta-daaaa! You should now have an executable that has been linked with your **DYNAMIC** library! And guess what? If you update that library... you won't have to use _ranlib_ to re-index it, or recompile!
