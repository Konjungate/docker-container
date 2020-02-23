# Konjungate docker-container
## How to run the Konjungate-qt GUI on a Docker Container

**Replace these strings in step 1. with the values that apply for your system:**
- PATH-TO-XAUTHORITY-FILE: location of the Xauthority file (usually /home/$user/.Xauthority)
- PATH-TO-LOCAL-WALLET-DIRECTORY: a directory for your local wallet

**1. Create a container**\
`docker create --name konjungate-qt \`\
`        -e DISPLAY=$DISPLAY \`\
`        -e XAUTHORITY=/tmp/Xauthority \`\
`        -v PATH-TO-XAUTHORITY-FILE:~/.Xauthority \`\
`        -v /tmp/.X11-unix:/tmp/.X11-unix \`\
`        -v PATH-TO-LOCAL-WALLET-DIRECTORY:/root/.Konjungate \`\
`        -v /etc/machine-id:/etc/machine-id \`\
`        thesix/konjungate-qt`
        
**2. The output will be the container ID. If you forgot it, then run `docker ps` and get the container ID of the thesix/konjungate-qt image. Copy this string and replace it with $containerID in the following command to allow forwarding from our container to xhost:**\
``xhost +local:`docker inspect --format='{{ .Config.Hostname }}' $containerID``

**3. Start the container**\
`docker start konjungate-qt`
