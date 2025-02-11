# The Ethereum Virtual Machine

At the heart of the Ethereum protocol and operation is the Ethereum Virtual Machine, or EVM for short. As you might guess from the name, it is a computation engine, not hugely dissimilar to the virtual machines of Microsoft's .NET Framework, or interpreters of other bytecode-compiled programming languages such as Java. In this chapter we take a detailed look at the EVM, including its instruction set, structure, and operation, within the context of Ethereum state updates.

## What Is the EVM?

The EVM is the part of Ethereum that handles smart contract deployment and execution. Simple value transfer transactions from one EOA to another don't need to involve it, practically speaking, but everything else will involve a state update computed by the EVM. At a high level, the EVM running on the Ethereum blockchain can be thought of as a global decentralized computer containing millions of executable objects, each with its own permanent data store.

The EVM is a quasi–Turing-complete state machine; "quasi" because all execution processes are limited to a finite number of computational steps by the amount of gas available for any given smart contract execution. As such, the halting problem is "solved" (all program executions will halt) and the situation where execution might (accidentally or maliciously) run forever, thus bringing the Ethereum platform to halt in its entirety, is avoided.

The EVM has a stack-based architecture, storing all in-memory values on a stack. It works with a word size of 256 bits (mainly to facilitate native hashing and elliptic curve operations) and has several addressable data components:

- An immutable program code ROM, loaded with the bytecode of the smart contract to be executed
- A volatile memory, with every location explicitly initialized to zero  
- A permanent storage that is part of the Ethereum state, also zero-initialized

There is also a set of environment variables and data that is available during execution. We will go through these in more detail later in this chapter.


## Comparison with Existing Technology

The term "virtual machine" is often applied to the virtualization of a real computer, typically by a "hypervisor" such as VirtualBox or QEMU, or of an entire operating system instance, such as Linux's KVM. These must provide a software abstraction, respectively, of actual hardware, and of system calls and other kernel functionality.

The EVM operates in a much more limited domain: it is just a computation engine, and as such provides an abstraction of just computation and storage, similar to the Java Virtual Machine (JVM) specification, for example. From a high-level viewpoint, the JVM is designed to provide a runtime environment that is agnostic of the underlying host OS or hardware, enabling compatibility across a wide variety of systems. High-level programming languages such as Java or Scala (which use the JVM) or C# (which uses .NET) are compiled into the bytecode instruction set of their respective virtual machine. In the same way, the EVM executes its own bytecode instruction set (described in the next section), which higher-level smart contract programming languages such as LLL, Serpent, Mutan, or Solidity are compiled into.

The EVM, therefore, has no scheduling capability, because execution ordering is organized externally to it—Ethereum clients run through verified block transactions to determine which smart contracts need executing and in which order. In this sense, the Ethereum world computer is single-threaded, like JavaScript. Neither does the EVM have any "system interface" handling or "hardware support"—there is no physical machine to interface with. The Ethereum world computer is completely virtual.