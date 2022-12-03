# Python
python tips:
1. how to save farsi fonts in json
```
json_object = json.dumps(new_dict_, ensure_ascii=False)
with open(res_dir, 'w', encoding="utf-8") as f:
    f.write(json_object)
```

How to make tqdm to remove the traces:
	1. set "leave" argument to False. In that case, it won't leave the traces behind.
1. How to add extra information to tqdm:
```
loop = tqdm(loader, leave=True)
for ... in loop:
    ...
    loop.set_postfix(H_real=H_reals / (idx + 1), H_fake=H_fakes / (idx + 1))
#result:
#25%|██▍       | 331/1334 [05:00<13:02,  1.28it/s, H_fake=0.47, H_real=0.527]
```
How to print colorful strings:
```
def colorstr(*input):
    # Colors a string https://en.wikipedia.org/wiki/ANSI_escape_code, i.e.  colorstr('blue', 'hello world')
    *args, string = input if len(input) > 1 else ('blue', 'bold', input[0])  # color arguments, string
    colors = {'black': '\033[30m',  # basic colors
              'red': '\033[31m',
              'green': '\033[32m',
              'yellow': '\033[33m',
              'blue': '\033[34m',
              'magenta': '\033[35m',
              'cyan': '\033[36m',
              'white': '\033[37m',
              'bright_black': '\033[90m',  # bright colors
              'bright_red': '\033[91m',
              'bright_green': '\033[92m',
              'bright_yellow': '\033[93m',
              'bright_blue': '\033[94m',
              'bright_magenta': '\033[95m',
              'bright_cyan': '\033[96m',
              'bright_white': '\033[97m',
              'end': '\033[0m',  # misc
              'bold': '\033[1m',
              'underline': '\033[4m'}
    return ''.join(colors[x] for x in args) + f'{string}' + colors['end']
print(f"\n{colorstr('PyTorch:')} starting from")
```

How to profile a python project:
```
python -m cProfile  Service.py -s 
python -m cProfile  Service.py -s -o out.profile
```

How to profile line by line:
```
!pip install pprofile

profiler = pprofile.Profile()

with profiler:
    # codes you want to profile line by line

profiler.dump_stats("./profiler_stats.txt") # this should be out of the context manager
```
reference: https://stackoverflow.com/questions/3927628/how-can-i-profile-python-code-line-by-line

How to put a string in the center:
```
str_.center(10)
```

How to load a class_based on its path:
```
# object_type is the path to that class. The connection are connected used with dot
cloths_segmentation.inference.InferenceDataset # InferenceDataset this is the class object
pydoc.locate(object_type)
```

How to add entry_points to a python library:
```
# Add the following part to the setup section of the setup.py
entry_points='''
            [console_scripts]
            submit=abstractions.submit_training_job:main
            train=abstractions.train:main
            evaluate=abstractions.evaluate:main
        ''',
# With this modification whenever you execute train in your terminal it's linked to abstractions.train.main function.
```

How to decorate abstract methods:
```
Not possible in python :)
Python is not an appropriate language for enforcing implementation strictures. Make sure to write a good doc for users to add necessary decorators after overwriting an abstract method.
abstract-method makes sure that a method is overwritten or not. It's at the abstraction or interface level. In contrast, decorators are at the implementation level which makes them mutually exclusive.
```

pytest:
```
@pytest.fixture():
This decorates a function as a fixture. Fixture means it's fixed through the rest of the tests. It will be invoked by other test-modules.

@pytest.mark.component
This says this is a component of a bigger structure.

@pytest.mark.dependency() # you should close the parenthesis. 
This states that other classes or modules will be dependent on this class or module. If you remove it the dependency decorators won't be activated and tests will be skipped. Make sure to add it!!!
@pytest.mark.dependency(depends=['TestDataLoader::test_train_generator']) #decoractor won't be activated with out the previous activator.

add --pdb to the end of your pytest commands and it will start the debugger at first error it meets.

use pytest -h !!!
```

what is type in parser.add_argument
```
parser.add_argument('--save_results', type=lambda x: (str(x).lower() in ['true', '1', 'yes']), default=True)
# type is a function that will be applied on the input. that's it.
```

how to bound a library between two specific versions:
```
torchaudio>=0.8.0,<=0.10.1
```

Does pool.map keep the input's order?
```
Yes it does.
pool.imap_unordered is the unordered type.
```

How to create a temporary directory in python:
```
with TemporaryDirectory() as tempdir:
    with ZipFile(io.BytesIO(contents.read())) as zf:
         zf.extractall(tempdir)
# tempdir is a directory and you can use it like a real directory
```

How to pass inputs to multi-argument function using pool.map:
```
use pool.starmap instead.
It's the same functionalities.
```
references: https://stackoverflow.com/questions/8533318/multiprocessing-pool-when-to-use-apply-apply-async-or-map



How to set contents in the center of a table in .md files:
```
| Service | Library | Framework | input data-type |   
|:-------:|:------:|:----------:|:----------:|
| Blood-cell-classification  |tf | uwsgi | Img |
# the colon are representor of alignment
```

How to read a png file with 4 channels:
```
cv2.imread(img-path, cv2.IMREAD_UNCHANGED)
# note: If you have a 4-channel img, you should save it with .png format unless it won't be saved!
```

How to have a combination of patterns in re
```
re.compile('[.-۹]+|٫') 
# note: using | you can have different pattern combination
```


Encoding:

1. If you have encoded a numpy with float64 at decode time you should decode with float64 as well unless the size of the numpy array won't match.

What "@" in python:
```
It's representer of __matmul__. If you implement the __matmul__ function for yourself, it will work fine. 
```

How to make an image to a io.byte and send a post request:
```
        # buf = io.BytesIO()
        # (Image.fromarray(frame)).save(buf, format='JPEG')
        # print(f"{self.frame_counter}-buffer", time.time() - tic)
        # tic = time.time()
        # respond = requests.post(plate_url,
        #                         files={'image': (f"frame_{self.frame_counter}.jpg",
        #                                          buf.getvalue(),
        #                                          'multipart/form-data'
        #                                          )})
```

How to send a json request:
```
byte_img = img_to_b64(frame)
        data = {'image': byte_img}
        print(f"{self.frame_counter}-buffer", time.time() - tic)
        tic = time.time()
        respond = requests.post(plate_url, json=data, headers={"Content-Type": "application/json"})
```

pytest error about missing __init__.py:
```
ERROR: module or package not found: abstractions.tests (missing __init__.py?)
# If you check and see __init__.py file is there. It means that pytest can't import the tests. There is a bug in your code. try to import yourself to find out the bugs.
```

How to make sure a cls is a subclass of the other one based on some specific methods:
```
@classmethod
def __subclasshook__(cls, c):
    """This defines the __subclasshook__ class method.
    This special method is called by the Python interpreter to answer the question,
     Is class C a subclass of this class?
    """

    if cls is PreprocessorBase:
        attrs = set(dir(c))
        if set(cls.__abstractmethods__) <= attrs:
            return True
    return NotImplemented
```


How to convert a list of integers to bytes?
```
h, w = img.shape[:-2]
shape = struct.pack('>II', h, w)
# It's used to pack the shape of an array with itself and ship them together.
```

How to create an installable package in python? we need the following files and folders:
```
1. build
2. dist
3. module_name.egg-info
4. module_name
5. setup.py
6. README.md
The last one is mostly for docker 
```

base64 numpy
```
import base64
import numpy as np

t = np.arange(25, dtype=np.float64)
s = base64.b64encode(t)
r = base64.decodebytes(s)
q = np.frombuffer(r, dtype=np.float64)

print(np.allclose(q, t))
```

how to print 10 like 010:
```
print("{10:03}")
```

How to download from kaggle:
```
os.environ['KAGGLE_USERNAME'] = kaggle_user  # username from the json file             
os.environ['KAGGLE_KEY'] = kaggle_key  # key from the json file                        
os.system('kaggle datasets download -d tawsifurrahman/covid19-radiography-database')
```

How to pass several items to argument parser:
```
nargs=+ >> you can have as much as inputs as possible
nargs=2 >> only two argument are possible
# the type should be the type of the each input element.
parser.add_argument('--target-size', type=int, nargs=2, default=[32, 32], help='Image size for model.',
                        required=False)
```


Flask

1.  is not developed and optimized for security, scalability, and efficiency. 
2. Flask is built on top of the WSGI protocol.
3. Flask doesn't finish a request unless app.after_request in case of existence is done!
4. For multi-scaling flask uWSGI or Gunicorn is used

uWSGI:

1. WSGI(web service gateway interface)
	1. How a web service communicates with web applications.
	2. It's written in python.
2. It's language-agnostic but mostly used for python applications.
3. capabilities:
	1. process management
	2. clustering
	3. load balancing
	4. monitoring
	5. resource limiting
	6. configuration.
4. Reset by peer:
```
Most surely, it happens when there is an error in the code or inside the app.ini
Therefore, Check the logs to solve the issue.
```
5. What is include uwsgi_params:
```
This file is inside /etc/nginx
It contains some information about uswgi
```
6. What is uwsgi_pass:
```
It's a protocol declaration.
uwsgi_pass uses an uwsgi protocol. proxy_pass uses normal HTTP to contact with uWSGI server. uWSGI docs claims that this protocol is better, faster and can benefit from all of uWSGI special features.

What does come after it:
set the address of the uWSGI socket with uwsgi_pass directive
```
7. If a logger prints two or multiple times, it means that several loggers are present in the code. 
	1. How should I solve it? the handlers are accumulated in that case. I solved it in deep-util's get_logger code you can see it there.
8. gdal could be installed in python 3.9 but the wheel should be downloaded or installed directly:
	1. python -m pip install https://sourceforge.net/projects/gdal-wheels-for-linux/files/GDAL-3.4.1-cp39-cp39-manylinux_2_5_x86_64.manylinux1_x86_64.whl
	2. https://sourceforge.net/projects/gdal-wheels-for-linux/

9. Toolbar of jupyter notebook is invisible how to solve it:
```
https://stackoverflow.com/a/65452881/16445477
You need to modify custom.css which is located in 
~/.jupyter/custom/custom.css
change none to block in the following section:
div#maintoolbar {
    display: none !important;
}
```

## How to get header of a request:
```python
import requests
respond = requests.post(URL, headers=headers, data=...)
print(f"respond headers: {respond.headers}")
print(f"request headers: {respond.request.headers}")
```

## How to define headers for form-request using request.post
If you are sending a post request which contains `files`, simply don't bother defining headers:
```python
request.post(URL, files=..., headers={'content-type': 'multipart/form-data'})
```
Because it needs an extra boundary which is like a hash-code. Leave it empty and it works fine.
```commandline
request.post(URL, files=...)
```

## How to run uvicorn with multi-processing
The name of the service should be wrapped in string, so it could be forked by different CPU cores.
```commandline
if __name__ == '__main__':
    run("entry_point:app", host=HOST, port=PORT_NUMBER, workers=4, reload=True)
```

## Where to find wheel files
Some libraries like pytorch have their own website offering the wheel file. However, you can find the wheel files of almost
any project in the following link:
```commandline
https://www.wheelodex.org/projects
https://www.wheelodex.org/projects/deep-utils/
https://www.wheelodex.org/projects/librosa/
```

## To define an enum with str use the following format
```commandline
class ClsName(str, Enum)
# not
class ClsName(Enum, str) # raises error!!
```

## How to add permitted choices to argparser:
```
parser.add_argument("--arg-name",
        default="default-val",
        type=str,
        choices=["default-val", "default-val-1", "default-val-2"],
    ),
```

## How to convert a jupyter notebook cell to a terminal
1) Add `!` before commands
2) Add `%%bash` add the beginning of the cell

## How to view the source code of a module in jupyter notebook:
```
??module-name
```
example:
```
from time import time
??time
output: >>
Docstring:
time() -> floating point number

Return the current time in seconds since the Epoch.
Fractions of a second may be present if the system clock provides them.
Type:      builtin_function_or_method
```
## How to view the definition of a module in jupyter notebook:
```
help(module)
```
or
```
?module
```

## What is `functools.partial`
It simply generates a new function from a predefined function.</br>
Using `partial` one can change the default variables and add new default vlaues
```
from functools import partial
def func(a, b=False):
     print(a, b)
f = partial(func, b=True)
f(1)
# output: 1 True

f = partial(func, a=2, b=True)
f()
# ouptut 2, True
```
 
## How to reload a module
```
import importlib
importlib.reload(module)
```


## How to use TypeVar:
1) When you want the input and output to be the same:
```
from typing import TypeVar

T = TypeVar("T")

def identity(arg: T) -> T:
    return arg
```
2) or
```AnyString = TypeVar("AnyString", str, bytes)

def triple(string: AnyString) -> AnyString:
    return string * 3

unicode_scream = triple("A") + "!"
bytes_scream = triple(b"A") + b"!"
```
Reference: https://dev.to/decorator_factory/typevars-explained-hmo

3) When to bound to a class
```
ClsA = TypeVar("ClsA", bound="A")
class A:
    def func(self) -> ClsA:
       pass
```



