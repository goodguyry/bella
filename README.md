Bella
===================

A Python script to take the redundancy out of Sass. Contributions welcomed and appreciated.

## Installation

#### Using Git

Clone the repo into the directory of your chosing and then ```cd``` into the project's root.

```bash
git clone https://github.com/goodguyry/bella.git && cd bella && source setup
```

#### Git-free

Download the files into the directory of your chosing.

```bash
curl -#L https://github.com/goodguyry/bella/tarball/master | tar -xzv --strip-components 1 --exclude={README.md,LICENSE} && source setup
```

#### Setup Options

Alternatively, you can run ```./setup``` from within the project root to set the files into place. There are three options available:

<table>
  <tr>
    <td><code>-h</code>, <code>--help</code></td>
    <td>Prints usage information</td>
  </tr>
  <tr>
    <td><code>--dev-mode</code></td>
    <td>Symlink files in place (default is copy)</td>
  </tr>
  <tr>
    <td><code>--no-global</code></td>
    <td>Supress copying/syncing the example global file</td>
  </tr>
</table>

Only **docs/bella\_global** and **bella** are copied/synced; **bella\_global** is copied to your home folder a hidden file and **bella** is copied to ~./bin.

### Use

Once in **~/.bin**, Bella can be run from the root of your site by typing ```bella```, or with the following optional arguments:

```python
bella -i <inputfile> -o <outputfile> -e <environment> -s <style>
```

- ```inputfile``` is the file you want Sass to watch.
- ```outputfile``` is the filename you want Sass to give the processed (CSS) file.
- Using ```environment``` is a quick way to switch away from your default environment
- ```style``` is one of the Sass style options

Any command line arguments override local settings, which in turn override any global settings. If you've got your configuration files set right, you should only need the options when switching environments.

Example: ```bella -e deploy```

Example files included in this repo:

1. **[bella_global](https://github.com/goodguyry/bella/blob/master/bella_global):**
This file is copied to your home folder **.bin/** directory during setup, or created manually if you chose not to use the example file. This is a great place to define your environment settings, as those usually won't change from project to project. See [bella_global](https://github.com/goodguyry/bella/blob/master/bella_global) for more.
2. **[bella.congif](https://github.com/goodguyry/bella/blob/master/bella.config):**
Project-specific settings to override the global defaults. This file must be in your project root.

### Configuration files

The configuration files (bella_global and bella.config) are python dictionary files.

```python
# From bella_global

{

  'defaults': {
    'environment': 'develop',
    'precision': 4,
    'watchFile': 'core',
    'processed-file': 'core',
    'addMinToFilename': True,
    'addMaxToFilename': True
  },

  'develop': {
    'style': 'expanded',
    'lineNumbers': True
  },

  'deploy': {
    'style': 'compressed',
    'lineNumbers': False
  }

}
```

```python
# From bella.config
{

  "paths": {
    "cssPath":"_/css/",
    "sassPath": "_/sass/"
  }

}

```

**Bella-specific settings**


```environment``` is the default environment; the environment can be either _develop_ or _deploy_.

```watchFile``` is the file you want Sass to watch; ```processed-file``` is the filename you want Sass to give the processed (CSS) file. If no _processed-file_ is set, the processed file with be named that same as the watchFile.

```addMinToFilename``` and ```addMaxToFilename``` will add _min_ or _max_ (respectively) to the processed CSS file's name; _max_ when not compressed, _min_ when compressed.

```paths``` are the paths to the Sass and CSS files.

**Sass-specific settings** ([from the Sass reference](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html))

```precision``` sets the number of digits of precision. For example, if this is 3, 3.1415926 will be printed as 3.142.

```style``` should be one of the following:

- nested (default)
- expanded (typical human-made CSS style)
- compact (takes up less space than Nested or Expanded)
- compressed (takes up the minimum amount of space possible)

```lineNumbers```: When set to true, causes the line number and file where a selector is defined to be emitted into the compiled CSS as a comment. Useful for debugging, especially when using imports and mixins.


##FAQ

#### Are there better ways of doing this?

Probaby.

#### Well, then why Python?

This was originally written as a Bash script, to get aquainted with Bash; this was the first project idea that came to mind. Once I was finished, I decided it needed to be rewritten in a more accessible way (the Bash script required Bash 4). So here we are... I should probably mention that this is my first Python script/project.

#### Why not Compass or [your favorite Sass framework/application]?

I just wanted a bare-bones, dead simple way of doing it. I definitely understand that this isn't for everyone. Frankly, it's for me, but you're free to use it if you find it useful.

#### Who is Bella?

[Bella](http://i.imgur.com/Nhu87.jpg) is my 7-year-old Wirehaired Pointer. She's the bacon to my eggs; the peanut butter to my jelly.

---

Note: This is my first Python script, so I am probably using it in naive ways - especially regarding it's distribution and installation. I appreciate any help or guidance you can contribute.

---

Copyright (c) Ryan Domingue. Distributed under MIT License.

