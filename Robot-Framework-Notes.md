# Setting up Robot Framework

## Install PIP & Robot
```
sudo apt install python3-pip lsscsi
sudo pip3 install robotframework
sudo pip3 install robotframework-sshlibrary
```
## (Optional) Install VSCode
```
sudo snap install --classic code
```
## Other libraries needed to be installed on the Raspberry Pi
```
sudo apt install genisoimage sshpass
```

# Running tests
To run the test suite, run the following commands:
```
git clone https://github.com/piscsi/piscsi.git
cd piscsi/test/robot
robot ./
```
If everything works, you should see something like this:
[[images/robot.png]]

# Troubleshooting
If everything fails and the error message is "timeout: timed out", the IP address of the raspberry pi could be wrong. Check test/robot/Resources/rascsi_utils.resource and linux_services.resource to make sure that Rascsi_Host is set appropriately.

