Before you go, there are a few other things you should know. This tutorial goes over the basics of Firecracker, but there are some other things which might be important if you want to use it in a business setting. 

For some more information about this you can check out the Firecracker repository on GitHub, for example these reccomentations: https://github.com/firecracker-microvm/firecracker/blob/main/docs/prod-host-setup.md

One thing to at least mention is the Jailer binary. This can be found in the same directory which contained the Firecracker binary in step 2. Jailer is included with every Firecracker release, and is crucial for security purposes. For example, it ensures the isolation of the microVM and limits resource consumption. 

Now all that remains is to shut the microVM down. We do this with another HTTP request:

`curl --unix-socket ./firecracker.socket -i \
    -X PUT "http://localhost/actions" \
    -d '{ "action_type": "SendCtrlAltDel" }'`{{Execute}}

Remember to delete the socket file if you want to relaunch Firecracker. Normally this file should be placed in the /tmp directory.