At this point our Firecracker microVM is ready to be started. But in order to be able to see some communication from it in our local interface (terminal 2 in Katacoda) we will use an additional API call to setup "metrics". This will show us a number of statistics for our virtual machine.

First, we create a file to which the virtual machine will store the metrics. Make sure that you are in Terminal 2 and then simply create the file with "touch".

`touch metrics.file`{{execute}}

After this we will make an HTTP API request to the /metrics path, setting up the virtual machine so that it will know where to output the metrics. 

`curl --unix-socket ./firecracker.socket -i \
    -X PUT 'http://localhost/metrics' \
    -H 'accept: application/json' \
    -H 'Content-Type: application/json' \
    -d '{
             "metrics_path": "metrics.file"
    }'`{{execute}}

If this call returns a 204 response then everything should be in order and we can start the virtual machine. We start it by sending another HTTP request containing the API-command "InstanceStart":

`curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/actions'       \
  -H  'Accept: application/json'          \
  -H  'Content-Type: application/json'    \
  -d '{
      "action_type": "InstanceStart"
   }'`{{Execute}}

When running this command, you should receive one last 204 response, and text should start appearing in the first terminal window. If you instead recieve an empty response, and find an error message in the first terminal, then kvm is probably not supported in your environment. If you're running on katacoda, take another look at step one. If running locally, it might have to do with kvm permissions. 

Assuming you did recieve a 204 response, the microVM should now be up and running and ready to use!