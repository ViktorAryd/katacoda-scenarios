Unfortunately, this tutorial doesn't always work. Firecracker requires something called KVM (Kernel Virtual Machine), which is a virtualization tool included in linux. The problem is that this feature is hardware dependent, and only some of Katacoda's servers seem to support it. Since a random host is used every time you load a Katacoda environment, there is no way to make sure KVM is supported.

There is unfortunately nothing that can be done about this, and to complete this tutorial you will simply have to refresh the page until you find a host where KVM is supported.

To check if the current host supports KVM, wait until the terminal is empty and run the following command:

`kvm-ok`{{execute}}

This will result in two lines telling you if KVM is supported. If the result tells you KVM acceleration can be used, then proceed to step 1. If not, reload the page and start from the beginning.
