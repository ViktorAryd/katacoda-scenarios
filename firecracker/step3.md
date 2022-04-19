Now it's time to actually start Firecracker itself. To do this, we first need to run the binary we just downloaded:

`./Firecracker --api-sock ./firecracker.socket`{{Execute}}

The argument provided specifies where to place the socket file, which we will soon use to communicate with the microVM.

Now Firecracker should be running, and to continue we need to open a second terminal window. In this new terminal window, make sure you're in the root folder, and that you can see the binary and the socket file.

`pwd
ls`{{Execute}}

## Configuration needed to launch microVM 

Firecracker needs a separate linux kernel and root file system to function. To ensure compatibility, we use the files provided by AWS in the set up instructions for Firecracker (This takes a few seconds):

``url="s3.amazonaws.com/spec.ccfc.min/img/quickstart_guide/`uname -m`"
curl -fsSL -o "hello-vmlinux.bin" "${url}/kernels/vmlinux.bin"
curl -fsSL -o "hello-rootfs.ext4" "${url}/rootfs/bionic.rootfs.ext4"``{{Execute}}


Then we send a HTTP PUT request to the socket file we created in the last step. This request contains the path to the kernel we just downloaded:

`path=$(pwd)"/hello-vmlinux.bin"
curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/boot-source'   \
  -H 'Accept: application/json'           \
  -H 'Content-Type: application/json'     \
  -d "{
        \"kernel_image_path\": \"${path}\",
        \"boot_args\": \"console=ttyS0 reboot=k panic=1 pci=off\"
   }"`{{Execute}}


You should receive a 204 success response, indicating everything went as expected. A similar HTTP request is then required containing the path to the root file system:

`path=$(pwd)"/hello-rootfs.ext4"
curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/drives/rootfs' \
  -H 'Accept: application/json'           \
  -H 'Content-Type: application/json'     \
  -d "{
        \"drive_id\": \"rootfs\",
        \"path_on_host\": \"${path}\",
        \"is_root_device\": true,
        \"is_read_only\": false
   }"`{{Execute}}


Another 204 response tells us that the Firecracker microVM is configured and ready to start. 