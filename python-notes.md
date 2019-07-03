# Python Notes
Benjamin Allan-Rahill

## Strings

### Replacement

#### Compile a script (check for syntax errors) without running

```bash
    python -m py_compile script.py
```
#### Strip a word or replace it from a string

```python
    str.replace(word, '')

    ### USING Reg Ex ###
    article = re.sub(r'(?is)</html>.+', '</html>', article)
```

Reg Ex Syntax:  https://docs.python.org/2/library/re.html

### Printing 

#### Print the representation of a string
```python
    s = 'a\tb'
    repr(s) == 'a\tb'
```
[See here](https://stackoverflow.com/questions/26520111/python-print-string-like-a-raw-string)

#### Print with format()
```python
    s = "Hi {}, my name is {}"
    print(s.format("world", "Ben"))

    ## USE VAR OVER AGAIN ##
    msg = "Hi I go to {0} College. It is located in {0}."
    print(msg.format("Middlebury")) # will print Middlebury in both spots 
```

### Binary

#### print particular length 

will print 2 with 3 places
```python
'{0:03b}'.format(2)
```

## System

### Subprocess

#### Run command

```python
    ## EXAMPLE WITH DOCKER ##
    cmd = 'docker build -t {}:latest . &> out.txt'.format(tag)
    result = subprocess.check_output(cmd, shell=True)
```

#### Capture STDIN and STDERR 

```python
def evalOrDie(cmd):
        proc = subprocess.Popen(cmd, shell=True, stdout = subprocess.PIPE)
        stdout, stderr = proc.communicate()

        if proc.returncode != 0:
            err_str = "\n\nError:\nCOMMAND: {}\nexited with exit value {}\n with output: {}\n and error: {}"
            err_str.format(cmd, proc.returncode, stdout,stderr);
            sys.exit(err_str)

        return stdout
```

#### Error handling 

Good resource [here](https://stackoverflow.com/questions/24849998/how-to-catch-exception-output-from-python-subprocess-check-output)

Good evalOrDie func:

```python
    def _evalOrDie(self, cmd, msg="ERROR"):
            try:
                res = self.subprocess.check_output(cmd, shell=True, stderr=self.subprocess.STDOUT)
                return res
            except self.subprocess.CalledProcessError as cmd_exp:
                print(self.colors.color(cmd_exp.output, fg='red'))
```

### Coloring Output 

#### Using ANSI colors

See PyPi [here](https://pypi.org/project/ansicolors/)

```bash
pip install ansicolors
```

```python 
from colors import color

print("Hello World", fg = 'yellow', bg='green')
```

## VirtualEnv 

### Create new env 

create in dir myenv 

```bash
virtualenv myenv

source mypython/bin/activate
```

## Style

## Docstrings 

see numpy guide [here](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard) 

#### Good Example

```python
        '''
        checkPermissions(file, user, perm)

        Verify the permissions of a specific user 
            
        Parameters
        ----------
        file: str
            the path to the file that is being checked
        user: str
            the name of the user '' '' '' ''
        perm: int
            octal value of permission to check

        Returns
        -------
        bool
            if the user has ALL specified permissions
        '''
```