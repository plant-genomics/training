## Nextflow

### The basics

* Install nextflow
* Write a script to run a workflow  



Nextflow documentation is good - prob delete this below




### A nextflow script  

Make a file called weather.nf
```
nano weather.nf
```

Add this to the script:

```
#!/usr/bin
process weather {    
  echo true         
  """
  echo "stormy"      
  """
}
```

* <ss>process</ss> is a step in the workflow
* <ss>echo "stormy"</ss> is the code block
* <ss>echo true</ss> allows it to print to screen
* the process is enclosed in these: <ss>{     }</ss>

Run the workflow:
```
nextflow run weather.nf
```

The screen will show:
```
N E X T F L O W  ~  version 19.01.0
Launching `weather.nf` [stupefied_legentil] - revision: eccaf7e744
[warm up] executor > local
[4a/bb33c4] Submitted process > weather
stormy
```
* Our output is on the last line
* Although we printed the output to the screen, nextflow has also saved the output in a default <fn>work</fn> directory
* See <ss>[4a/bb33c4]</ss> next to <ss>Submitted process</ss> - this is the name of the exectued process called "weather". This is also a folder of output in your <fn>work</fn> directory.
* `cd 4a/bb33c4` (replace with your process number)
* `ls -la` to see hidden files (these start with a . )
* `less .command.out` to look at output

### Inputs, outputs, channels

Example script:

```
#!/usr/bin/env nextflow

//env is a command that looks in the user's path for nextflow
//this will use whatever version of nextflow is first in the path


//input file
params.in = "reads.fasta"

//a channel called "sequences"
sequences = file(params.in)

process split {

input:
file 'zebra.fa' from sequences

output:
file 'part_zeb.fa' into records
//"records" will be a new channel


"""
head -10 zebra.fa > part_zeb.fa
//note any programs in here need to be installed in the environment
"""
}


process show {

input:
file x from records
//"records" is a channel

output:
stdout result

"""
less  $x
//refer to variable x
"""

}

result.subscribe { println it }
```









### Links

* [https://nf-co.re/nextflow_tutorial](https://nf-co.re/nextflow_tutorial)
* [https://github.com/nextflow-io/awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow)
