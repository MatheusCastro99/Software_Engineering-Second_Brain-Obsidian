Virtualized OS that contains just the requirements for your application to run
Uses **Images** and **Containers** to run applications
Containers are not small virtual machines
- VM virtualizes hardware while containers virtualizes only the OS Kernel
- Each Image works as an application itself, bringing the whole environment required for what it is trying to run
Container is composed of tow spaces: Host and Kernel
	- 8 preset Host namespaces (brief description of each one)
	- Kernel spaces monitor and restrict computer resources
Docker Desktop as a GUI solutions