# demo1

pipeline {

agent any

stages {

stage('Checkout') {

steps {

git branch: 'main', 
url:
'https://github.com/cmritsarada/exp6.git' /

}

}

stage('Build') {
steps {

sh 'mvn clean package'
}
}
stage('Test') {
steps {
sh 'mvn test'
}
}
}
}

#7
#!/usr/bin/python
from ansible.module_utils.basic import AnsibleModule
def walk():
module_args = dict(name=dict(type='str', required=True))
module = AnsibleModule(argument_spec=module_args)
result = {"changed": False, "message": f"Welcome, {module.params['name']}!"}
module.exit_json(**result)
if __name__ == '__main__':
walk()

To come out of the library directory, type the below command
cd ..

61 | Page Department of CSE

e. To give execute permission for the module, type the below command
chmod +x library/firstmodule.py

gedit secondpb.yml

3. Add the following YAML content:

- - -
- name: Ansible with one module
hosts: localhost
gather_facts: no
tasks:
- name: Welcome friends
firstmodule:
name: “Ansible”
register: result
- name: Show message
debug:
msg: “{{result.message}}”



#8
pipeline
{
agent any
stages
{
stage('Checkout')
{
steps
{
git branch: 'main', url: 'https://github.com/cmritsarada/m2.git' // Replace with your repository URL
}
}

stage('Build')
{
steps
{
// Use 'mvn clean package' for Maven or 'gradle build' for Gradle
sh 'mvn clean package'
}
}

65 | Page Department of CSE

stage('Test')
{
steps
{
// Run unit tests using Maven or Gradle
sh 'mvn test'
}
}

stage('Archive Artifacts')
{
steps {
archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
}
}

stage('Deploy')
{
steps{
sh """
export ANSIBLE_HOST_KEY_CHECKING=False
ansible-playbook -i hosts.ini deploy.yml
--extra-vars='ansible_become_pass=exam@cse'

"""
//enter student password above
}

}

}

}

1. Open Your Text Editor and create a file called deploy.yml:
2. nano deploy.yml
3. Enter the Following YAML Content:
4.
---
- name: Deploy Artifact to Localhost
hosts: localhost
tasks:
- name: Copy the artifact to the target location
become: true
become_user: student
become_method: su
copy:
src: "/var/lib/jenkins/workspace/exp8/target/my-app-1.0-SNAPSHOT.jar"
dest: "/home/student/t.jar"
