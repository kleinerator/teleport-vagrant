# teleport-vagrant

Set up two nodes to test out teleport.

add `10.100.198.200 auth-proxy` to your /etc/hosts file

## Requirements

* Vagrant
* VirtualBox

## Post Deployment

You will need to create a user.

`sudo tctl users add vagrant`

This will give you a link to go to. You will have to bypass SSL Errors.

If you want to use a different use, the user needs an account on the client.
