vagrant up
vagrant ssh

sudo apt-get update
sudo apt-get install default-jre
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
sudo apt-get install git
ssh -T git@github.com

sudo cp -r /vagrant/jobs /var/lib/jenkins
sudo chown -R jenkins:jenkins /var/lib/jenkins/jobs/GradleFx\ Develop\ Build/
sudo chown -R jenkins:jenkins /var/lib/jenkins/jobs/GradleFx\ Testbed\ Build/
sudo mkdir /var/lib/jenkins/.gradle
cp gradle.properties /var/lib/jenkins/.gradle/
sudo chown -R jenkins:jenkins /var/lib/jenkins/.gradle/

sudo apt-get install vnc4server
sudo apt-get install ant
sudo apt-get install unzip
mkdir /var/lib/jenkins/sdks
cd /var/lib/jenkins/sdks
wget http://apache.belnet.be/flex/4.13.0/binaries/apache-flex-sdk-4.13.0-bin.tar.gz -O apache-flex-sdk-4.13.0-bin.tar.gz
tar -xvzf apache-flex-sdk-4.13.0-bin.tar.gz
copy flexunit 4.1.0-8 libraries to ./flexunit
wget http://fpdownload.macromedia.com/pub/flashplayer/updaters/11/flashplayer_11_sa_debug.i386.tar.gz -o flashplayerdebugger.tar.gz
tar -zxvf flashplayerdebugger.tar.gz
tar -zxvf jdk-8u11-linux-i586.gz
cd /var/lib/jenkins/sdks/apache-flex-sdk-4.13.0-bin
ant -f installer.xml -Dair.sdk.version=2.6
mkdir -p frameworks/libs/player/11.1/
wget http://download.macromedia.com/get/flashplayer/updaters/11/playerglobal11_1.swc -O frameworks/libs/player/11.1/playerglobal.swc
cd frameworks
ant thirdparty-downloads
cp ide/flashbuilder/config/* frameworks/
add the following to /var/lib/jenkins/.bash_profile:
	export JAVA_HOME=/var/lib/jenkins/sdks/jdk1.8.0_11
	export FLEX_HOME=/var/lib/jenkins/sdks/apache-flex-sdk-4.12.1-bin
	export CUSTOM_FLEX_HOME=/var/lib/jenkins/sdks/apache-flex-sdk-4.12.1-bin
	export FLEXUNIT_HOME=/var/lib/jenkins/sdks/flexunit
	export FLASH_PLAYER_EXE=/var/lib/jenkins/sdks/flashplayerdebugger

install gradle, git & xvnc plugin
Enable xvnc for the GradleFx Testbed Build (but turn off 'Create a dedicated Xauthority file per build?')

sudo su jenkins
vnc4server
Generate an ssh key on the jenkins user: https://help.github.com/articles/generating-ssh-keys

reboot vagrant box

Go to http://192.168.111.222:8080/



# Fixing problems

## Vagrant forgets the existing box and creates a new one:
solution: http://paulfreeman.me.uk/notes-to-self/point-vagrant-at-correct-virtualbox-vm-when-it-forgets-it-and-creates-a-new-instance