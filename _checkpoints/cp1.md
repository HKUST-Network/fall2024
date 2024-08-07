---
type: assignment
date: 2018-09-26T4:00:00+4:30
title: 'Checkpoint 1: Kickoff'
due_event: 
    type: due
    date: 2018-11-13T23:59:00+3:30
    description: 'Checkpoint #1 due'
---

# Validate your GitHub student status

Please do it as soon as possible. It may take a few days to validate your status.

# Create a **PRIVATE** repo of your project

Later, clone the repo to your local machine.
```
git clone <your-repo-url>
```
*Reminder: Use git to clone the repo instead of download as a zip. Otherwise you cannot track the changes.*

# Install Vagrant and VirtualBox

You can use Vagrant and VirtualBox to automatically setup the environment. Different OSes require different installation steps.

If you are using Windows Subsystem for Linux (Linux), please refer to the installation steps for Linux. I also recommend you to do in that way -- Linux is an important tool for developers.
Otherwise, follow the instructions below.

* [Install Vagrant](https://www.vagrantup.com/downloads.html)
* [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)

*FAQ: Where is the terminal on my laptop?* The best way to access the terminal is in Visual Studio Code. This is the most popular IDE for developers. Under the View menu, you can find the Terminal option. 

# Setup the environment

Once you have both Vagrant and Docker Desktop installed, navigate inside this repo and run:

```bash
# In your project root folder where your Vagrantfile is located
vagrant up --provider=docker
# builds the server and client containers using Docker.
```
*If error messages show up, double check if the Docker Engine has started. For Windows users, open the Docker Desktop and manually start the Docker Engine if it's not started.*

*FAQ：Error message "config.size > 0"* This is because you are using an old version of Vagrant. Please download the version 2.4.2 or above.

After the containers are built, you can access the client and server containers using the following commands:
```bash
vagrant ssh client
vagrant ssh server
# connects to either the client or server using SSH.
```
*You will need to open two terminals to connect to server and client separately.*

Vagrant keeps all files synchronized between your host machine and the two containers. 
In other words, the code will update automatically on the containers as you edit it on your computer. 
Similarly, debugging files and other files generated on the containers will automatically appear on your host machine.

# Run the server and client

## Build the binaries

```bash
# In the server VM
cd /vagrant/foggytcp
make system
```
You will see the binaries `server` and `client` in the `foggytcp` folder.

Remember, each time when you modify the code, you need to rebuild the binaries.

## Read and understand the `server.cc` and `client.cc`

The `server.cc` and `client.cc` are the main files for the server and client respectively.


## Send a file from the client to the server

In the server VM, at the `/vagrant/foggytcp` folder, run the server with the following command:
```bash
./server 10.0.1.1 3120 test.out
```

In the client VM, at the `/vagrant/foggytcp` folder, run the client with the following command:
```bash
./client 10.0.1.1 3120 src/client.cc
```

Now you have successfully transmitted the `client.cc` file from the client to the server, named as `test.out`.

# What to submit

## Codes

This checkpoint is about setting up the environment and understanding the code.
You do not need to modify the code for this checkpoint.
We hope that you can familiarize yourself with the submission procedure on Gradescope.

1. Modify any place in the `*.cc` or `*.h` (it can even be adding a new space).
2. Commit your code. If you're using VS Code, follow [this video](https://youtu.be/9cMWR-EGFuY?si=etqYwMOt5sz1QgCL&t=289) to commit the changes (from 4m49s to 6m22s).
3. Run the `submit.py` at the root of the project. It will generate a `submit.zip` file.
```
python submit.py
```
4. Submit the `submit.zip` file to Gradescope.

## Report

In the first report, you will need to follow the hypothesis-experiment-conclusion format.

Transmission time of
* Different bandwidth
* Different delay
* Different file sizes.