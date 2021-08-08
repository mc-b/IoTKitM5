LoraWAN
-------
***


### AT Commands

**Hardware/Firmware Info**

* `AT+CGMI?` - Read Manufacturer Identification
* `AT+CGMM?` - Read Model Identification 
* `AT+CGMR?` - Read Version Identification

**Link Informationen**

* `AT+CJOINMODE=?` - Read Join Mode (0：OTAA, 1：ABP)      
* `AT+CDEVEUI=?` - Read DevEUI
* `AT+CAPPEUI?` -  Read AppEUI 
* `AT+CAPPKEY?` - Read AppKey
* `AT+CFREQBANDMASK?` - Read Frequency Band Mask (0001 = 0-7 channel, 0002 = ：8-15 channel)
* `AT+CCLASS?` - Read Class (0 = A, 1 = B, 2 = C)
* `AT+CNWKSKEY?` - Read NwkSKey

**Debug**

* `AT+ILOGLVL=5` - Set/Read Log Level


Set/Read Join

    AT+CJOIN?
    
    AT+CJOIN=1,1,10,8
    
Set JOIN parameter: enable auto-JOIN, the period of JOIN is 10s, and the maximum retry times of JOIN is 8 times

ParaTag1 represent do the JOIN operation，ParaTag1’s value range：
0– Stop JOIN
1– Start JOIN, restart one JOIN procedure, for module which have enable the
warm boot, do the oeration will clear the parameters of JOIN procedure.
ParaTag2 represent if enable the auto-JOIN function, its factory value is 1,
ParaTag2’s value range:
0 – Disable auto-JOIN
1 – Enable auto-JOIN. When module enter into passthrough mode, enable autoJOIN.
ParaTag3 represent the period of JOIN, ParaTag3’s value range is 7~255, its
unit is seconds.
Factory default value：8
ParaTag4 represent the maximum retry times of JOIN, ParaTag4’s value range is
1~256    
    

Send/Receive Data

    AT+DTRX?
    
     
        

### Links

* [LoraWAN Modem Datenblatt](https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/docs/datasheet/unit/lorawan/ASR650X%20AT%20Command%20Introduction-20190605.pdf)
* [The Things Network Console](https://eu1.cloud.thethings.network/console/applications)
