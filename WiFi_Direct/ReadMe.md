# Establishing a Wi-Fi Direct Connection Between Calypso and an Android Smartphone

This guide outlines the steps required to establish a Wi-Fi Direct (Peer-to-Peer) connection between the Calypso Wi-Fi module and an Android smartphone. This setup has been tested with a Samsung Galaxy S23 Ultra.

## Prerequisites

1. **Calypso Wi-Fi Module** in P2P mode, with firmware version 2.2.1 or higher.
2. **Android Smartphone** configured for Wi-Fi Direct (tested with Samsung Galaxy S23 Ultra).
3. **AT Command Tool** for the Calypso Wi-Fi module.

## Step 1: Configuring the Android Phone for Wi-Fi Direct (P2P Mode)

1. Open **Wi-Fi Direct** settings on the Android phone.
2. Enable Wi-Fi Direct mode and keep the tab open to scan for available P2P devices.
3. Follow this guide for details on enabling Wi-Fi Direct: [How to Use Wi-Fi Direct](https://www.lifewire.com/how-to-use-wifi-direct-4685655#:~:text=Launch%20the%20Settings%20app%20and,Direct%20enabled%20and%20are%20visible).

## Step 2: Configuring Calypso Module for P2P Mode

Run the following AT commands in sequence to configure the Calypso Wi-Fi module to work in Wi-Fi Direct (P2P) mode:

```plaintext
AT+wlansetmode=P2P
AT+wlanpolicyset=P2P,client,active
AT+stop=0
AT+start
AT+wlanscan=1,10
```

Note: The first scan command (AT+wlanscan=1,10) initiates a scan and may return an error code SL_ERROR_WLAN_GET_NETWORK_LIST_EAGAIN (-2073) before listing the available P2P devices. This is normal.

Once a P2P device is found, you should see a message like the following:
```
+eventwlan:p2p_devfound,Shashank's S23 Ultra,0xbe:0x32:0xb2:0x7:0x65:0x89
```

## Step 3: Connecting Calypso to the Android Device
To connect to the detected P2P device, use the AT+wlanconnect command with the desired PIN 12345670:

AT+wlanconnect=Shashank's S23 Ultra,,P2P_PIN_DISPLAY,12345670,,,

Replace Shashank's S23 Ultra with the actual name of the Android device detected.

Set the PIN to 12345670 or any preferred value.

Upon running this command, a pop-up window should appear on the Android phone requesting the PIN.

![WiFi_Direct_Setup](../imgs/WiFiDirect_connect.jfif)

*Fig.1 WiFi_Direct*

## 4: Finalize the Connection
Enter the correct PIN on the Android device when prompted.
Once the correct PIN is entered, the Calypso module will connect to the Android phone via Wi-Fi Direct.

![WiFi_Direct_Image](../imgs/WiFi_Direct2.jfif)
*Fig.2 WiFi_Direct*

