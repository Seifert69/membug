# membug
Memory debugging for C / C++

I've used this code to find a super difficult memory bug. Thinking it will be useful to others.

I wholeheartedly recommend first using Valgrind. If you can't find your issues with Valgrind,
then this code is a path forward from there.

I'll improve documentation later

To use, add membug.cpp to your project and make sure you include membug.h in ALL of your files. 
Recompile your entire project with the MEMORY_DEBUG flag set.

You will need to make the following code changes:

For C code - no changes are needed. Macros override malloc, free, calloc, realloc.

You can sprinkle 

void membug_verify_reg(void *ptr);

at any point in your code to check the validity of an allocated memory chunk in C.

For C++

Add "EMPLACE(class)" to all C++ classes you wish to include in memory debugging, like this:

fptr->next = new EMPLACE(unit_fptr) unit_fptr;

Note that EMPLACE will be ignored when compiling without the MEMORY_DEBUG flag.

Correspondingly, use DELETE(unit_fptr, unit->fptr); to delete rather than delete unit->fptr;

Use void membug_verify_class(void *ptr) to verify C++ memory allocated blocks.

use void membug_verify(void *ptr) to validate a block when you don't know if it's allocated from C or C++

