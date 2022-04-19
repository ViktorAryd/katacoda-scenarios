Now it's time to actually start Firecracker itself. To do this, we first need to run the binary we just downloaded:

`./Firecracker --api-sock ./firecracker.socket`{{Execute}}

The argument provided specifies where to place the socket file, which we will soon use to communicate with the microVM.

Now Firecracker should be running, and to continue we need to open a second terminal window. In this new terminal window, make sure you're in the root folder, and that you can see the binary and the socket file.

`pwd
ls`{{Execute}}

## (WIP) Commands to Configure & Start VM

Downloading linux kernel and root file system:

``url="s3.amazonaws.com/spec.ccfc.min/img/quickstart_guide/`uname -m`"
curl -fsSL -o "hello-vmlinux.bin" "${url}/kernels/vmlinux.bin"
curl -fsSL -o "hello-rootfs.ext4" "${url}/rootfs/bionic.rootfs.ext4"``{{Execute}}


HTTP put request to socket file containing path to Linux kernel we just downloaded.

`kernel_path=$(pwd)"/hello-vmlinux.bin"
curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/boot-source'   \
  -H 'Accept: application/json'           \
  -H 'Content-Type: application/json'     \
  -d "{
        \"kernel_image_path\": \"${kernel_path}\",
        \"boot_args\": \"console=ttyS0 reboot=k panic=1 pci=off\"
   }"`{{Execute}}


HTTP put request to socket file containing path to root file system we just downloaded.

`rootfs_path=$(pwd)"/hello-rootfs.ext4"
curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/drives/rootfs' \
  -H 'Accept: application/json'           \
  -H 'Content-Type: application/json'     \
  -d "{
        \"drive_id\": \"rootfs\",
        \"path_on_host\": \"${rootfs_path}\",
        \"is_root_device\": true,
        \"is_read_only\": false
   }"`{{Execute}}


HTTP put request to start Firecracker VM.

`curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/actions'       \
  -H  'Accept: application/json'          \
  -H  'Content-Type: application/json'    \
  -d '{
      "action_type": "InstanceStart"
   }'`{{Execute}}