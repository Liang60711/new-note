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


## SCSI iSCSI FC 協議
* SCSI: 小型計算機系統接口 (Small Computer System Interface)。

* iSCSI: 網際網路小型計算機系統接口 (Internet Small Computer System Interface)，是一種在TCP/IP上進行數據塊傳輸的標準，實現在IP網絡上運行SCSI協議。


* FC: 光纖通道 (Fibre Channel)，
是一種高速網路互聯技術（最高速度128Gbps），主要用於連接儲存裝置，為企業級儲存 SAN 中的一種常見連接類型。


## target lun
NAS 上會有許多 SCSI，但數量是有限制的，通常會用 target ID 來描述這些設備，設備只要一加入系統，就會有 ID。當 target ID 數量不夠時，採用 lun ID，擴充了每個 target ID，`每個 target 下都可以有多個lun `。

## cluster
* 指多台電腦透過某些技術或架構運作成單一系統，共同提供服務，多台電腦互相為備援，以維持伺服器與應用程式運作時間，確保服務的可用性。
* 在叢集中我們常以節點 (Node) 來稱呼叢集主機。

## ESX host 和 vMotion
* ESX host: VMware 的 cluster。
* vMotion: VMware 技術，將工作負載從預計發生停機的 ESX host 移轉到另一部 ESX host 上。

	* 舉例: vm 所在的 ESX host 出現系統資源 (如 CPU, RAM) 短缺的問題, VMware 在偵測到這種情況之下，就有可能把這個 vm 移轉 (v-motion) 到另外一個可用的 ESX host 通常 v-motion 也可以被視為高可用性 (HA: High Availability，指系統無中斷地執行其功能的能力) 及災難復原 (DR: Disaster Recovery) 的方法之一。

## VM snapshot
虛擬主機快照，VM 虛擬主機層級的備份。

## Scalability 可伸縮性、可擴展性
* 縱向的可伸縮性: 在同一個邏輯單元內增加資源來提高處理能力。這樣的例子包括在現有伺服器上增加 CPU，或者在現有的 RAID/SAN 儲存中增加硬碟來提高儲存量。
* 橫向的可伸縮性: 增加更多邏輯單元的資源，並令它們像是一個單元一樣工作。大多數叢集方案、分散式檔案系統、負載平衡提高橫向的可伸縮性。
* RDBMS (一台機器跑一個服務或多個服務) 透過縱向的擴展；noSQL (多個機器跑一個服務) 則透過橫向擴展。





<br/>

<br/>

