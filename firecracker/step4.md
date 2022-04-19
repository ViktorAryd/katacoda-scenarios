We start it by sending one last HTTP request containing the API-command "InstanceStart":

`curl --unix-socket ./firecracker.socket -i \
  -X PUT 'http://localhost/actions'       \
  -H  'Accept: application/json'          \
  -H  'Content-Type: application/json'    \
  -d '{
      "action_type": "InstanceStart"
   }'`{{Execute}}

When running this command, you should receive one last 204 response, and text should start appearing in the first terminal window. If you instead recieve an empty response, and find an error message in the first terminal, then kvm is probably not supported in your environment. If you're running on katacoda, take another look at step one. If running locally, it might have to do with kvm permissions. 

Assuming you did recieve a 204 response, the mivroVM should now be up and running and ready to use!