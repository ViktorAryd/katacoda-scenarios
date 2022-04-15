First off, we need to get Fireracker itself. We can do this in one of two ways. Either we get the binary itself, or clone the entire git repository and build the binary ourselves. To continue, complete one of these options and then move to step 3.

### Option 1: Clone The Repo and Build Binary

Clone the Firecracker Repository
`git clone https://github.com/firecracker-microvm/firecracker`{{Execute}}

Navigate to the firecracker root directory and then build the binary:

`tools/devtool build`{{Execute}}

### Option 2: Get The Binary

Use the following command to get the complete binary:



`release_url="https://github.com/firecracker-microvm/firecracker/releases"
latest=$(basename $(curl -fsSLI -o /dev/null -w  %{url_effective} ${release_url}/latest))
arch=`uname -m`
curl -L ${release_url}/download/${latest}/firecracker-${latest}-${arch}.tgz \
| tar -xz`{{Execute}}

