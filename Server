#include <ESP8266WiFi.h>
extern "C" {
  #include<user_interface.h>
}
void setup()
{
  pinMode(LED_BUILTIN,OUTPUT);
  Serial.begin(115200);
  Serial.println();
  Serial.print("Setting soft-AP ... ");
  boolean result = WiFi.softAP("ESPsoftAP_01", "12345678",11,false,2);
  Serial.print("IP:");Serial.println(WiFi.softAPIP());
  Serial.print("MAC:");Serial.println(WiFi.softAPmacAddress());
  if(result == true)
  {
    Serial.println("Ready");
  }
  else
  {
    Serial.println("Failed!");
  }
}
void loop()
{  delay(5000);
  client_status();
  Serial.printf("Stations connected = %d\n", WiFi.softAPgetStationNum());
  if(WiFi.softAPgetStationNum()>=1)
  {
    digitalWrite(LED_BUILTIN,LOW);
  }
  else
  {
    digitalWrite(LED_BUILTIN,HIGH);
  }
}
void client_status() {
 
  unsigned char number_client;
  struct station_info *stat_info;
  
  struct ip4_addr *IPaddress;
  IPAddress address;
  int i=1;
  
  number_client= wifi_softap_get_station_num();
  stat_info = wifi_softap_get_station_info();
  
  Serial.print(" Total Connected Clients are = ");
  Serial.println(number_client,DEC);
  Serial.print(",");
  
    while (stat_info != NULL) {
    
      IPaddress = &stat_info->ip;
      address = IPaddress->addr;
      
      Serial.print("client= ");
      
      Serial.print(i);
      Serial.print(" IP adress is = ");
      Serial.print((address));
      Serial.print(" with MAC adress is = ");
      
      Serial.print(stat_info->bssid[0],HEX);Serial.print(" ");
      Serial.print(stat_info->bssid[1],HEX);Serial.print(" ");
      Serial.print(stat_info->bssid[2],HEX);Serial.print(" ");
      Serial.print(stat_info->bssid[3],HEX);Serial.print(" ");
      Serial.print(stat_info->bssid[4],HEX);Serial.print(" ");
      Serial.print(stat_info->bssid[5],HEX);Serial.print(" ");
      
      stat_info = STAILQ_NEXT(stat_info, next);
      i++;
      Serial.println();
    }
}
