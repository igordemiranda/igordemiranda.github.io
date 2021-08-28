---
layout: post
title:  "Fun with compilers!"
categories: miscellaneous
---

Found an interesting piece by @jckarter [on Twitter](https://twitter.com/jckarter/status/1428072308351016969?s=20).

Consider the following incorrect implementation of `isEven` in C++:

```
bool isEven(int x) {
    switch (x) {
        case 0: return true;
        case 1: return false;
        case 2: return true;
        case 3: return false;

        default: return isEven(x); // infinite loop
    }
}
```

In a funny coincidence, compiling this with the clang compiler with optimization flag `-O2` turns out to generate a correct and efficient `isEven(int)` solution!

Here is what the compiled output looks like:

```
isEven(int): # @isEven(int)
  test dil, 1
  sete al
  ret
```

In summary:
- `dil` is the pseudo-register for the 8 least significant bits of the first function argument (stored in register `rdi`)
- `test` performs a bitwise AND operation between `dil` and 1, and sets ZF (zero flag) if the result is 0, which is an efficient way to test for even numbers
- `sete` sets `al` according to `ZF`
- `al` is the pseudo-register for the 8 least significant bits of register `rax`, which is used to store the function return value
- The infinite loop caused by calling isEven(x) recursively is thrown away because it's [undefined behavior](https://en.wikipedia.org/wiki/Undefined_behavior#Examples_in_C_and_C++).

Moreover, if you were to remove any of the `case` statements in the C++ code, you wouldn't get the correct `isEven` function compiled. Each one there is meaningfully influencing the compiler towards the right output!

References:
- [Compiler explorer](https://gcc.godbolt.org/#g:!((g:!((g:!((g:!((h:codeEditor,i:(filename:'1',fontScale:14,fontUsePx:'0',j:1,lang:c%2B%2B,selection:(endColumn:2,endLineNumber:10,positionColumn:2,positionLineNumber:10,selectionStartColumn:2,selectionStartLineNumber:10,startColumn:2,startLineNumber:10),source:'bool+isEven(int+x)+%7B%0A++++switch+(x)+%7B%0A++++++++case+0:+return+true%3B%0A++++++++case+1:+return+false%3B%0A++++++++case+2:+return+true%3B%0A++++++++case+3:+return+false%3B%0A%0A++++++++default:+return+isEven(x)%3B%0A++++%7D%0A%7D'),l:'5',n:'0',o:'C%2B%2B+source+%231',t:'0')),k:50.481284988327246,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:compiler,i:(compiler:clang_trunk,filters:(b:'0',binary:'1',commentOnly:'0',demangle:'0',directives:'0',execute:'1',intel:'0',libraryCode:'0',trim:'0'),flagsViewOpen:'1',fontScale:14,fontUsePx:'0',j:1,lang:c%2B%2B,libs:!(),options:'-O2',selection:(endColumn:6,endLineNumber:4,positionColumn:6,positionLineNumber:4,selectionStartColumn:6,selectionStartLineNumber:4,startColumn:6,startLineNumber:4),source:1,tree:'1'),l:'5',n:'0',o:'x86-64+clang+(trunk)+(C%2B%2B,+Editor+%231,+Compiler+%231)',t:'0')),k:49.51871501167276,l:'4',n:'0',o:'',s:0,t:'0')),l:'2',m:76.18048268625394,n:'0',o:'',t:'0'),(g:!((h:executor,i:(argsPanelShown:'1',compilationPanelShown:'0',compiler:g112,compilerOutShown:'0',execArgs:'',execStdin:'',fontScale:14,fontUsePx:'0',j:1,lang:c%2B%2B,libs:!(),options:'',source:1,stdinPanelShown:'1',tree:'1',wrap:'1'),l:'5',n:'0',o:'Executor+x86-64+gcc+11.2+(C%2B%2B,Editor+%231)',t:'0')),header:(),l:'4',m:23.819517313746065,n:'0',o:'',s:0,t:'0')),l:'3',n:'0',o:'',t:'0')),version:4)
- [Recap of x86-64](https://web.stanford.edu/class/cs107/guide/x86-64.html)