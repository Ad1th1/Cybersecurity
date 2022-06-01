- exploitable by a local user

- Vulnerability
  > when sudo is run through shell mode (through -s or -i option),
  > then parse_args() rewrites argv by concatenating command-line-arguments and escaping meta-characters with back-slashes
  
  > later, set_cmnd() concatenates command-line-arguments into a heap-based buffer and unescapes meta-characters
  > if a command line argument ends with \, it acts as a null terminator that is copied to the "user-args" buffer
  > set_cmnd() is vulnerable to heap-based buffer overflow
  
  
  https://www.youtube.com/watch?v=TLa2VqcGGEQ&t=98s
  - because I am finding the paper a lil hard to digest
  
  - bug that allows any user to gain root priveleges
  - CVE-2021-3156
  - sudoedit -s 'AAAAAAAAAAAAAAAAAAAAAAAAA\'
  - afl is used to fuzz file parsing
  
  - bug was discovered, not by fuzzing, but by going through the sudo source code
  - started with finding a loop in setcmnd() that may incrementa pointer out of bounds
  - then they realized that this should be impossible, because of parse_arg()'s escape
  - then they tried looking for ways to bypass this escape and discovered the sudoedit trick
  
  
  - there is one function that copies strings as command-line arguments and stores it in a heap.
  - at the beginning, this function checks the number of command line arguments and allocates heap space accordingly
  - all is well until a \ is reached, 
  - when we get to a \, we also copy the string's null byte and this points to unrelated data after the string.
  - because of the first \, we also copy the '\0'
  - buffer is now too small
  
  - but there is a function, called parse_args that checks this \ condition to ensure that overwriting won't take place
  - the researchers tried finding another command that can completely bypass this parse_args function
  - modes were checked -> this part is still a little fuzzy to me -> haven't really inderstood which mode
  - best mode is sudoedit -s
  
  
  Exploits:
    - exploitations seem low
    - figure out a way to overflow a service_user structure
    - we have a buffer on the heap that can be overflown
    - to exploit this, we need to be able to control what comes after the buffer
    - during execution, different sized objects are allocated and freed on the heap, leaving the heap fragmented
    - malloc places arguments into different holes
    - grooming the heap to have stuff where you want it to be to exploit easily = heap feng-shui
    - write a script, randomize lc environment variables and buffer size
    - check where sudo crashes using gdb
    - lots of nss functions
    - this is the only seemingly viable exploitation
  
  
  
  
Additional Information:
- fuzzing : novel way to discover security vulnerabilities or bugs in software applications.\ 
            pings” code with random (or semi-random) inputs in an effort to crash it and thus identify “faults” that would otherwise not be apparent.
            
- Parsing a file means reading in a data stream of some sort and building an in memory model of the semantic content of that data. This aims at facilitating\
perfoming some kind of transformation on the data.

- Fuzzing binaries : carried out by afl-fuzz utility. 

- afl = american fuzzy lop. use afl++ instead
- be careful about user priveleges used for fuzzing and debugging

- suid = set user id = allows anyone to run the command as root
- sgid = set group id = allows groups to run the command as root
- sticky bit

- ASLR: Address space layout randomization
       - memory-protection process for OS'es to guard against buffer-overflow attacks by randomizing the location where system-executables are loaded into memory\
       - created as a Linux patch
       - can be defeated in 2 ways
         - leak addresses
         - calculate offsets

- Name Service Switch: 
    - important file for operating system 
    - helps your system know where to find info about different services
    -  ldap = used for user authentication
    -   yet to explore, not completely understood
    -   






            
