# NOP loop

Credit to Brendan Gregg's bechamrking post http://www.brendangregg.com/blog/2014-04-26/the-noploop-cpu-benchmark.html

Modified ``noploop.s`` can be compiled `gcc -o noploop noploop.s` and run for benchamrking

This loop is running 10000000 x 2000 of `noop` instructions on the CPU and you need to watch for a wall clock time.
For example 
```
$ sudo perf stat ./noploop

 Performance counter stats for './noploop':

       2092.079115      task-clock (msec)         #    1.000 CPUs utilized
                 2      context-switches          #    0.001 K/sec
                 0      cpu-migrations            #    0.000 K/sec
                39      page-faults               #    0.019 K/sec
     5,024,248,023      cycles                    #    2.402 GHz
    20,042,764,139      instructions              #    3.99  insn per cycle
        10,486,492      branches                  #    5.012 M/sec
            21,441      branch-misses             #    0.20% of all branches

       2.092597245 seconds time elapsed
```
In this `((10000000 x 2000)/  2.092597245)/1000000` = 9557.5 MHz as a processor speed. By looking at `insn per cycle` it looks like 4-Wide multi scalar processor so actual speed will be  `9557.5/3.99 = 2.395 GHz`.


Here 1 MHz == 1000000 Hz.


