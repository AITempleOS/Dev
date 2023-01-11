# AITempleOS V 1.0.0
The Official AITempleOS Development Git


Here's an example of what the Goal is so far for AITempleOS could look like:

**Version 1.0.0**

First, we will start by creating the basic structure of our operating system. We will be using the ZealOS kernel as a base and modifying it to include our new language, Holy Lua.

To begin, we will need to install the necessary tools and dependencies for building the kernel. This includes GCC, Make, and the GNU Binutils. Once these are installed, we will download the ZealOS source code and begin making our modifications.

Next, we will add support for Holy Lua by integrating the Lua interpreter into the kernel. This will allow us to run Lua scripts directly on the operating system. To do this, we will need to add the Lua library files to the kernel and create a new system call for running Lua scripts.

Once the kernel is modified, we will then create a new shell for the operating system that will allow us to run Holy Lua scripts. This shell will include commands for running, editing, and debugging Lua scripts.

Now that we have the basic structure of the operating system in place, let's take a look at an example script. In this example, we will create a simple script that prints "Hello, world!" to the screen.

Here is the code for the script:

Copy code

`print("Hello, world!")`

To run the script, we will use the command "runscript [script name]". In this case, the command would be "runscript helloworld.lua".

That's it! With these basic steps, we have created a new operating system that incorporates Holy Lua and allows for the execution of Lua scripts. Of course, there are many more advanced features and optimizations that can be added, but this should give you a good starting point.

To add support for Holy Lua by integrating the Lua interpreter into the kernel, we will need to follow these steps:

1. Download the Lua source code and extract it to a directory on your computer.
  
2. Modify the kernel's build system to include the Lua source code during the compilation process. This will typically involve adding the Lua source code directory to the list of include directories and adding the Lua library files to the list of libraries to be linked with the kernel.
  
3. Create a new system call for running Lua scripts. This can be done by adding a new function to the kernel's syscall table and providing a wrapper function that calls the Lua interpreter to execute the script.
  
4. Test the Lua integration by creating a simple Lua script and running it on the operating system.
  

Here is a more specific example:

1. Download the Lua 5.3.5 source code from the official website and extract it to a directory called "lua-5.3.5" in your kernel source directory.
  
2. In the kernel's Makefile, add the path to the Lua header files to the list of include directories and add "-llua" to the list of libraries to be linked. The Makefile should now look something like this:
  

Copy code

`INCLUDE_DIRS += -I./lua-5.3.5/src LIBS += -llua`

3. In the kernel's syscall.c file, create a new function called "sys_run_lua_script" that takes the path to the Lua script as a parameter. This function will be used to run the Lua script.

Copy code

`int sys_run_lua_script(char *path) { lua_State *L = luaL_newstate(); luaL_openlibs(L); if (luaL_dofile(L, path) != 0) { printk(KERN_ERR "Error running Lua script: %s\n", lua_tostring(L, -1)); lua_pop(L, 1); return -1; } lua_close(L); return 0; }`

4. In the kernel's syscall_table, register the new system call "sys_run_lua_script" so that it can be called from user space.

Copy code

`[SYS_RUN_LUA_SCRIPT] = sys_run_lua_script,`

5.Finally, test the Lua integration by creating a simple Lua script called "helloworld.lua" that contains the following code:

Copy code

`print("Hello, world!")`

and use the "runscript" command to run it on the operating system.

Copy code

`runscript helloworld.lua`

It should print out "Hello, world!" in the kernel log.

Keep in mind that this is just a basic example, and there are many different ways to integrate Lua into the kernel depending on your specific use case.

##Disclamer this is currently a working project for a game
