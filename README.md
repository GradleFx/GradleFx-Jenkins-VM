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

install gradle & git plugin

Generate an ssh key on the jenkins user: https://help.github.com/articles/generating-ssh-keys

reboot vagrant box

Go to http://192.168.111.222:8080/