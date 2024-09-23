
---
# REJECTED

 
---
## Potential Ideas

I've been finding it hard to think of anything specific because im not sure of potential use cases for these devices. Might be easier to write a tailor-made OS for a specific use case

### RTOS Implementation
* RTOS for edge devices that are doing something
* Barebones but with networking support, filesystem, usb, and real-time scheduler

**Watchdog**

### Modular OS
* Effectively a very simple way to pack together different features 

### IoT-focused OS
* Low power implementation of IoT protocols
* Builtin integration with other devices

### WinFS filesystem implementation
(specifically the distributed storage) (would probably require pi level hardware)

---
## Chips

Take arduino - easy to do with their libraries
More capable than AVR
Look at hardware library

Single board computers
Good documentation on pi (smaller pi?)

**Do suggest own project (make it sound difficult, Jim Garside) for this type of project**

---
## Questions for Jim

**Optimising mat-mul**
On macbook macos, can run
1. Natively (requires changing SIMD code to use NEON + other stuff)
2. Ubuntu Container (aarch64) (SIMD -> NEON again)
3. Ubuntu Container (x86 emulation)

(imagine containers add overhead - too much noise for measurement?)
will 2/3 affect results. Can I rewrite to use NEON? Best approach for not losing marks?

**About the project**
* Pros and cons of ideas
* Is the scope appropriate

**General**
1. What will the project process look like
2. What do you think separates a good project from an average one (i.e. what is needed for a good mark)
3. What is exciting and new in the unikernel space that I can look into more

Go to script viewing for exam and contest things



