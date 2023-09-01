Project 0: Introduction to Go concurrency and testing
==

## Setting up Go

You can download and install Go for your operating system from [the official site](https://golang.org/doc/install).

**Please make sure you install Go version 1.21. The Gradescope autograder uses Go version 1.21 too.**

### Using Go on AFS

For those students who wish to write their Go code on AFS (either in a cluster or remotely), first see if Go 1.21.* is already installed:

```bash
$ go version
go version go1.21.0 linux/amd64
```

If not, follow the guidance to download Go for linux [here](https://golang.org/doc/install).

The file can be downloaded using wget, as below:

```bash
$ wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
```

However, instead of extracting the archive into `/usr/local` as mentioned in the installation instructions, extract the 
archive into a custom location in your home folder with following commands:

```bash
$ tar -C $HOME/(custom_directory) -xzf go1.21.0.linux-amd64.tar.gz
```

Then, instead of adding `/usr/local/go/bin` to the PATH environment variable as mentioned in the
installation instructions, replace `/usr/local` with the path in which you have extracted the archive 
in the step before:

```bash
$ export PATH=$HOME/(custom_directory)/go/bin:$PATH
```

You will also need to set the `GOROOT` environment variable to be the path which you have just extracted
the archive (this is required because of the custom install location):

```bash
$ export GOROOT=$HOME/(custom_directory)/go
```

To avoid having to export the variables across sessions, you can create a bash profile (via `touch ~/.bash_profile`) and add the following statements there:

```bash
export PATH=$HOME/(custom_directory)/go/bin:$PATH
export GOROOT=$HOME/(custom_directory)/go
```

### Using Windows for P0
For the students who wish to write their Go code on their local Windows machine, we suggest using [Windows Subsystem for Linux 2 (WSL 2)](https://docs.microsoft.com/en-us/windows/wsl/about#what-is-wsl-2) because some of our tests use Linux-specific functions.

## Part A: Implementing a key-value messaging system

This repository contains the starter code that you will use as the basis of your key-value messaging system
implementation. It also contains the tests that we will use to test your implementation,
and an example 'server runner' binary that you might find useful for your own testing purposes.

The below `go test` commands should work out-of-the-box. If at any point you have any trouble with building, installing, or testing your code, the article
titled [How to Write Go Code](https://go.dev/doc/code) is a great resource for understanding
how Go workspaces are built and organized. You might also find the documentation for the
[`go` command](http://golang.org/cmd/go/) to be helpful. As always, feel free to post your questions
on Edstem as well.

### Running the official tests

To test your submission, we will execute the following command from inside the
`src/github.com/cmu440/p0partA` directory:

```sh
$ go test
```

We will also check your code for race conditions using Go's race detector by executing
the following command:

```sh
$ go test -race
```

To execute a single unit test, you can use the `-test.run` flag and specify a regular expression
identifying the name of the test to run. For example,

```sh
$ go test -race -test.run TestBasic1
```

### Testing your implementation using `srunner`

To make testing your server a bit easier (especially during the early stages of your implementation
when your server is largely incomplete), we have given you a simple `srunner` (server runner)
program that you can use to create and start an instance of your `KeyValueServer`. The program
simply creates an instance of your server, starts it on a default port, and blocks forever,
running your server in the background.

To compile and build the `srunner` program into a binary that you can run, execute the
command below from within the `src/github.com/cmu440/` directory:

```bash
$ go install github.com/cmu440/srunner
```

Then you can run the `srunner` binary from anywhere by executing:

```bash
$ $HOME/go/bin/srunner
```

(`$HOME/go/bin` is Go's default destination for `go install`'d binaries. If the command fails or you want to change the install directory, see the options [here](https://go.dev/doc/code#Command).)

The `srunner` program won't be of much use to you without any clients. It might be a good exercise
to implement your own `crunner` (client runner) program that you can use to connect with and send
messages to your server. We have provided you with an unimplemented `crunner` program that you may
use for this purpose if you wish. Whether or not you decide to implement a `crunner` program will not
affect your grade for this project.

You could also test your server using Netcat (i.e. run the `srunner`
binary in the background, execute `nc localhost 9999`, type the message you wish to send, and then
hit enter). You can get more information on how to use netcat using the man pages (`man nc`).

## Part B: Testing a squarer

Once you have written your test, simply run

```sh
$ go test
```

in `p0partB` to confirm that the test passes on the correct implementation.

## Submission

Submit the `handin.zip` file created by running `make handin` in `src/github.com/cmu440`. **Do not change the names of the files (`server_impl.go` and `squarer_test.go`) as this will cause the tests to fail.**
