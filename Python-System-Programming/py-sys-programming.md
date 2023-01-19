# **Python System Programming**

Text used as guidance is O'Reilly Programming Python 4th Edition

## What is system programming?

To understand what system programming is, we must first understand some basic concepts.  The following definitions are taken from an article written by Stephen Watts in April 2020 ('https://www.bmc.com/blogs/systems-programming/'):

  **What is a system?**: a system is “a set of things working together as parts of a mechanism or an interconnecting network.”  A system is comprised of five primary elements: architecture, modules, components, interfaces, and data.

  **Architecture** - Architecture is the conceptual model that defines the system structure and behavior. This is often represented graphically through the use of flowcharts that illustrate how the processes work and how each component is related to one another.

  **Modules** - Modules are pieces (hardware or software) of a system that handle specific tasks within it. Each module has a defined role that details exactly what its purpose is.

  **Components** - Components are groups of modules that perform related functions. Components are like micro-systems within the system at large. Using components and modules in this way is called modular design, and it’s what allows systems to reuse certain pieces or have them removed and replaced without crippling the system. Each component can function on its own and can be interchanged or placed into new systems.

  **Interfaces** - Interfaces encompass two separate entities: user interfaces and system interfaces. User interface (UI) design defines the way information is presented to users and how they interact with the system. System interface design deals with how the components interact with one another and with other systems.

  **Data** - Data is the information used and outputted by the system. System designers dictate what data is pertinent for each component within the system and decide how it will be handled.

  **Systems Design** - Systems design involves defining each element of a system and how each component fits into the system architecture.

  System designers focus on top-level concepts for how each component should be incorporated into the final product. They accomplish this primarily through the use of Unified Modeling Language (UML) and flow charts that give a graphical overview of how each component is linked within the system.

  Systems design has three main areas:
  
    - architectural design
    - logical design
    - physical design
  
  The architectural design deals with the structure of the system and how each component behaves within it. Logical design deals with abstract representations of data flow (inputs and outputs within the system).

  Physical design deals with the actual inputs and outputs. The physical design establishes specific requirements on the components of the system, such as input requirements, output requirements, storage requirements, processing requirements, and system backup and recovery protocols. Another way of expressing this is to say that physical design deals with user interface design, data design, and process design.

**Systems programming** involves the development of the individual pieces of software that allow the entire system to function as a single unit. Systems programming involves many layers such as the operating system (OS), firmware, and the development environment.

## Python System Modules

Some of the more common system level modules in Python are:

- **sys**
- **os**
- **glob** - for filename expansion
- **socket** - for network connections and inter-process communication
- **threading, _thread, queue** - for running and synchronizing concurrent threads
- **time, timeit** - for accessing system time details
- **subprocess, multiprocessing** - for launching and controlling parallel processes
- **signal, select, shutil, tempfile** - for various other system related tasks

Note: There are several other third-party system modules

## Using System Modules

> dir returns a list containing the string names of all the attributes in any object with attributes. Eg `dir(sys)`
> All python objects have an attribute `**__doc__ **` which provides a documentation of the object.
