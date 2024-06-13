

Develop with on a remove server with vscode

### Make sure you can ssh, take gcp vm as an example

* make sure a vm is running, say in gcp
* lets generate the ssh keypare

    ```
    ssh-keygen -t ed25519 -b 4096 
    # and give it a good name

    # then copy the public key
    cat ~/.ssh/id_ed25519_for_ssh.pub | pbcopy
    ```

* now lets add the public ssh to the vm, there are 2 ways
    * add to the specific vm, at edit vm
    * add to whole project and allow vm to take ssh keys from metadata, at the metadata page (by default, vm will take, unless you disallow it)
    
    * however, the ssh pub key value need to be changed a bit, when you generate you probably get:
        
        ```
        ssh-ed25519 jiberish <your-localname>@<your-local-machine>.local
        ```

        but the value you provide to google needs to be

        ```
        ssh-ed25519 jiberish <name-when-you-ssh-into-the-machine-via-ssh-on-web-page>
        ```

* finally, make things easier, lets create the ssh config file

    ```
    ➜  ~ cat ~/.ssh/config
    Host gcp-dev-vm   # anyname you think convenient
        User tomxuerjun   # name-when-you-ssh-into-the-machine-via-ssh-on-web-page
        HostName 35.198.200.65  # the external ip
        IdentityFile ~/.ssh/id_ed25519_for_ssh  # the PRIVATE keyfile we just generated
    ```

* now you are good to go:

    ```
    ➜  ~ ssh gcp-dev-vm 
    Welcome to Ubuntu 24.04 LTS (GNU/Linux 6.8.0-1008-gcp x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/pro
    ...
    ```

### At vscode side

* make sure remote-ssh extension is installed
* click the button left corner, find `connect to host`
* since we have a ssh config nicely, you will be able to just click, then you are!


### Clone code

* when you are in:
    * add your private key to like `~/.ssh/id_ed25519`
    * then `chmod 600 ~/.ssh/id_ed25519`
    * now you can git clone `git clone git@github.com:youname/yourrepo.git`
    * now the repo is cloned
    * click the file icon at navigation, then open folder, choose the repo you just cloned!, now your are remotely developping!

### devcontainer

* the configuration is difficult, lets 

