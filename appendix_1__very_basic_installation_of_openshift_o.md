# Appendix 1 – Very basic Installation of Openshift on RHELFollow the following steps: {#appendix-1-very-basic-installation-of-openshift-on-rhelfollow-the-following-steps}

sudo yum repolist all

sudo yum-config-manager --enable rhui-REGION-rhel-server-extras

sudo yum install docker docker-registry

cd /etc/sysconfig/

sudo vi docker

**change the line

# INSECURE_REGISTRY=&#039;--insecure-registry&#039;

to

INSECURE_REGISTRY=&#039;--insecure-registry 172.30.0.0/16&#039;

DON&#039;T FORGET TO UN-COMMENT

and save

sudo systemctl start docker

sudo systemctl status docker

***Install Client tools - followed &quot;Installing and Running an All-in-One Server&quot; here: https://docs.openshift.org/latest/getting_started/administrators.html

cd ~

sudo yum install wget

sudo wget https://github.com/openshift/origin/releases/download/v1.5.0-alpha.2/openshift-origin-client-tools-v1.5.0-alpha.2-e4b43ee-linux-64bit.tar.gz

sudo tar xzvf openshift-origin-client-tools-v1.5.0-alpha.2-e4b43ee-linux-64bit.tar.gz

sudo mv openshift-origin-client-tools-v1.5.0-alpha.2+e4b43ee-linux-64bit oc-cli-tools

sudo vi ~/.bash_profile

***make the changes save and exit

PATH=$PATH:/home/ec2-user/oc-cli-tools

source ~/.bash_profile

*** check new location is on the path

echo $PATH

***Start Openshift – replacing with your hostname and IP

sudo /home/ec2-user/oc-cli-tools/oc cluster up --public-hostname=**_&lt;your RHEL host&gt;_ **--routing-suffix==**_&lt;your RHEL IP&gt;_**.xip.io

***Should see something like: You are logged in as:

User: developer

Password: developer

***Web console. Can login as developer/developer.

https://**_&lt;your host&gt;_**:8443