SL(1): Cure your bad habit of mistyping
=======================================

SL (Steam Locomotive) runs across your terminal when you type "sl" as
you meant to type "ls". It's just a joke command, and not useful at
all.

Copyright 1993,1998,2014 Toyoda Masashi (mtoyoda@acm.org)

![](demo.gif)

### Pre-requisites
This distribution requires the following pre-reqs to be installed
assuming a Debian system.

```bash
# apt install build-essential
# apt-get install libncurses5 libncurses5-dev
# apt-get install ghostscript
```

### Adding a new vehicle
Adding a new vehicle involves a couple of steps:

##### Find an ASCII art 
Find a new vehicle ASCII art from resources such as https://www.asciiart.eu/ or create one yourself.

##### Add vehicle to header file
Adding a new train as strings involves dividing the ASII art into three string categories. The first is the body of the vehicle. The second is the "wheel" or part that you want to optionally animate. The third is a string filled with spaces that is used to erase (for example with the -F option). See for example, CC00xxx and C01xxx strings in sl.h for vehicles that have been added.

Once you have added the string in sl.h, its time to move to the code:
1. Create a function of the form `add_CXX(int x)`. Look for example functions such as `add_C00(int x)`. This function  is essentially the loop that the program goes through. The beginning of this function is a `static char *cXX[][]` array with the rows equal to the number of patterns/wheels and the columns equal to the height + 1. The rest of the code is pretty much a template that is easy to understand from previous examples.

2. Increase the value of `NUM_VEHICLES` by 1.

3. Add `add_CXX()` to the list of function pointers in `init_slfuncs()`. For example: `ptr_sl[5] = &add_C02;` where now there are 5 vehicles.

4. Update the man pages `sl.1`

#### Tips
- You can change the `usleep()` value to a lower value so that you do not have to suffer with the delays when testing!
- Makefile has been updated with a `make debug` target.

