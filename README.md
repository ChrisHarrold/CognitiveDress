# CognitiveDress



This project using a raspberry pi 3, IBM Watson's speech to text service, a usb microphone, ws2801 LED strips and a tulle skirt highlights how digital objects can be controlled with the human voice.  Cognitive technology interprets the speech, converts it to text, and code is executed to change the colors of the LED strip. 

 # Materials
 
 Raspberry pi 3 (can be found in many places.  Mine was purchased here: https://www.adafruit.com/product/3055)
 
 Micro SD Card with NOOBS (https://www.adafruit.com/product/3259)
 
 Mini USB Microphone (https://www.amazon.com/gp/product/B00IR8R7WQ/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1)
 Female to Male jumper wires (https://www.amazon.com/Multicolored-Breadboard-Dupont-Jumper-wires/dp/B073X7P6N2/ref=sr_1_1_sspa?ie=UTF8&qid=1515098517&sr=8-1-spons&keywords=female+to+male+jumper+wires&psc=1)
 
 ws2801 LED strip (https://www.amazon.com/Led-World-Digital-Waterproof-Addressable/dp/B012W5YURY).  
 ****Note... there are various types of LED strips.  This code was designed to work with ws2801.  To verify you have the correct kind check the pins.  You should see 4 pins marked 5V, SI, CK, and GND. 
 
# Getting Started with Your Pi
(Note this section of instructions should be credited to IBM research and the instructions for setting up a TJBot)

Raspberry Pi is similar to a full computer, which means you need a monitor, mouse, and keyboard for it. If you have a TV around, you can connect your Pi to your TV via a HDMI cable. Insert the SD card in the Pi, turn the Pi ON and follow the instructions on screen to complete the installation of the operating system. If you have problems setting up your Pi, you can troubleshoot here: https://www.raspberrypi.org/learning/hardware-guide/.


Install Packages

Open a terminal application on the Pi and execute the following commands to install the latest version of Node.js and npm (Node Package Manager). You need these packages later to run your code.

curl -sL http://ibm.biz/tjbot-bootstrap | sudo sh -

This process may take several minutes.  When prompted to make selections always select the default (indicated by capital letters such as Y/n). 

Enable SPI by clicking on the Raspberry Pi icon on the top left corner of the screen, selecting preferences, then Raspberry Pi configuration. Click the interfaces tab and enable SPI.  Click ok.

Install the hardware SPI control module for python. Start by updating the system, installing the development tools and pip with the following commands:

sudo apt-get update
sudo apt-get install python-dev
sudo apt-get install python-pip
sudo pip install spidev

#Connect your LED Strip to the raspberry pi and test your python code to control the lights

On your pi, Connect pin 6 to GND on the LED strip, pin 19 to data (SI), pin 23 to clock (CK) and pin 2 to 5v. Note on the LED strip there is an arrow which indicates the direction of data flow.  We are providing data to the strip and want to start at the base of the arrow, not the end the tip of the arrow is pointing to. 


Once your connections are made, connect power to the pi. Clone this repository with the command

git clone https://github.com/ericareuter/CognitiveDress.git

Change into the directory (CognitiveDress) that was just created by the colone with the command

cd CognitiveDress

Test to ensure your lights are reponding as expected by running the python code included in the repository.  Run the command

sudo python changecolor.py

Your lights should turn blue then fade off

## Node-RED... adding the speech to text functionality

Follow the instructions in the videos found on this page (https://medium.com/@jeancarlbisson/setting-up-your-tjbot-to-use-node-red-df94ff94a114) to set up Node-RED with TJBot modules that will be used to listen for commands to change the light colors.  You may skip the 3rd video. 

We need to install one more node to execute python code within Node-RED.  To do so go to your Node-RED session running in the browser. Click the menu in the top right corner, and select "Manage Palette". Click the install tab and type the word python. Click to install the first option "node-red-contrib-python-function", and click the install prompt once it appears.  Close this window and scroll through your nodes.  You should now see a node entitled "python function" listed in your functions. 

You are now ready to import the completed Node-RED flow to run this project. Click on the menu once again and Import from the Clipboard.  Go to the Node-RED flow file in your CognitiveDress directory, select all and copy.  Paste this content into the clipboard and click import.  The flow is imported.  

Enter your watson speech to text credentials by clicking on the pencil to the right of the Bot field and filling in the user name and password. If you have not configured a watson speech to text service, instructions are below.  You may skip this section if you already have a service provisioned. 

---
In this step, we help you get API access to the Watson Speech to Text. Let's start with creating a Speech to Text instance on IBM Cloud If you don't have a IBM Cloud account, follow the instructions (https://developer.ibm.com/predictiveanalytics/wp-content/uploads/sites/48/2015/09/Getting-Started-with-Watson-Services-on-Bluemix.pdf) to create a free trial.

When creating your service you may leave the default values and select 'Create'.

Click on 'Sevice Credentials' on the left menu and copy your credentials into the the user name and password fields for the listen node.

---

Once your credentials are entered, ensure your microphone is plugged in to the raspberry pi and click "Deploy" in Node-RED.  You can start the flow and prompt your pi to listen to a color by clicking on the small box to the left of the start listening node, and click the small box to the left of stop listening to stop.  Colors will change when spoken.  Currently this project is programmed to recognize blue, white, yellow, red, rainbow and green.  

Enjoy your new colorful project!





 
