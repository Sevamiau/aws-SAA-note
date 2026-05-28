### EC2 User Data 

1.It is possible to bootstrap our instance using an EC2 User Data script.
2.bootstraping means launching commands when a machine starts
3.That script only run once at the instance first starts
4.EC2 user data is used to automate boot tasks such as:
    -Installing updates
    -Installing Software
    -Downloading common files from the internet
    -Anything you can think of 
5.The EC2 User Data script runs with the root user.
