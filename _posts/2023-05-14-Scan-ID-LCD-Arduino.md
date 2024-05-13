---
title: Scan ID LCD 16x2 Arduino - Code
author: mrhmt
date: 2023-4-23 11:45:00 +/-0084
categories: [catatan, coding]
tags: [lcd, arduino]
toc: true # table of content
comments: true 
math: true
mermaid: true # diagram generation tool
image:
    src: https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Arduino_Logo.svg/2560px-Arduino_Logo.svg.png
    width: 1000 
    height: 400
    alt: halo
pin: false
excerpt_separator: <!--more-->
published: true
---

# 1. Pendahuluan

berikut catatan untuk melakukan proses scan ID pada LCD 16x2. silahkan gunakan code dibawah

<!--more-->
# 2. Persiapan


List Code

````c

#include <Wire.h>
 
void setup() {
  Wire.begin();
  Serial.begin(115200);
  Serial.println("\nI2C Scanner");
}
 
void loop() {
  byte error, address;
  int nDevices;
  Serial.println("Scanning...");
  nDevices = 0;
  for(address = 1; address < 127; address++ ) {
    Wire.beginTransmission(address);
    error = Wire.endTransmission();
    if (error == 0) {
      Serial.print("I2C device found at address 0x");
      if (address<16) {
        Serial.print("0");
      }
      Serial.println(address,HEX);
      nDevices++;
    }
    else if (error==4) {
      Serial.print("Unknow error at address 0x");
      if (address<16) {
        Serial.print("0");
      }
      Serial.println(address,HEX);
    }    
  }
  if (nDevices == 0) {
    Serial.println("No I2C devices found\n");
  }
  else {
    Serial.println("done\n");
  }
  delay(5000);          
}


````

# 3. Hasil

Silahkan Dicoba

