# fofo
Formatted Ordered FOrest

## Overview

The fofo is one of markup languages inspired by YAML. Compared to YAML, fofo's grammar is simpler and the format must be defined and  outputs are restricted.

The fofo is invennted in order to descript settings of deep learning architecture.

But the fofo can be used in other domains.

## Feature

* Formatted:
  all contents of fofo is formatted.
* Output:
  fofo's output is only one list of list.
* Extension:
  .fofo

## Example

The fofo file is described like below,

```
# this is comment
HDF5Layer
    name = <string>
    dimensions = <int> ...
    source
        file = <string>
        name = <string>
        
    name = input_data
    dimensions = 784
    source
        file = /path/to/mnist.h5
        name = input

    name = output_data
    dimensions = 1
    source
        file = /path/to/mnist.h5
        name = output

ReshapeLayer
    name = <string>
    dimensions = <int> ...
    
    name = reshape1
    dimensions = 1 28 28

ConvolutionalLayer
    name = <string>
    dimensions = <int> ...
    steps = <int = 1> ...
    
    name = conv1
    dimensions = 8 24 24
    
    name = conv2
    dimensions = 8 8 8

MaxPoolLayer
    name = <string>
    dimensions = <int> ...
    
    name = mp1
    dimensions = 4 12 12
    
    name = mp2
    dimensions = 4 4 4

DropOutLayer
    name = <string>
    drop_rate = <float = 0.5>
    
    name = drop1
    drop_rate = 0.5

LogisticRegressionLayer
    name = <string>
    dimensions = <int>
    
    name = logreg1
    dimensions = 10

Network
    arc = <string> <string>
    
    arc = input_data reshape1
    arc = reshape1 conv1
    arc = conv1 mp1
    arc = mp1 conv2
    arc = conv2 mp2
    arc = mp2 drop1
    arc = drop1 logreg1
    arc = output_data logreg1
```

Parsed the fofo file, you can access each contents like below, 

```c++
/* UNDER COSTRUCTION */
#include "fofo/fofo.h"

int main()
{
    const fofo::String fofo_file("/path/to/file.fofo");
    fofo::Parser parser(fofo_file);
    parser.parse();
    for (auto item: parser.items())
    {
        std::cout << item << std::endl;
    }
}

```
