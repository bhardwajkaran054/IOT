# IOT

# Control Home appliances via Google Assistant 

Requirements:
----------------------
NodeMCU
Arduino IDE
Blynk Android App

1. Open Arduino IDE and Install Blynk libraries (Tools Menu > Manage Libraries > Search "Blynk" & Install) - Adding Blynk Library in Arduino IDE
2.1 Add this link to File Menu > Preferences > Additional Boards Manager URLs: "http://arduino.esp8266.com/stable/package_esp8266com_index.json" - Adding esp8266 Board to Arduino IDE
2.2 Add Tools Menu > Board > Boards Manager > Search "esp8266" and Install
3.1 Goto File Menu > Examples > Blynk > WiFi Boards > NodeMCU - Blynk code for NodeMCU
3.2 Select proper "Board" & "Port" from Tools Menu, Enter Wifi SSID & Pass, Enter proper Token Auth (Get from Blynk Android App) and Upload the Code  to esp8266 NodeMCU board.
4. Install "Blynk" App in Android and "Create new App" Copy the generated "Token Auth" and Paste to code, select button and set property to PIN: GP16 (NodeMCU BuiltIn LED)

Check, it's working or not.

After this Open IFTTT in web browser create account and "Create new Applet" goto "Create" Menu in IFTTT
1. "IF+ThisThenThat" Click on "this" and Search "Google Assistant" and fill all the fields.
   NOTE: Make sure use your correct Google Email ID while sync Google Assistant
2. Then after this Click on "That" and Search "Web Hook" and fill all the fields as follow:
    a. URL: <Blynk_Cloud_IP>/<Auth_Token_Generated_by_Blynk>/update/<Digital_Pin>
            e.g. "http://188.166.206.43/U2voAGjGdf0KSlI2iAg8Mv1TAp2ZNwUp/update/D16"
      NOTE-1: For Blynk Cloud IP ping "ping blynk-cloud.com" on Command Prompt and copy IP 
      NOTE-2: If you are using Arduino IDE to code NodeMCU then check PIN configuration of NodeMCU to map Arduino IDE
              for e.g. NodeMCU D0 -> GPIO16 BUT!!! Instead of GPIO16 you have to write D16 in WebHook so
              NodeMCU D0 -> D16
              NodeMCU D1 -> D5
              .
              .
              .
              PIN configuration: https://www.electronicwings.com/public/images/user_images/images/NodeMCU/NodeMCU%20Basics%20using%20Arduino%20IDE/NodeMCU%20GPIO/NodeMCU%20GPIOs.png
    b. Method: "PUT"
    c. Content Type: "Application/JSON"
    d. Body: ["1"] - for ON, Body: ["0"] - for Off
    
 After this say "OK Google" in your Android phone (make sure same Google Email Id login with your Android Phone)
 and say Command whatever you set on "IFTTT Google Assistant" e.g. Trun on Light
 then google assistant automatically sent the request to IFTTT to triger the Web Hook and Light will the turned ON
