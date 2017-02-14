# The Dynamic Cuckoo Filter

## Overview
The Dynamic Cuckoo Filter (DCF) is an efficient approximate membership test data structure. Simarlar with the classic Bloom filter, it aims at quickly determining whether or not an item belongs to a given dataset with an acceptable error. Different from Bloom filter and its variants, DCF is especially designed for highly dynamic dataset and support extending and reducing its capacity by adding and removing building blocks. The advantages of DCF is as follow

* the DCF design is the first to achieve both reliable item deletion and flexibly extending/reducing for approximate set representation and membership testing
* DCF outperforms the state-of-the-art DBF design in terms of the capability of reliable item deletion
* A DCF reduces the required memory space of the DBF by 75% as well as improving the speeds of inserting and membership testing by 50% and 80%, respectively.


## API
Generate DCF according to the expected maximum item number, expected false positive rate

```c++
DynamicCuckooFilter* dcf = new DynamicCuckooFilter(config.item_num, config.exp_FPR);
```

The expected building block number of DCF is set to 8 by default and can also be modified as follows

```c++
DynamicCuckooFilter* dcf = new DynamicCuckooFilter(config.item_num, config.exp_FPR, config.exp_BBN);
```


Four operations of DCF: Insert, Query, Delete and Compact

```c++
dcf->insertItem(item) // insert item ,item is a char* format
dcf->queryItem(item)  //query item
dcf->deleteItem(item) //delete item
dcf->compact() //compact DCF
```

## How to use?
### OpenSSL libiary
Our implementation of DCF can be run in a Linux with OpenSSL libiary. See more details in https://www.openssl.org.
### Build and run the example:

```txt
cd src/
make test
./test
```


### Configurations and Results
Configurations including false pisitive, item number and dataset path can be costomized in "configuration/config.txt". Change the value after the symbol "=" ONLY!!!

```txt
false positive = 0.02
item number = 1000000
input file path = input/input2.txt
```

Results are show in "output/results.txt", including false positive, fingerprint size, building block number, operation time consumed and etc.

```txt
       item_num        exp_FPR     actual_FPR     actual_BBN   F_size(bits) space_cost(MB)      I_time(s)      Q_time(s)      D_time(s)    C_rate
        1000000           0.02       0.009292              9             12        1.76947       0.784629        1.05502        1.29057         1
```


## Author and Copyright

DCF is developed in Big Data Technology and System Lab, Services Computing Technology and System Lab, School of Computer Science and Technology, Huazhong University of Science and Technology Wuhan, China by Liangyi Liao (liaoliangyi@hust.edu.cn), Hanhua Chen (chen@hust.edu.cn), Hai Jin (hjin@hust.edu.cn)

Copyright (C) 2017, [STCS & CGCL](http://grid.hust.edu.cn/) and [Huazhong University of Science and Technology](http://www.hust.edu.cn).


