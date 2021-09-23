[Logging Howto](https://docs.python.org/3/howto/logging.html#)

- Basic Configuration

  - default level is `WARNING`

  - simple example of `logging.basicConfig`:

    ```python
    import logging
    
    '''
    Changed in version 3.9: The encoding argument was added. In earlier Python versions, or if not specified, the encoding used is the default value used by open(). While not shown in the above example, an errors argument can also now be passed, which determines how encoding errors are handled.
    '''
    logging.basicConfig(filename='example.log', encoding='utf-8', filemode='a',level=logging.DEBUG)
    ```

  - simplest way of using logging in multiple modules:

    ```python
    # myapp.py
    import logging
    import mylib
    
    def main():
        logging.basicConfig(filename='myapp.log', level=logging.INFO)
        logging.info('Started')
        mylib.do_something()
        logging.info('Finished')
    
    if __name__ == '__main__':
        main()
    
    # ---------------------------- #
    # mylib.py
    import logging
    
    def do_something():
        logging.info('Doing something')
    ```

    

[Logging Cookbook](https://docs.python.org/3/howto/logging-cookbook.html)

[Advanced Logging Tutorial](https://docs.python.org/3/howto/logging.html#logging-advanced-tutorial)

### Config File

[a blog](https://www.internalpointers.com/post/logging-python-sub-modules-and-configuration-files)

> - the debug **level**;
> - the **qualname** - the name used by the application to get the logger. In my case is **core**, as I did in `core.py` with the instruction `logging.getLogger(__name__)`, and there `__name__` corresponds to **core**;
> - **propagate** - if true, events logged by this logger will be passed to the upper level.



- Handler:
  - the **class** `logging.StreamHandler` to output the messages. That class simply redirects any string to the console;
  - my **defaultFormatter** as a **formatter**;
  - **args** as the list of arguments to the constructor for the handler class. In my example I want to print to the standard ouput.

- Logging from the `__main__` module：

  > When you run a Python script as `python script.py`, the file you feed into the Python interpreter is a module itself and its fully qualified name is `__main__`. This is why it is also called the **main module**. So if you want to print log messages from the main module you need to include it too in the configuration file, like this:
  >
  > ```[loggers]
  > [loggers]
  > keys=root,main,[...]
  > 
  > [...]
  > 
  > [logger_main]
  > handlers=consoleHandler
  > level=DEBUG
  > qualname=__main__
  > propagate=0
  > ```
  >
  > 

- logging variable data
  - "%-style" format-string

```python
import logging
logging.warning('%s before you %s', 'Look', 'leap!')
```

- newer style formatter: [Using particular formatting styles throughout your application](https://docs.python.org/3/howto/logging-cookbook.html#formatting-styles)
  - [LogRecord attributes](https://docs.python.org/3/library/logging.html#logrecord-attributes)

  - for simple usage: `*levelname*` (severity), `*message*` (event description, including variable data) & datetime

  - datetime

    - ‘%(asctime)s’

    -  `basicConfig` `datefmt` argument

      - The format of the *datefmt* argument is the same as supported by [`time.strftime()`](https://docs.python.org/3/library/time.html#time.strftime)

      ```python
      import logging
      logging.basicConfig(format='%(asctime)s %(message)s', datefmt='%m/%d/%Y %I:%M:%S %p')
      ```

      

## Advanced Logging Tutorial

- The logging library takes a modular approach

- Components: loggers, handlers, filters, and formatters.

  - **Loggers** expose the interface that application code directly uses.
  - **Handlers** send the log records (created by loggers) to the appropriate destination.
  - ***Filters*** provide a finer grained facility for determining which log records to output.
  - **Formatters** specify the layout of log records in the final output.

- Log event information is passed between components above in a [`LogRecord`](https://docs.python.org/3/library/logging.html#logging.LogRecord) instance.

- Module-level Logger

  ```python
  logger = logging.getLogger(__name__)
  ```

  
  - logger names track the package/module hierarchy

- Root Logger

- Logging Destination

  - files, HTTP GET/POST locations, email via SMTP, generic sockets, queues, or OS-specific logging mechanisms such as syslog or the Windows NT event log.
  -  ***handler*** classes
  - By default, no destination is set for any logging messages. -> console (`sys.stderr`) 

- Logging Flow

- Loggers:

  >  First, they expose several methods to application code so that applications can log messages at runtime. Second, logger objects determine which log messages to act upon based upon severity (the default filtering facility) or filter objects. Third, logger objects pass along relevant log messages to all interested log handlers.
  - **configuration** and **message sending** methods
  - the most common configuration methods
    - [`Logger.setLevel()`](https://docs.python.org/3/library/logging.html#logging.Logger.setLevel) 
    - [`Logger.addHandler()`](https://docs.python.org/3/library/logging.html#logging.Logger.addHandler) and [`Logger.removeHandler()`](https://docs.python.org/3/library/logging.html#logging.Logger.removeHandler) 
    - [`Logger.addFilter()`](https://docs.python.org/3/library/logging.html#logging.Logger.addFilter) and [`Logger.removeFilter()`](https://docs.python.org/3/library/logging.html#logging.Logger.removeFilter)
  - create log messages:
    - [`Logger.debug()`](https://docs.python.org/3/library/logging.html#logging.Logger.debug), [`Logger.info()`](https://docs.python.org/3/library/logging.html#logging.Logger.info), [`Logger.warning()`](https://docs.python.org/3/library/logging.html#logging.Logger.warning), [`Logger.error()`](https://docs.python.org/3/library/logging.html#logging.Logger.error), [`Logger.critical()`](https://docs.python.org/3/library/logging.html#logging.Logger.critical) 
    - `**kwargs` -> keyword `exc_info`
    - [`Logger.exception()`](https://docs.python.org/3/library/logging.html#logging.Logger.exception) dumps a **stack trace** along with it;  [`Logger.error()`](https://docs.python.org/3/library/logging.html#logging.Logger.error) don't.
    - [`Logger.log()`](https://docs.python.org/3/library/logging.html#logging.Logger.log)  takes a log level as an explicit argument.  Used for logging at custom log levels.
  - [`getLogger()`](https://docs.python.org/3/library/logging.html#logging.getLogger) returns a reference to a logger instance with the specified name if it is provided, or `root` if not. 
    - he names are **period-separated hierarchical structures**.
      - For example, given a logger with a name of `foo`, loggers with names of `foo.bar`, `foo.bar.baz`, and `foo.bam` are all descendants of `foo`.
    - Multiple calls to [`getLogger()`](https://docs.python.org/3/library/logging.html#logging.getLogger) with the same name will return a reference to the same logger object.
    - ***effective level*** : all ancestors are searched until an explicitly set level is found; The root logger always has an explicit level set (`WARNING` by default). 
    - **Message propogation**:
      - Child loggers propagate messages up to the handlers associated with their ancestor loggers.
      - Because of this, it is **unnecessary to define and configure handlers for all the loggers** an application uses.
      - sufficient to **configure handlers for a top-level logger and create child loggers as needed.** 
      - turn off propagation by setting **the *propagate* attribute of a logger** to `False`.

- Handlers

  > [`Handler`](https://docs.python.org/3/library/logging.html#logging.Handler) objects are responsible for dispatching the appropriate log messages (based on the log messages’ severity) to the handler’s specified destination.

  - Muliple Handlers for One logger: 

    - an application may want to send all log messages to a log file, all log messages of error or higher to stdout, and all messages of critical to an email address. 

  - [Useful Handlers](https://docs.python.org/3/howto/logging.html#useful-handlers)

  - built-in handlers' configuration methods:

    -  [`setLevel()`](https://docs.python.org/3/library/logging.html#logging.Handler.setLevel) 

    - [`setFormatter()`](https://docs.python.org/3/library/logging.html#logging.Handler.setFormatter)
    - [`addFilter()`](https://docs.python.org/3/library/logging.html#logging.Handler.addFilter) and [`removeFilter()`](https://docs.python.org/3/library/logging.html#logging.Handler.removeFilter) 

- Formatters

  - Unlike the base [`logging.Handler`](https://docs.python.org/3/library/logging.html#logging.Handler) class, application code may **instantiate formatter classes**

  - three optional arguments – a message format string, a date format string and a style indicator.

  - ```python
    logging.Formatter.__init__(fmt=None, datefmt=None, style='%')
    ```

  - default date format string: `%Y-%m-%d %H:%M:%S`

  - The `style` is one of %, ‘{‘ or ‘$’

-  human-readable format:

  - `'%(asctime)s - %(levelname)s - %(message)s'`

## Configuring Logging

- Three ways:

  - Creating loggers, handlers, and formatters explicitly using **Python code** that calls the configuration methods listed above.

  - Creating a **logging config file** and reading it using the [`fileConfig()`](https://docs.python.org/3/library/logging.config.html#logging.config.fileConfig) function.

    ```python
    logging.config.fileConfig(fname, defaults=None, disable_existing_loggers=True)
    ```

    [Configuration functions](https://docs.python.org/3/library/logging.config.html#logging-config-api)

  - Creating **a dictionary of configuration information** and passing it to the [`dictConfig()`](https://docs.python.org/3/library/logging.config.html#logging.config.dictConfig) function.

  - Method1 example:

    - 1. console handler + formatter

    ```python
    import logging
    
    # create logger
    logger = logging.getLogger('simple_example')
    logger.setLevel(logging.DEBUG)
    
    # create console handler and set level to debug
    ch = logging.StreamHandler()
    ch.setLevel(logging.DEBUG)
    
    # create formatter
    formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    
    # add formatter to ch
    ch.setFormatter(formatter)
    
    # add ch to logger
    logger.addHandler(ch)
    
    # 'application' code
    logger.debug('debug message')
    logger.info('info message')
    logger.warning('warn message')
    logger.error('error message')
    logger.critical('critical message')
    ```

  - Method2 simple example：

    ```python
    import logging
    import logging.config
    
    logging.config.fileConfig('logging.conf')
    
    # create logger
    logger = logging.getLogger('simpleExample')
    
    # 'application' code
    logger.debug('debug message')
    logger.info('info message')
    logger.warning('warn message')
    logger.error('error message')
    logger.critical('critical message')
    ```

    ```ini
    [loggers]
    keys=root,simpleExample
    
    [handlers]
    keys=consoleHandler
    
    [formatters]
    keys=simpleFormatter
    
    [logger_root]
    level=DEBUG
    handlers=consoleHandler
    
    [logger_simpleExample]
    level=DEBUG
    handlers=consoleHandler
    qualname=simpleExample
    propagate=0
    
    [handler_consoleHandler]
    class=StreamHandler
    level=DEBUG
    formatter=simpleFormatter
    args=(sys.stdout,)
    
    [formatter_simpleFormatter]
    format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
    datefmt=
    ```

    

- Configuration File Format
  - [Configuration file format](https://docs.python.org/3/library/logging.config.html#logging-config-fileformat)

## LOGGING COOKBOOK

### Using logging in multiple modules[¶](https://docs.python.org/3/howto/logging-cookbook.html#using-logging-in-multiple-modules)

- Multiple calls to `logging.getLogger('someLogger')` return a reference to the **same logger object**. This is true not only within the same module, but also across modules as long as it is **in the same Python interpreter process**

- additionally, application code can define and configure a **parent logger in one module** and create (but not configure) a **child logger in a separate module**

- Example:

  - main module

    ```python
    import logging
    import auxiliary_module
    
    # create logger with 'spam_application'
    logger = logging.getLogger('spam_application')
    logger.setLevel(logging.DEBUG)
    # create file handler which logs even debug messages
    fh = logging.FileHandler('spam.log')
    fh.setLevel(logging.DEBUG)
    # create console handler with a higher log level
    ch = logging.StreamHandler()
    ch.setLevel(logging.ERROR)
    # create formatter and add it to the handlers
    formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    fh.setFormatter(formatter)
    ch.setFormatter(formatter)
    # add the handlers to the logger
    logger.addHandler(fh)
    logger.addHandler(ch)
    
    logger.info('creating an instance of auxiliary_module.Auxiliary')
    a = auxiliary_module.Auxiliary()
    logger.info('created an instance of auxiliary_module.Auxiliary')
    logger.info('calling auxiliary_module.Auxiliary.do_something')
    a.do_something()
    logger.info('finished auxiliary_module.Auxiliary.do_something')
    logger.info('calling auxiliary_module.some_function()')
    auxiliary_module.some_function()
    logger.info('done with auxiliary_module.some_function()')
    Here is the auxiliary module:
    
    import logging
    
    # create logger
    module_logger = logging.getLogger('spam_application.auxiliary')
    
    class Auxiliary:
        def __init__(self):
            self.logger = logging.getLogger('spam_application.auxiliary.Auxiliary')
            self.logger.info('creating an instance of Auxiliary')
    
        def do_something(self):
            self.logger.info('doing something')
            a = 1 + 1
            self.logger.info('done doing something')
    
    def some_function():
        module_logger.info('received a call to "some_function"')
    ```

    Auxiliary Module

    ```python
    import logging
    
    # create logger
    module_logger = logging.getLogger('spam_application.auxiliary')
    
    class Auxiliary:
        def __init__(self):
            self.logger = logging.getLogger('spam_application.auxiliary.Auxiliary')
            self.logger.info('creating an instance of Auxiliary')
    
        def do_something(self):
            self.logger.info('doing something')
            a = 1 + 1
            self.logger.info('done doing something')
    
    def some_function():
        module_logger.info('received a call to "some_function"')
    ```

    

