First off, we need to get Firecracker itself. We can do this in one of two ways. Either we get the binary itself, or clone the entire git repository and build the binary ourselves. To continue, complete one of these options and then move to step 3.

### Option 1: Get Binary (1 min)

Use the following command to get the complete binary:

``url="https://github.com/firecracker-microvm/firecracker/releases"
latest=$(basename $(curl -fsSLI -o /dev/null -w  %{url_effective} ${url}/latest))
arch=`uname -m`
curl -L ${url}/download/${latest}/firecracker-${latest}-${arch}.tgz \
| tar -xz``{{Execute}}

Rename the binary and move it to the root folder for the next step in the tutorial:

`mv release-${latest}-$(uname -m)/firecracker-${latest}-$(uname -m) Firecracker`{{Execute}}

### Option 2: Clone Repo and Build Binary (4-5 min)
This process takes a while, so this is mainly recommended if you intend to contribute to the project yourself, or want to explore the project more thoroughly.

First, clone the Firecracker Repository:
`git clone https://github.com/firecracker-microvm/firecracker`{{Execute}}

Navigate to the firecracker root directory and build the binary:

`tools/devtool build`{{Execute}}

The firecracker binary can be found under   `firecracker/build/cargo_target/x86_64-unknown-linux-musl/debug/` Navigate to the root folder, then move it there and rename it for the next step of the tutorial:

`mv firecracker/build/cargo_target/x86_64-unknown-linux-musl/debug/firecracker Firecracker`{{Execute}}