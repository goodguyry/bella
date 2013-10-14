Bella
===================

A Python script to take the redundancy out of executing the ```sass --watch``` command. Contributions welcomed and appreciated.

## Installation

#### Using Git

Clone the repo into the directory of your chosing and run the setup file (with no options).

```bash
git clone https://github.com/goodguyry/bella.git && cd bella && source setup
```

#### Git-free

Download the files into the directory of your chosing and run the setup file (with no options).

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

During setup, [.bella_global](https://github.com/goodguyry/bella/blob/master/docs/bella_global) is copied to your home folder and [bella](https://github.com/goodguyry/bella/blob/master/bella) is copied to ~/.bin (the directory is created if it doesn't already exist).

### Use

Once in **~/.bin**, Bella can be run from the root of your site:

```
bella
```

The following optional arguments are available to override your [configuration files](https://github.com/goodguyry/bella#configuration-files):

```python
bella -w <watchFile> -p <processedFile> -e <environment> -s <style>
```

<table>
  <tr>
    <td><code>-w</code>, <code>--watchFile</code></td>
    <td>The file you want Sass to watch</td>
  </tr>
  <tr>
    <td><code>-p</code>, <code>--processedFile</code></td>
    <td>The filename you want Sass to give the processed (CSS) file</td>
  </tr>
  <tr>
    <td><code>-e</code>, <code>--environment</code></td>
    <td>Switch away from your default environment</td>
  </tr>
  <tr>
    <td><code>-s</code>, <code>--style</code></td>
    <td>One of the <a href="#sass">Sass style options</a></td>
  </tr>
</table>

If you've got your [configuration files](https://github.com/goodguyry/bella#configuration-files) set right, you should only need the options when switching environments...

```
bella -e deploy
```

... or if you want to watch a file other than the default input file...

```
bella -w print
```

... or if you want to change the name of the processed file.

```
bella -p main
```

The settings are applied in this order:

1. bella_global
2. bella.config
3. Optional command line arguments

**Screenshot** *(based on the configuration in the following section):*

![](http://i.imgur.com/9b5vEuC.png)

### Configuration files

The configuration files (bella_global and bella.config) are python dictionary files.

[bella_global](https://github.com/goodguyry/bella/blob/master/docs/bella_global):
This is a great place to define your environment settings, as those usually won't change from project to project.

```python
# From bella_global

# Global configuration file
# Served from home directory
# If not present in the user's home directory,
#   all configuration setting must be in bella.config

{

  'defaults': {
    'environment': 'develop',
    'precision': 4,
    'watchFile': 'core',
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

[bella.config](https://github.com/goodguyry/bella/blob/master/bella.config):
Project-specific settings to override the global defaults. This file is required and must be in your project root.

```python
# From bella.config

# Local configuration file
# Required to be served from the project's root directory

{

  "paths": {
    "cssPath":"_/css/",
    "sassPath": "_/sass/"
  }

}

```

**Bella-specific settings**


```environment``` is the default environment; the environment can be either _develop_ or _deploy_.

```watchFile``` is the file you want Sass to watch; the processed (output) file will be named the same as the watchFile unless overridden by the ```-o``` command line option.

```addMinToFilename``` and ```addMaxToFilename``` will append _min_ or _max_ (respectively) to the processed CSS file's name; _max_ when not compressed, _min_ when compressed (e.g, default.min.css).

```paths``` are the relative paths (from the root) to the Sass and CSS files.

**<a name="sass"></a>Sass-specific settings** ([from the Sass reference](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html))

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

I just wanted a bare-bones, dead simple way of doing it. I definitely understand this isn't for everyone. Frankly, it's for me, but you're free to use it if you find it useful.

#### Who is Bella?

[Bella](http://i.imgur.com/Nhu87.jpg) is my 7-year-old Wirehaired Pointer. She's the bacon to my eggs; the peanut butter to my jelly.

---

Note: This is my first Python script, so I am probably using it in naive ways - especially regarding it's distribution and installation. I appreciate any help or guidance you can contribute.

---

Copyright (c) Ryan Domingue. Distributed under MIT License.

