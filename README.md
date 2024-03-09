# Smart-Irrigation-System

Protocol: 

In our study, we utilized the MQTT protocol to establish communication between the various sensors and the central hub (Raspberry Pi). The MQTT broker acted as a mediator, receiving data from the sensors and forwarding it to the appropriate subscriber. The subscriber, in this case the Raspberry Pi, would then process and store the data for further analysis.

A lightweight publish-subscribe system is MQTT (Message Queuing Telemetry Transport)[28] is used for the communication for our proposed model. It is often used in IoT (Internet of Things) and M2M (machine-to-machine) communication and is designed to be used on unreliable or high-latency networks. This protocol is a Publish-Subscribe model. The Publisher publishes the data and the subscriber receives the message, with the help of a broker [29]. This broker is responsible for receiving the requests from the clients and responding to them with the appropriate messages. The Publisher only publish the data. It has no work processing the request from the clients. TLS is suggested by the MQTT standard as a transport alternative to protect communication using port 8883. (secure-MQTT) [30]. The architecture of the MQTT protocol is shown below in Figure 1.


Figure 1: MQTT protocol


The reason we are using the MQTT protocol is that it is 74 times faster than HTTP [31].   


System Architecture:


Figure 2: Architecture of Proposed System

In the above figure 2, the system architecture, of the proposed system is shown. The water motor is designed to switch on and switch off by ESP32 or Node MCU using a relay by sensing the data from the Ultrasonic liquid level sensor. ESP32 or node MCU is connected to the microcontroller or Raspberry Pi using MQTT protocol. The Ultrasonic sensor will be sending the sensed data to the Raspberry Pi using ESP32 via an MQTT broker. The proposed system consists of three components. The first component consists of sensors that collect the data. The second component consists of processing the data frequently in the NODE RED platform. The third component consists of an MQTT broker along with a user interface which will be displaying the data sensed and that will be displayed to the user.

The first component consists of a sensor (DHT11, Tensiometer, BH1750, potentiometric pH meter, and Ultrasonic liquid level sensor), that will sense the data. In the second section, the Raspberry pi is will be collecting the data published by the sensors using Pub-Sub communication. Data originates from publishers who transmit it to topics managed by brokers. The consumers are unknown to publishers. Consumers subscribe to topics managed by brokers and receive data from publishers when the broker receives it. The broker disseminates the data to all subscribed consumers for a given topic. The Raspberry Pi and the users will be the subscribers. The data processed by the sensors are analyzed in the NODE RED platform, where the model is developed to make its decisions. 

The third component in the system connects the ESP32 or Node MCU to the MQTT broker. In this study, broker.hivemq.com is used to be an MQTT broker for communication. Arduino IDE is used to program the ESP32 or Node MCU to collect the data and publish it in Node-Red. So, whenever the water level goes down below the threshold value, the system switches on the water motor and the user will be getting a notification about switching the motor. The user can manually operate the water motor as well. The user can also view the data sensed on his web page, to which he is subscribed.



Figure 3: Connection of sensors to Raspberry Pi

The research work presented in this study utilizes various IoT devices for data collection from sensors installed in an agricultural field. The sensors used include DHT11, Tensiometer, BH1750, potentiometric pH meter, and Ultrasonic liquid level sensor. The data collected from these sensors is used for monitoring the environmental conditions of the field.

The data collection process is divided into several steps. In Step 1, the sensors are installed in the field. In Step II, data is collected from some of the sensors on a daily basis (pH, Sunlight index) while the others on a frequent basis (Temperature, Soil moisture, Water level).

The collected data is then sent to the server through ESP32/Node MCU using MQTT protocol to the Raspberry Pi in Step III. In Step IV, the collected data is processed in the Raspberry Pi using some functions. The final action on the water motor and water flow device can be made by the combined result of both the user and the developed model.

Finally, in Step V, the user is notified accordingly of any necessary actions or changes. The overall architecture of the system is shown in Figure 3, where the sensors connect to Node-Red using the MQTT protocol to Raspberry Pi.


Process Flow:

The real working model was illustrated in Figure 4 below. 


Figure 4: Developed model in Node-Red

The DHT11 sensor senses the real-time temperature and humidity of a particular area and updates the data in the cloud every 4 hours. The Tensiometer or water moisture sensor will be sensing the moisture content of the soil and updates the same in the cloud every 8 hours. The BH1750 sensor will be sensing the sunlight index, and push the data into a function where it will return whether to switch on the insecticides or not. The function for this sunlight index will be activated every 6 hours as shown in Figure 5 below. 


Figure 5: Flow diagram for insecticides

The potentiometer pH meter will be responsible for updating and sending notifications to the end user about the pH of the soil. The data sensed by this sensor will pass through a function, where it be sending a notification to the user about the fertility of the soil as shown in Figure 6.


Figure 6: Flow diagram for pH sensor

The ultrasonic liquid level sensor is responsible for updating the level of water in the field. The data collected by this sensor passes through a function. This function will be returning a value (either 1 or 0, 1 means ON and 0 means OFF) to the relay module. If the relay module gets switched ON the user will be notified that the water motor is switched ON. The function is designed in such a way that, if the level of water is below 20%, it will be switched on for 8 hours and if the water level is between 50% to 60%, it will be switched on for 4 hours and of the water level is above 90%, the function will be returning 0, which means the relay will be in OFF state. This process will continue till the harvest of the crop. The ultrasonic liquid sensor is also responsible for letting the water flow down the field. Another function will be checking whether the water level is up to the threshold or not. This function will be returning 1, if the per cent of water is above 95% and below anything, it will be returning 0 (Zero). Figure 7 below illustrates the processes of switching the water motor and solenoid valve.

Figure 7: Flow diagram for water level sensor and solenoid valve

The camera module captures the images of the crops and process the image and sends the notification to the user according to the features it recognizes. If the processed image of the crop is not matured enough, it will be returning 0. The model will be returning 1 if the image of the crop is matured enough. It will be returning 2 if the field can be stooped irrigating. It will be returning 3 if the crop is ready to harvest as shown in Figure 8. This cycle repeats every 15 days. Our developed model is developed using CNN in a Python environment.

Fig 8: Flow chart for image reorganization of crops

The developed system also gives the user the flexibility to wireless(ly) switch on and off the insecticides, water motor and solenoid valve according to the conditions. 


Results:


Figure 8: User Interface to monitor the output of the sensed data

The smart irrigation system is implemented in agricultural lands. As shown in Figure 8, the Temperature, moisture, soil moisture, sunlight intensity, pH of the soil and water level is displayed in the Monitor Group. In the Control Group, we can monitor the controls of Auto-switching of the Water motor, water flow and insecticides. Along with that, the developed model is having switches for manual operating of the Water motor, water flow and insecticides.

With the help of this advanced system, We have been able to regulate both the volume of water pushed and the motor according to the field's water level. The pump is activated automatically when the water level falls below the predefined threshold. In the event of a mistake, the motor may be operated manually via the app. The system records and updates all sensor readings in real time on the cloud, and the data can be accessed at any time through the specified URL.
