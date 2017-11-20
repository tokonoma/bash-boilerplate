SCSSMAPMAKER
================

A simple shell script that takes a SCSS file of variables and creates a map of name and variable pairings.

Based on the shell script boilerplate [created by alphabetum](https://github.com/alphabetum/bash-boilerplate).



## Basics

This script takes a SCSS file that (ideally) has nothing in it but variable definitions and creates a new file that contains a SCSS map of those variables, pairing the variable's name as a string and the variable itself.

This example input file:

```scss
$color-black: #292E31;
$color-gray: #777C7F;
$color-white: #FFFFFF;
```

Would yield this output file:

```scss
$color-map: (
	"color-black" : $color-black,
	"color-gray" : $color-gray,
	"color-white" : $color-white
);
```

This script is specifically designed with sass loops in mind. By automating the process, changes to variable lists do not require manual tracking and modification of the maps that reference them - just run the script, then compile your SCSS.

An example based on the map above:

```scss
@each $color-name, $color-variable in $color-map{
	.text-#{$color-name} {
		color: $color-variable;
	}
}

//yields
.text-color-black{
  color: $color-black;
}
.text-color-gray{
  color: $color-gray;
}
.text-color-white{
  color: $color-white;
}
```

Imagine if this list had 50 colors instead of 3. And imagine you needed to add 5 new colors and remove 10 colors. Instead of manually tracking changes between the list of variables and the map used for looping, all you have to do is change your list of variables then run the script to produce a new map with all the variables paired with a label.



## Running the Script

##### Input & Output

This script requires at least one argument - the input scss file with the list of variables. An additional argument is optional and will serve as the name of the output file. If no output file name is provided, the script will add `map-` to the front of the input file's name.

```
scssmapmaker input.scss output.scss
```

This command will look for `input.scss` and create a new file called `output.scss`

```
scssmapmaker input.scss
```

This command will look for `input.scss` and will produce a file called `map-input.scss`



##### Run Locally

You can run this locally by placing the script in the directory where your input scss file resides.

```
bash scssmapmaker input.scss output.scss
```



##### Global Install

To install globally, first place this in a directory that makes sense for accessing globally, for example `home/Scripts/scssmapmaker` .

Next, open your `bash_profile` with your choice of text editor:

```
nano ~/.bash_profile
```

and add the following line:

```
export PATH=~/Scripts/scssmapmaker:$PATH
```

replacing ` ~/Scripts/scssmapmaker/` with the path for wherever you put the script. If this line or something like it already exists, just add your path to the list. Paths are separated by `:` like so:

```
export PATH=path/im/adding:one/more:$PATH
//or
export PATH=$PATH:this/ones/at/the/end:heres/another
```

Making sure that `$PATH` is somewhere in there… 

Finally, run:

```
source ~/.bash_profile
```

And you should be good to go.

If the script won't run, make sure the script is executable by navigating to the directory the script is in and running:

```
chmod +x scssmapmaker
```



---

Original Work Copyright (c) 2015 William Melody • hi@williammelody.com

Modified Work Copyright (c) 2017 Timothy Reeder