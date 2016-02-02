# game-on-room

Installation prerequisites
Docker - You will need Docker on your host machine to create a docker image to be pushed to IBM Bluemix Containers

Log in to Bluemix
To build a room as a container in Bluemix, you will need to log in to Bluemix to push to IBM Containers.
	1.	Log in with the command: `cf ic login` 

Make sure you have an available IP
<Copy this from HDS>



Update the server.js file with the API Key, User ID, and Container IP.
	1.	Go to https://game-on.org/ and click **Play**
	2.	Select any authentication method to log in with your username and password for that type.
	3.	Click the **Edit Profile** button(the person icon) at the top right.
	4.	You should now see the Id and ApiKey at the bottom of the page.  You may need to refresh the page to generate the ApiKey.

Update server.js file
The server.js file contains information about the new room and your user credentials. The user credentials must be set manually. Other variables may be set automatically if the container was built using the Deploy to Bluemix button.

	⁃	**gameonAPIKey** - Use the ApiKey value from the game-on.org user settings page.
	⁃	**gameonUID**  - Use the Id value from the game-on.org user settings page..
	⁃	**endpointip** - Use the IP requested or retrieved from earlier steps.
	⁃	**port** - The default value is 3000. This port must be opened when running the container.

Build the Docker container locally
	1.	Start Docker to run Docker commands. e.g. with the Docker QuickStart Terminal.
	2.	In the folder, build the container using run `docker build -t registry.ng.bluemix.net/<your_namespace>/<imageName> .`
	3.	To verify the image is now created, you can run `docker images`

Push and run on Bluemix
	1.	Make sure you are logged in with the `cf ic login` command.
	2.	Push the container to Bluemix using the command `docker push registry.ng.bluemix.net/<your_namespace>/<imageName>` using the same image name you used to create the local container.

Run the container on Bluemix
	1.	Use the following command to run the container: `cf ic run -p <port>:<port> -d registry.ng.bluemix.net/<your_namespace>/<imageName>` using the same image name you used to create the local container and port 3000 as the open port as set for the port variable in the server.js.
	2.	With the resulting container ID, use that value to bind to the IP you got earlier with the command `cf ic ip bind <IP> <Container ID>`

Accessing a running container
To edit a file on a running container, you can log in to the container with the command `cf ic exec -it <Container ID> /bin/bash`
The container has been created with vim to allow editing. You may need this to edit the files in /usr/src/app.
To start the room run `node server.js &`
