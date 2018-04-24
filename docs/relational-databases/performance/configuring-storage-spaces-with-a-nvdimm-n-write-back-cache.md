---
title: Konfigurieren von Speicherplätzen mit NVDIMM-N-Zurückschreibcache | Microsoft Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d24f8c39d4ab76c7887fb100a6235a1a8d775279
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-storage-spaces-with-a-nvdimm-n-write-back-cache"></a>Konfigurieren von Speicherplätzen mit NVDIMM-N-Zurückschreibcache
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows Server 2016 unterstützt NVDIMM-N-Geräte, die extrem schnelle Eingabe-/Ausgabevorgänge (E/A-Vorgänge) ermöglichen. Eine hervorragende Möglichkeit der Verwendung solcher Geräte ist ein Zurückschreibcache, um niedrige Schreiblatenzen zu erreichen. In diesem Thema wird erläutert, wie ein gespiegelter Speicherplatz mit einem gespiegelten NVDIMM-N-Zurücksückschreibcache als virtuelles Laufwerk eingerichtet werden kann, um das SQL Server-Transaktionsprotokoll zu speichern. Wenn Sie den Speicherplatz auch dazu verwenden möchten, Datentabellen oder andere Daten zu speichern, können Sie weitere Datenträger in den Speicherpool aufnehmen oder, wenn Isolation wichtig ist, mehrere Pools erstellen.  
  
 Ein Channel 9-Video zur Nutzung dieser Technik finden Sie unter [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016](https://channel9.msdn.com/Events/Build/2016/P466).  
  
## <a name="identifying-the-right-disks"></a>Ermitteln der geeigneten Datenträger  
 Ein Einrichten von Speicherplätzen in Windows Server 2016, insbesondere mit erweiterten Funktionen wie Zurückschreibcaches, lässt sich am einfachsten über PowerShell erledigen. Der erste Schritt besteht darin, zu ermitteln, welche Datenträger zu dem Speicherplätzepool gehören sollen, aus dem der virtuelle Datenträger erstellt wird. NVDIMM-Ns haben den Medientyp und Bustyp SCM (Storage Class Memory), der über das PowerShell-Cmdlet „Get-PhysicalDisk“ abgefragt werden kann.  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  Mit NVDIMM-N-Geräten ist es nicht mehr erforderlich, dass Sie speziell die Geräte auswählen, die Ziele für einen Zückschreibcache sein können.  
  
 Um einen gespiegelten virtuellen Datenträger mit gespiegeltem Zurückschreibcache zu erstellen, sind mindestens 2 NVDIMM-Ns und 2 weitere Datenträger erforderlich. Die Vorgehensweise lässt sich vereinfachen, indem die gewünschten physischen Datenträger einer Variablen zugeordnet werden.  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 Der Screenshot zeigt die Variable „$pd“ sowie die 2 SSDs und 2 NVDIMM-Ns, die ihr zugewiesen sind und mit dem folgenden PowerShell-Cmdlet zurückgegeben wurden.  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![Auswählen von FriendlyName](../../relational-databases/performance/media/select-friendlyname.png "Select FriendlyName")  
  
## <a name="creating-the-storage-pool"></a>Erstellen des Speicherpools  
 Über die Variable „$pd“, die die physischen Datenträger enthält, ist es einfach, den Speicherpool mit dem PowerShell-Cmdlet „New-StoragePool“ zu erstellen.  
  
```  
New-StoragePool –StorageSubSystemFriendlyName “Windows Storage*” –FriendlyName NVDIMM_Pool –PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## <a name="creating-the-virtual-disk-and-volume"></a>Erstellen des virtuellen Datenträgers und Volumes  
 Nachdem ein Pool erstellt wurde, besteht der nächste Schritt darin, einen virtuellen Datenträger anzulegen und diesen zu formatieren. In diesem Fall wird nur 1 virtueller Datenträger erstellt, und das PowerShell-Cmdlet „New-Volume“ kann verwendet werden, um diesen Prozess zu optimieren:  
  
```  
New-Volume –StoragePool (Get-StoragePool –FriendlyName NVDIMM_Pool) –FriendlyName Log_Space –Size 300GB –FileSystem NTFS –AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 Der virtuelle Datenträger wurde erstellt, initialisiert und mit NTFS formatiert. Der folgende Screenshot zeigt, dass der Datenträger eine Größe von 300 GB und eine Schreibcachegröße von 1 GB hat, die auf den NVDIMM-Ns gehostet wird.  
  
 ![Get-VirtualDisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-VirtualDisk")  
  
 Sie können dieses neue Volume jetzt auf dem Server sehen. Dieses Laufwerk können Sie nun für Ihr SQL Server-Transaktionsprotokoll verwenden.  
  
 ![Log_Space-Laufwerk](../../relational-databases/performance/media/log-space-drive.png "Log_Space Drive")  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Speicherplätze unter Windows 10](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)   
 [Speicherplätze unter Windows 2012 R2](https://technet.microsoft.com/en-us/library/hh831739.aspx)   
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Anzeigen oder Ändern der Standardspeicherorte für Daten- und Protokolldateien &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)  
  
  
