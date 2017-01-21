This is a demo Ansible playbook to deploy the Grails Petclinic app on a remote server.

# Pre-requisites

 * The controller (from which you'll run Ansible) must have Python 2.7 and Ansible 2.2 installed.
 * The target server must have Python installed. This cannot be done by Ansible. Run `sudo apt-get install python-minimal` and you're good to go!

 # Using the script

 ## Deployment

 The simplest way is to run the playbook and pass the target IP on the command line:

 ```
 ansible-playbook deploy-petclinic.yml -i '192.168.0.33,'
 ```

 Replace `192.168.0.33` with the IP of the machine on which you want to install the Grails app.

 Note the `,` comma which is necessary for Ansible to know this is an IP address as opposed to an inventory file.

 You can also configure an inventory file if you prefer.

 NB: The first execution can take time, especially the Gradle build as it needs to download all the dependencies.

## Rollback

The script allows to rollback to an earlier version of the code by passing the version parameter:

```
ansible-playbook deploy-petclinic.yml -i '192.168.0.33,' --extra-vars 'version=f4020df0cb114fea32f4ac792e947237f84ac61d'
```

The `version` parameter could be any tag or commit hash in the Github repo. Sadly the Petclinic app does not have tags so we will have to use commit hashes. A proper production project would be expected to tag its versions.
