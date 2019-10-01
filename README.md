# PyCon 2018 Notes

I am adding the notes I took from the PyCon 2018 in Cleveland, with my own commentary in the **TL;DR** section of each talk.


## Keynote - Tools vs. Platforms

Dan Callahan (Mozilla)

[Video](https://www.youtube.com/watch?v=ITksU31c1WY)

**TL;DR**: For those who care about the Python's longevity in the web-first future,check out Wasm. It is less relevant for me as a data scientist though.

* Platform dictates the tool
  * When Dan grew up, platform that he was using completely dictates the tool he use. (IBM -> BASIC)
  * TI-82 is also programmable in BASIC
  * Can the future tool be Python?

* Mozilla:
  * Mozilla uses Python in their development. Python is a great tool, but the tool is at the mercy of the platform.
  * He has had experiences in other platforms where Python is not as relevant.

* "Python is the second best language for anything" - speaks about the versatility of Python.

* Prevalent platforms:
  * Current: Windows, macOS, Linux
  * Emerging: iOS, Android, ChromeOS
  * Future: Augmented reality? Smart fridges?
  * Increasingly, mobile and web are the emerging computing platforms, where Python may not be as relevant
  * The only tool that is universal is the web

* Javascript is increasingly popular because of the prevalence of web. Everyone has a browser!

* Jupyter notebook:
  * Good: Interface with Python from within the browser
  * Bad: Python has to run somewhere. What if you don't have PC or a reliable internet connection?
  * Solution: WebAssembly (new project that surfaced in last year)

* WebAssembly
  * Wasm is designed as a portable target for compilation of high-level languages like C/C++/Rust, enabling deployment on the web for client and server applications.
  * We can run (emulate) OS and OS-specific apps from the web! (Demo: Win 3.1 + Netscape inside a modern Firefox browser)
  * Limitations for Python: because it runs inside the web-based sandbox, it only has access to the resources that the web has access too. It does not have access to the main memory and large CPU resources, etc


## Build Teams as an Engineer

Joyce Jang

[Video](https://www.youtube.com/watch?v=-9NpTeddWds)

**TL;DR**: comparing the process of team building and setting up rituals with software and API development is an interesting analogy. Good primer for those who are (or at least thinking about) building new teams; may be less relevant for those who are individual contributors.

**Abstract**: We build product and software as teams. And as anyone who as worked on a team knows, there’s often a lot more that goes into working together to build that product than actually just building the product itself. A highly functional team is not as elusive it may seem. Software engineering is a skill we’ve developed, but even more importantly software engineering on teams is another skill we’ve been practicing and improving on as an industry. Software engineering principles and best practices may seem to have very little to do with teamwork, but being able to thoughtfully apply some of what we’ve learned as engineers towards teamwork, we can help move towards creating such success with our teams.

* Determine how each individual fits into the team focus, and how they will contribute to the success of the team.

### Communications

* How does an individual on the team communicate with rest of th team
* How does the team communicate with other teams
* How does the team communicate with the larger company
* ... not unlike API design

### Checklist

* Gather information, get answers
* Set a focus
* Draft a team plan
* Design a communication system
* Execute & drive sustainability
  * Practice make decisions
  * Have them drive meetings (set up agenda, document meeting notes)
  * Keep the feedback loop tight


## Performance Python: Seven Strategies for Optimizing Your Numerical Code

Jake VanderPlas

[Video](https://www.youtube.com/watch?v=zQeYx87mfyw), [Slide deck](https://speakerdeck.com/jakevdp/seven-strategies-for-optimizing-numerical-code)

**TL;DR**: Nice overview of strategies for numerical python code optimization. Though I imagine that a lot of user in C1 data community will be adequately-served by using pandas.

**Abstract**: Python provides a powerful platform for working with data, but often the most straightforward data analysis can be painfully slow. When used effectively, though, Python can be as fast as even compiled languages like C. This talk presents an overview of how to effectively approach optimization of numerical code in Python, touching on tools like numpy, pandas, scipy, cython, numba, and more.

The best of both worlds for fast write and fast execution

1. Line profiling: `line_profiler` extension - helping you optimize which part of your routine needs optimization
2. Numpy vectorization. For deeper dive, see his same talk "Lose your loops" from PyCon 2015
3. Specialized data structures (e.g. Scipy).
   * Example: for K-means clustering, we can use KD-Tree for searching nearest neighbors, or use pandas groupby
   * Other examples: `scipy.spatial`, `pandas`, `xarray`, `scipy.sparse`, `scipy.sparse.csgraph`
4. Cython: combine power C and Python. Recommendation: use for operations that can't be easily expressed in numpy
5. numba: infer types. Use by introducing numba decorators. Recommendation: use for analysis scripts where dependencies are not a concern.
6. Dask: similar with numpy API. Recommendation: use when data size or computation time warrants (high overhead)
7. Find an existing implementation!


## Using Python to build an AI to play and win SNES StreetFighter II

Adam Fletcher, Jonathan Mortensen

[Video](https://www.youtube.com/watch?v=NyNUYYI-Pdg)

**TL;DR**: Cool application of state-of-art computer vision and reinforcement learning techniques on a classic game. It speaks volumes to how "trendy" the topic of machine learning is - it was a standing room only talk

**Abstract**: Hear the story of how we used Python to build an AI that plays Super StreetFighter II on the Super NES. We'll cover how Python provided the key glue between the SNES emulator and AI, and how the AI was built with gym, keras-rl and tensorflow. We'll show examples of game play and training, and talk about which bot beat which bot in the bot-v-bot tournament we ran.

After this talk you'll know how easy it is to use Python and Python's machine learning libraries to teach a computer to play games. You'll see a practical example of the same type of machine learning used by AlphaGo, and also get to find out which character in StreetFighter II is best to pick when playing your friends.

* They use `gym`, `keras-rl` and `tensorflow`.
* This sounds like a side-of-desk project. The presenters work at a startup called gyroscope, which is recently acquired by BlueVoyant.
* (Didn't take any notes because I was not near my computer)


## Beyond scraping: how to use machine learning when you're not sure where to start

Julie Lavoie

[Video](https://www.youtube.com/watch?v=BwC01zoSRBc)

**TL;DR**: a pretty-well structured talk on a bite-sized machine learning problem (classifying DOM elements on whether or not they contain dates). You won't learn any new fancy algorithms, but the speaker did a good job of explaining when machine learning may or may not make sense. (Again, room was completely full, also standing only)

**Abstract**: Scraping one web site for information is easy, scraping 10000 different sites is hard. Beyond page-specific scraping, how do you build a program than can extract the publication date of (almost) any news article online, no matter the web site?

We’ll cover when to use machine learning vs. humans or heuristics for data extraction, the different steps of how to phrase the problem in terms of machine learning, including feature selection on HTML documents, and issues that arise when turning research into production code.

* Problem domain: extract dates from news article online.
  * Extract dates of "any" page is hard.
* Solutions that don't make sense:
  * Get people to do it (mechanical turk) - not scalable, but might be necessary to enable training samples
  * Get a programmer to do it - patterns can be more complex than a human can understand
  * The big guns: get machine learning to do it - they use supervised training
    * machine learning is a PITA
    * "The punishment has to fit the crime"
* The hardest part of machine learning... is setting up the problem so that the machine learning can answer.
* Supervised learning / classification
  * Classification: does this DOM element contain pub date for this article or not
* Practical issues in date collection:
  * After correct publication date is entered into csv, web apge goes 404
  * Articles have pub dates when viewed in the browser
  * ....
* Get all DOM elements w/ dates
* Feature selection
  * Good to start with heuristics b/c a lot of features can come from there
  * contains word "posted", "modified", ""
  * Bold or italic
* Train the models: she used NLTK + Naive Bayes


## Elegant Solutions For Everyday Python Problems

Nina Zakharenko

[Video](https://www.youtube.com/watch?v=WiQqqB9MlkA), [Slide deck](https://www.slideshare.net/nnja/elegant-solutions-for-everyday-python-problems-pycon-2018)

**TL;DR**: A fast-paced talk about the magic methods, custom iterators, and the like. Worth re-visiting - I definitely did not absorb all the concepts the speaker said.

**Abstract**:

Are you an intermediate python developer looking to level up? Luckily, python provides us with a unique set of tools to make our code more elegant and readable by providing language features that make your code more intuitive and cut down on repetition. In this talk, I’ll share practical pythonic solutions for supercharging your code.

Specifically, I'll cover:

What magic methods are, and show you how to use them in your own code.
When and how to use partial methods.
An explanation of ContextManagers and Decorators, as well as multiple techniques for implementing them.
How to effectively use NamedTuples, and even subclass and extend them!
Lastly, I'll go over some example code that ties many of these techniques together in a cohesive way. You'll leave this talk feeling confident about using these tools and techniques in your next python project!

* How do we make code elegant? We pick the right tool for the job!
* Magic methods
  * start and end with a double underscore (aka. dunder)
  * you can make your objects behave like built-ins (dict, numbers, numberic operations, etc)
  * See example from slide deck
* Custom iterators
  * Making classes iterable: need to implement `__iter__()` and `__next__()`
  * tip: if your iterator does not need to maintain state (which is most of the time), use a generator instead
* Method Magic
  * We can alias methods: `concat = __add__`
  * `getattr()`
* `functools.partial`
  * Returns a new partial object which behave like func called with args and kwargs
* Context managers
  * feature tags: Turn features of your applcation on and off easily. (A/B testing, rolling releases, etc)
  * example: freezegun
* NamedTuple


## Keynote - App security primer

Ying Li (security software engineer @ Docker)

[Video](https://youtu.be/VJ0vibC_Hl0?t=35m24s)

**TL;DR**: Security is everyone's responsibility and your should start by following basic practices. (Side note: the keynote speaker delivered this content in the form of children's book! Extremely engaging, entertaining and accessible!)

* Security is everyone's responsibility
* Follow basic best practices (Django default, ORM, Auth, TLS, updates)
  * Use Django defaults to prevent string literal job
  * Use VPN so that the different server are compartmentalized
  * Anonymizing customer info and set up cron job to delete old data
  * Add static code analysis tool in Jenkins to prevent injection attacks
* Jetbrains and PSF survey of Python user base (https://www.jetbrains.com/research/python-developers-survey-2017/):
  * ~ 23% web developers
  * ~ 27% data scientist


## Keynote - Coding class for Detroit library

Qumisha Goss

[Video](https://youtu.be/VJ0vibC_Hl0?t=1h8m2s)

**TL;DR**: This talk touches upon a deeper level of causes of lower-engagements from minority communities.

* Detroit public library wants to teach kids how to code. They started with Tynker; engagement was great in the beginning but decreased later because it was too easy
* Next up: Raspberry PI, Minecraft PI, Robocars Pi, etc
  * Next project: greenhouse. Build water sensors and camera system to watch the plants grow
* Her issues w/ the Python training for kids
  * Diversity (women / minorities)
  * Fundamental issues: poverty, illiteracy, hunger, crime / violence


## Democratizing Distributed Computing with Dask and JupyterHub

Matthew Rocklin

[Video](https://www.youtube.com/watch?v=Iq72dt1gO9c), [Slide deck](https://matthewrocklin.com/slides/pycon-2018#/)

**TL;DR**: Accessible talk about numerical scientific computing stack used by Pangeo team with concrete examples. Also a call for help for developing these open source tools.

**Abstract**: We use JupyterHub, XArray, Dask, and Kubernetes to build a cloud-based system to enable scientists to analyze and manage large datasets. We use this in practice to serve a broad community of atmospheric and climate scientists.

Atmospheric and climate scientists analyze large volumes of observational and simulated data to better understand our planet. They have historically used tools like NumPy and SciPy along with Jupyter notebooks to combine efficient computation with accessibility. However, as datasets increase in size and collaboration extends to new populations of scientists these tools begin to feel their age. In this talk we use more recent libraries to build a modern deployment for academic scientists. In particular we use the following tools:

Dask: to parallelize and scale NumPy computations
XArray: as a self-describing data model and tool kit for labeled and index arrays
JupyterLab: to enable more APIs for users beyond the classic notebook
JupyterHub: to manage users and maintain environments for a new population of cloud-friendly users
Kubernetes: to manage everything and deploy easily on cloud hardware
This talk will focus less on how these libraries work and will instead be a case study of using them together in an operational setting. During the talk we will build up and deploy a running system that the audience can then use to access distributed computing resources.

* Enabling Climate Science at Scale.
  * Toolset: xarray, jupterhub -> PANGEO

* Context for scientific python (specifically for atmospheric and oceanographic science)
* Small data (100GB or smaller on one machine)
  * jupyter notebook
  * xarray: store and compute on collections of multi-dimensional arrays
  * numpy & pandas
  * Matplotlib
* Challenges:
  * Data scale: NASA plans to dump 100's of petabytes of images
  * Human scale: more researchers adopting new data sources, but average technical proficiency is often not enough
* Big data (larger than 100GB):
  * Jupyterlab: more mature, more IDE-like. Benefits are more obvious when you work on clusters
  * Jupyterhub
  * Dask
  * Kubernetes: manage resources like JupyterHub and Dask


## Inside the Cheeseshop: How Python Packaging Works

Dustin Ingram

[Video](https://www.youtube.com/watch?v=AQsZsgJ30AE), [Slide deck](https://github.com/di/talks/tree/master/pycon_2018)

**TL;DR**: The speaker is a maintainer of PyPi and this talk is a very good talk about the history of python packaging! I definitely walked away thinking that I know quite a bit more about the history of python packaging.

**Abstract**: Questions and confusion about the Python packaging ecosystem abound. What is this setup.py file? What's the difference between wheels and eggs? Do I use setuptools or distutils? Why should I use twine? Do I put my projects dependencies in a requirements.txt or in setup.py? How do I just get my module up on PyPI? Wait, what is Warehouse?

This talk will identify the key tools one might encounter when trying to distribute Python software, what they are used for, why they exist, and their history (including where their weird names come from). In addition, we'll see how they all work together, what it takes to make them work, and what the future has in store for Python packaging.

* Archaeology of Python packaging
  * Before PyPi: Email, personal website ...
  * Problem: How do I find Python code?
  * Old portal: Vaults of Parnassus
  * `disutils`: included in standard lib since 2001 (Python 1.6). Write `python setup.py`
  * `sdist`: `python setup.py sdist` (problem: building takes too long)
  * `bdist`: Build distributions (no build step). Problem: how to manage packages?
  * Use platform packaging (e.g. Linux has rpm). But many OS don't have official package managers
  * PyPi (Python package index)
  * Specify dependencies: `setuptools`
  * `easy_install`: in conjunction with `egg` distribution, make installation easy
  * `pip`: "pip install packages" - only install from source distribution. Better for managing your existing install.
  * Problem:
    * Install from PyPI is slow (PyPI at the time only just link to external lib)
  * Problem:
    * New distribution: wheel. Upgrade to wheel
* `twine`: upload to PyPI using security https
* PyPI is showing age its age.
  * Predates the modern web frameworks
  * Not compatible with state-of-art CICD platforms
* Re-written PyPI
  * Warehouse
  * Https everywhere
* Resources
  * Python package guide
  * sampleproject
* Ongoing problems:
  * Spammers (typo-squatting, etc)
  * Sometimes I need more than Python - solution: `conda`
  * Reproducible environments - `pipfile/pipfile.lock
  * `setup.py` executes arbitrary code
  * The disutils / setuptools dance - hard to improve/maintain, and hard for users to use anything else (because they are de facto standards)


## Reinventing the Parser Generator

David Beazley

[Video](https://www.youtube.com/watch?v=zJ9z6Ge-vXs)

**TL;DR**: This is one of those talks where even I can't understand it, I can still consider it fun. I have no idea how Python work behind the scenes, and this talk make me appreciate just how much I don't understand!

**Abstract**: Writing lexers and parsers is a complex problem that often involves the use of special tools and domain specific languages (e.g., the lex/yacc tools on Unix). In 2001, I wrote Python versions of these tools which can be found in the PLY project. PLY predates a huge number of modern Python features including the iteration protocol, generators, decorators, metaclasses, and more. As such, it relied on a variety of clever hacks to layer a domain specific parser specification language on top of Python itself.

In this talk, I discuss a modernization of the PLY project that abandons its past and freely abuses modern Python features including advanced metaclasses, guaranteed dictionary ordering, class decorators, type hints, and more. The result of this work can be found in the SLY project. However, this talk isn't so much about SLY as it is focused on how far you can push Python metaprogramming features to create domain-specific languages. Prepare to be horrified--and to write code that will break your IDE.

* Programming is magic
  * Basic data structure
  * Magic methods
  * Linguistic abstraction - making your own programming languages
    * Lexing (recognize what are numbers, operations, etc)
    * Parsing (recognize grammar of programs )
    * Abstract syntax tree
* Parsing is magic
  * Theory is dense
  * Most people turn to tools. e.g. yacc
  * Python source works this way too, pgen parse python code into C (?)
* PLY:
  * Python Lex-Yacc
  * A mashup of Unix yacc and Spark


## Bayesian Non-parametric Models for Data Science using PyMC3

Christopher Fonnesbeck

[Video](https://www.youtube.com/watch?v=-sIOMs4MSuA)

**TL;DR**: the first one-third of the talk is a high level introduction to Bayesian statistics and Gaussian process. The rest of the talk I learned that I don't know enough about Bayesian statistics.

**Abstract**: Nowadays, there are many ways of building data science models using Python, including statistical and machine learning methods. I will introduce probabilistic models, which use Bayesian statistical methods to quantify all aspects of uncertainty relevant to your problem, and provide inferences in simple, interpretable terms using probabilities. A particularly flexible form of probabilistic models uses Bayesian non-parametric methods, which allow models to vary in complexity depending on how much data are available. In doing so, they avoid the over-fitting that is common in machine learning and statistical modeling. I will demonstrate the basics of Bayesian non-parametric modeling in Python, using the PyMC3 package. Specifically, I will introduce two common types, Gaussian processes and Dirichlet processes, and show how they can be applied easily to real-world problems using two examples.

* Specific application for statistical and probabilistic machine learning
* He is going to cover primarily non-parametric models.
* Motivation: data is messy
  * Textbook examples are often not reflective of real world
* Default statistical assumptions often include:
  * Parametric distribution for data
  * Linear relationships among variables
* Bayesian inference
  * Make inference about things we care about using probability
* Example for today: Model complex, non-linear distributions using gaussian function
  * Nice things we use for: The conditional distribution of some elements of a multivariate normal is also normal
  * Marginal distribution of some elements of a multivariate normal is also normal
* Gaussian process: general process. Rather than distribution over values, it is a distribution over functions
  * Infinite collections of random variables, any finite subset of which has a Gaussian distribution
  * Infinite parameters: need big data to really shine
  * Art in using Gaussian process is to pick the right covariance function
    * Quadratic
    * Cosine
    * (Others)
* Prior Gaussian process
  * need to specify mean and covariance function
  * Gaussian processes in Python
    * GPy, GPflow, scikit-learn, PyStan, Edward, George, PyMC3
* PyMC3
  * PP framework for fitting arbitrary probaility models
  * based on Theano (but may be switched to Tensorflow backend)
* Example: salmon spawning data
  * Gaussian data + GP prior, get Gausssian process back
  * Making prediction with Gaussian processes - posterior predictive distribution
  * Probabilistic models has error bars that comes more or less for free
* Example: coal mining disasters
  * Latent Gaussian process:
  * For counts we can use a Poisson distribution
  * MCMC sampling
  * With MCMC you can get posterior hyperparameter eisates
* Example: measles outbreak (published paper from his group in 2018)
* Scaling Gaussian processes
  * Does not scale well. Not a big data analysis tool
  * Reason: Posterior covariance has O(N^3) compute time, O(N^2) memory
  * Solution: sparse approximation methods to select a very small subset of the data to run your process.
* Example: Boston marathon times
  * PyMC3 use K-means to decide which data to sample (e.g. picking the rightly-space points in age)
* Example: Spatial sample (non-uniform sample in space)
  * Matern32 covariance
* Other things you can do with Gaussian processes:
  * GP for classification
  * Neural networks
  * Reinforcement learning
* Pros:
  * Flexible modeling of complex, non-linear processes
  * Fully probilistic predictions
  * Interpretable hypermeters
  * Easy to automate
* Cons:
  * Scale poorly with large data (without approximation)


## The Journey Over the Intermediate Gap

Sara Packman

[Video](https://www.youtube.com/watch?v=49CIIu1XkIE)

**TL;DR**: helpful tips if you are a Python newbie. Not so helpful if you are not.

**Abstract**: Congratulations on finishing your first tutorials or classes in python! In the parlance of the hero’s journey myth, you’ve had your ‘threshold moment”: you’ve started down a path that could lead to a long and fulfilling career. But the road to this glorious future is frustratingly obscured by a lack of guidance in the present. You know enough to realize that you don’t have all the skills you need yet, but it’s hard to know how to learn those skills, or even articulate what they are. There are no easy solutions to this problem. There are, however, a few fundamental things to know and advice to keep in mind. Drawing from my own experience and with input from others, I’ve compiled some helpful hints about the skills, tools, and guiding questions that will get you to mastery.

* You have to step over your own threshold
* Find mentor and allies
* Learn to work collaboratively
* Rely on the work of others (use libraries)
* Get to know your tooling (editor goodies, linters, debuggers and REPLs)
* Study up! (choose books that match learning style)
  * Version control, testing, command line and shell navigation, environment management


## Keynote - setting expectations for OSS contributions

Brett Cannon @ Microsoft

[Video](https://www.youtube.com/watch?v=Qzl8A6x7XZE)

**TL;DR**: Good overview of reasonable expectations for OSS contributions, both from the maintainer and user side.

* What is the purporse of an open source project / community?
  * To collaborate on the maintenance of a project
  * To have fun
* How do you sustain an open source project / community?
  * Attract new people
  * Retain current people
* Set reasonable expectations so that open source works for everyone
* People tend to forget two things:
  * Everything in open soruce has a cost (time, effort, emotional output)
  * Open source should be a series of unsolicited kindness.
* Using open source (Maintainer -> User)
  * It can be like someone leaving out pamphlets you find offensive. Solution: even the docs matter - needs to be inclusive and understanding
  * Providing feedback: it can be like a family member telling you, "you're stupid". Solution: think about that there is a person behind every code
  * Submitting a contribution; it can be like when someone tries to give you a puppy you didn't want
  * Maintaining: it can be like arguing with your siblings about politics
* Simply based on csale, maintainers are abused much more often than contributors
* Everyone needs to act like a kindness does not require anything in return. (e.g. don't take "maintainer didn't accept my PR" personally)
* Everyone needs to act like everything is being done as a kidness for them (e.g. give people benefit of doubt)
