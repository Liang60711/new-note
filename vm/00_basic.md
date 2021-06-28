# 名詞解釋

## Hypervisor
虛擬機器監視器 (virtual machine monitor，VMM)，用來建立與執行虛擬機器的軟體、韌體或硬體。近年來虛擬化技術重新被重視的原因：**雲端運算**，伺服器的平均使用率低於 30%，但真正遇到高峰期的業務量時、現有伺服器仍無法滿足需求。

* Type 1: Bare metal Hypervisor (裸機):
    * 直接安裝於空機或新機上，直接掌控硬體資源。
    * 硬體無須先有作業系統，VMM 直接作為主作業系統、運行效率高。

* Type 2: Hosted Hypervisor:
    * 需先有 Windows 或 Linux 等作業系統在機器上才能安裝 VMM。
    * 運行效率一般較 Type 1 還低。



## SAN
儲存區域網路 (Storage Area Network) 是由儲存裝置所組成的網路，可供多部伺服器與電腦存取，並提供共用的儲存空間集區。網路上的每部電腦都可以存取儲存區域網路中的儲存空間，如同直接安裝在電腦上的本機磁碟機。

||LAN|SAN|
|--|--|--|
|下層協議|Ethernet|Fibre Channel|
|上層協議|TCP/IP|SCSI|
|交換機|L2/L3 switch|FC switch/director|


## Fibre Channel (FC)
是一種高速網路互聯技術（最高速度128Gbps），主要用於連接儲存裝置，為企業級儲存 SAN 中的一種常見連接類型。