# Small, Better Logger
A small, better logger for C++ (and any project that wishes to use it as .dll) 
> ***Note:*** *From now on, I will refer to this library as ***SBLogger***.*

## Getting Started
This section will provide the information needed to include **SBLogger** in your projects, either as source code or as a library (```.lib``` or ```.dll```).

### Prerequisites
In order to use this library, you will need to compile using a **C++17 (or later)** compiler.

### Including as Source Code
All you need to do if you wish to use **SBLogger** (in a C++ project) is to clone/fork the repo or download the [`SmallBetterLogger.hpp`](SmallBetterLogger/SmallBetterLogger.hpp) file to your project and added as a header file in your code:
````cpp
...
#include "SmallBetterLogger.hpp"
...
````

### Including as Library (WIP)
For other projects, you need to compile it to either a ```.lib``` or a ```.dll``` library and link it in the compiler specific way of your prefered language.

## Usage
All the code which is related to the **SBL** is located in the ```sblogger``` namespace. The loggers are of 2 types: 
  * **```sblogger::StreamLogger```** (which writes to the standard streams)
  * **```sblogger::FileLogger```** (which writes to a file) 


There is also an enum, ```sblogger::STREAM_TYPES``` which is useful when logging with ```sblogger::StreamLogger```, in order to specify STDOUT, STDERR or STDLOG. 
> ***Note:*** *All those previously mentioned can also be written with lowercase letters (i.e.: ```sblogger::stream_logger```, ```sblogger::stream_types```).*

### Logger Methods
All loggers have the following methods for printing messages (inherited from ```sblogger::Logger```):
  * **```void Write(const std::string& message, const T& ...t)```** - write the message ```const std::string& message``` after replacing all placehodlers with the respective parameter value (ex.: ```"{0}"``` will be changed to the value of the first parameter after the string)
  * **```void WriteLine(const std::string& message, const T& ...t)```** - same as ```Write(...)```, but appends the newline character (system dependent, define system macros for proper support, check the [Cross-Platform Info](README.md#Cross-Platform-Info))
  * **```int Indent()```** - increase indent by 1
  * **```int Dedent()```** - decrease indent by 1
  * **```void Flush()```** - flushes the stream

**```sblogger::StreamLogger```** constains an additional method:
  * **```void SetStreamType(STREAM_TYPE streamType)```** - change the current stream type to a different ```STREAM_TYPE```

**```sblogger::FileLogger```** also contains an additional method:
  * **```void ClearLogs()```** - removes all content from the log file

For more information regarding usage, please refer to the [Wiki](README.md) *(WIP)*.

### Usage Examples
The quickest way to use **SBLogger** is to simply create an instance of it. Then just use the methods available for outputting your logs:
````cpp
...
  sblogger::StreamLogger logger;
  ...
	logger.WriteLine("Hello");
	logger.Write("{0}!", "World");
...
````
or if you wanted to write to a file:
````cpp
...
  sblogger::FileLogger logger("mylog.log");
  ...
	logger.WriteLine("Hello");
	logger.Write("{0}!", "World");
...
````

If you wanted to stylize your logs a bit, a basic way to do this is to use a format when instantiating a logger and/or use ```sblogger::Logger::Indent```, as follows:
````cpp
...
  sblogger::StreamLogger logger("[MyLogFormat]");
  ...
  logger.Indent();
	logger.WriteLine("Hello World,");
  logger.Dedent();
	logger.Write("This is my logger!");
...
````
Output:
````
    Hello World,
This is my logger!
````

> ***Note:*** *You can find basic usage examples in the [`Source.cpp`](SmallBetterLogger/Source.cpp) file.*

## Cross-Platform Info
In order for **SBLogger** to work properly outside of **MS Windows**, you should define (at the begining of the file preferably) the following macros:
  * ```#define SBLOGGER_UNIX``` - for ***nix** systems and **Mac OS X+**
  * ```#define SBLOGGER_OS9``` - for **Mac OS 9 and lower**
> ***Note:*** *There is no need to define any macros for ***Windows***, as that is the default for this library.*

## License
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) or [`SmallBetterLogger.hpp`](SmallBetterLogger/SmallBetterLogger.hpp) files for details.

## Acknowledgments
  * [@eugencutic](http://github.com/eugencutic) - Special thanks for code reviews and advice
