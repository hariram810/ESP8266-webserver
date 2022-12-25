# ESP8266-webserver

![Screenshot (776)](https://user-images.githubusercontent.com/118633170/209475953-f05ff836-a9f9-4245-a851-88c2211ff33f.png)

If you have hard-time 3d printing stuff and other materials which i have provided in this project please refer the professionals for the help, [JLCPCB](https://jlcpcb.com/RNA) is one of the best company from shenzhen china they provide, PCB manufacturing, PCBA and 3D printing services to people in need, they provide good quality products in all sectors

[JLCPCB](https://jlcpcb.com/RNA)


Please use the following link to register an account in [JLCPCB](https://jlcpcb.com/RNA)

https://jlcpcb.com/RNA


Pcb Manufacturing

----------

2 layers

4 layers

6 layers

jlcpcb.com/RNA



PCBA Services

[JLCPCB](https://jlcpcb.com/RNA) have 350k+ Components In-stock. You don’t have to worry about parts sourcing, this helps you to save time and hassle, also keeps your costs down.

Moreover, you can pre-order parts and hold the inventory at [JLCPCB](https://jlcpcb.com/RNA), giving you peace-of-mind that you won't run into any last minute part shortages. jlcpcb.com/RNA


3d printing

-------------------

SLA -- MJF --SLM -- FDM -- & SLS. easy order and fast shipping makes [JLCPCB](https://jlcpcb.com/RNA) better companion among other manufactures try out [JLCPCB](https://jlcpcb.com/RNA) 3D Printing servies

[JLCPCB](https://jlcpcb.com/RNA) 3D Printing starts at $1 &Get $54 Coupons for new users

![Screenshot (774)](https://user-images.githubusercontent.com/118633170/209475981-1f8dc215-9c6f-4b2b-adfc-d0f476bbe843.png)


One of the most useful features of the ESP8266 is its ability to not only connect to an existing WiFi network and act as a Web Server, but also to create its own network, allowing other devices to connect directly to it and access web pages.

This is possible because the ESP8266 can operate in three modes: Station (STA) mode, Soft Access Point (AP) mode, and both simultaneously.

In STA mode, the ESP8266 obtains an IP address from the wireless router to which it is connected. With this IP address, it can set up a web server and serve web pages to all connected devices on the existing WiFi network.

Soft Access Point (AP) Mode
In Access Point (AP) mode, the ESP8266 sets up its own WiFi network and acts as a hub (just like a WiFi router) for one or more stations.

![Screenshot (775)](https://user-images.githubusercontent.com/118633170/209475984-a30825ba-7433-4872-940c-e865a91f6d7c.png)
![Screenshot (777)](https://user-images.githubusercontent.com/118633170/209475986-f5cce52a-03cc-469d-bec8-8f3d929f6fb2.png)


However, unlike a WiFi router, it does not have an interface to a wired network. So, this mode of operation is called Soft Access Point (soft-AP). Also, no more than five stations can connect to it at the same time.

Wiring LEDs to an ESP8266
Now that we understand the fundamentals of how a web server works and the modes in which the ESP8266 can create one, it’s time to connect some LEDs to the ESP8266 that we want to control via WiFi.

Begin by placing the NodeMCU on your breadboard, making sure that each side of the board is on a different side of the breadboard. Next, connect two LEDs to digital GPIO D6 and D7 using a 220Ω current limiting resistor.

It’s extremely simple. We’re going to control things by visiting a specific URL.

When you enter a URL into a web browser, it sends an HTTP request (also known as a GET request) to a web server. It is the web server’s responsibility to handle this request.

Assume you entered a URL like http://192.168.1.1/ledon into a browser. The browser then sends an HTTP request to the ESP8266. When the ESP8266 receives this request, it recognizes that the user wishes to turn on the LED. As a result, it turns on the LED and sends a dynamic webpage to a browser that displays the LED’s status as “on.” Quite simple, right?

![Screenshot (779)](https://user-images.githubusercontent.com/118633170/209475992-3b82e295-255a-4136-b87f-2be7e78b18c1.png)


Configuring the ESP8266 Web Server in Access Point (AP) mode
Let’s get to the interesting stuff now!

This example, as the title suggests, shows how to configure the ESP8266 Web Server in Access Point (AP) mode and serve web pages to any connected client. To begin, connect your ESP8266 to your computer and run the sketch. Then we will look at it in more detail.

#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>

/* Put your SSID & Password */
const char* ssid = "NodeMCU";  // Enter SSID here
const char* password = "12345678";  //Enter Password here

/* Put IP Address details */
IPAddress local_ip(192,168,1,1);
IPAddress gateway(192,168,1,1);
IPAddress subnet(255,255,255,0);

ESP8266WebServer server(80);

uint8_t LED1pin = D7;
bool LED1status = LOW;

uint8_t LED2pin = D6;
bool LED2status = LOW;

void setup() {
  Serial.begin(115200);
  pinMode(LED1pin, OUTPUT);
  pinMode(LED2pin, OUTPUT);
  
  After uploading the sketch, open the Serial Monitor at 115200 baud and press the RESET button on the ESP8266. If everything is fine, it will show the “HTTP server started” message.
  
 ![Screenshot (784)](https://user-images.githubusercontent.com/118633170/209476001-c58aedf9-5db5-4cfb-890d-f10ad09dec05.png


The sketch begins by including the ESP8266WiFi.h library. This library contains ESP8266-specific methods that we use to connect to the network. Following that, we include the ESP8266WebServer.h library, which contains some methods that will assist us in configuring a server and handling incoming HTTP requests without having to worry about low-level implementation details.

#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>
Because we are configuring the ESP8266 web server in Access Point (AP) mode, it will create its own WiFi network. So, we need to set the SSID, password, IP address, IP subnet mask, and IP gateway.

/* Put your SSID & Password */
Now we must write the handle_OnConnect() function, which we previously attached to the root (/) URL with server.on. We begin this function by setting the status of both LEDs to LOW (initial state of LEDs) and printing it on the serial monitor.

We use the send method to respond to an HTTP request. Although the method can be called with a number of different arguments, the simplest form requires the HTTP response code, the content type, and the content.

The first parameter we pass to the send method is the code 200 (one of the HTTP status codes), which corresponds to the OK response. Then we specify the content type as “text/html,” and finally we pass the SendHTML() custom function, which generates a dynamic HTML page with the LED status.

Following that, we create an object of the ESP8266WebServer library so that we can access its functions. The constructor of this object accepts as a parameter the port to which the server will be listening. Since HTTP uses port 80 by default, we’ll use this value. This allows us to connect to the server without specifying the port in the URL.

![Screenshot (785)](https://user-images.githubusercontent.com/118633170/209476007-59f439b1-c288-4680-b758-f6d65081f784.png)


// declare an object of ESP8266WebServer library
ESP8266WebServer server(80);
Next, we declare the NodeMCU’s GPIO pins to which LEDs are connected, as well as their initial state.

uint8_t LED1pin = D7;
bool LED1status = LOW;

uint8_t LED2pin = D6;
bool LED2status = LOW;
Inside Setup() Function
In the setup function, we configure our HTTP server. First, we establish a serial connection for debugging purposes and configure the GPIO pins to behave as an OUTPUT.

Serial.begin(115200);
pinMode(LED1pin, OUTPUT);
pinMode(LED2pin, OUTPUT);
Then, we configure a soft access point to create a Wi-Fi network by providing an SSID, password, IP address, IP subnet mask, and IP gateway.

WiFi.softAP(ssid, password);
WiFi.softAPConfig(local_ip, gateway, subnet);
delay(100);

![Screenshot (785)](https://user-images.githubusercontent.com/118633170/209476015-ba5fe417-9b1b-4d28-a3d5-496c3f6d9a6b.png)


To handle incoming HTTP requests, we must specify which code should be executed when a specific URL is accessed. For this, we use the .on() method. This method accepts two parameters: a relative URL path and the name of the function to be executed when that URL is visited.
