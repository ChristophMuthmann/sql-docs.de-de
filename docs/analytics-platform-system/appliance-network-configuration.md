---
title: Appliance-Netzwerkkonfiguration (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e2b9abe-963d-479b-a4a7-1739fcb3e249
caps.latest.revision: "27"
ms.openlocfilehash: e24ed8e992591d08628ffeb14c30a47d7fa5b54a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-network-configuration"></a>Appliance-Netzwerkkonfiguration
Die SQL Server PDW-Anwendung wird erstellt und mit einem Update von IP-Adressen in allen Servern und Geräten aus der IHV Herstellerstandort konfiguriert. Bei der Übermittlung der Appliance muss die externen (Ethernet) IP-Adresse gerichtet neu konfiguriert werden, um die kundenspezifischen Daten Center Anforderungen entsprechen.  
  
> [!NOTE]  
> PDW-V1 erforderlich 8 IP-externe (*Kunden mit Internetzugriff*) Adressen für die externe Verbindung an jeden des Steuerelements rack-Knoten. PDW-2012 (V2) verbessert die Netzwerkkommunikation, verfügbar machen, jede Komponente der Anwendung extern über IP-Adressen an. Dieser Ansatz bietet einen robusteren Entwurf reduziert Kosten, und erhöht die Flexibilität und verbessert die datenverschiebung, Laden von Daten und Hadoop-Integration. Die Anzahl der erforderlichen IP-Adressen hängt davon ab, die Anzahl der Knoten in der Einheit und das Vorhandensein von Features wie HDInsight. Um dieser größeren Block von IP-Adressen zu unterstützen, sollte der Kunde eine getrenntes Subnetz für PDW einrichten. In diesem Subnetz werden genügend IP-Adressraum (bis zu 250 Adressen), um die Komponenten von bis zu 5 PDW Racks Rechnung zu tragen.  
  
Die **Netzwerkkonfiguration** Seite können Sie die externe Netzwerkeinstellungen für die Knoten auf Ihrer Anwendung Analytics Platform System anzuzeigen. Diese Seite ist schreibgeschützt.  
  
![DWConfig, Anwendungsnetzwerk](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Um die Netzwerkkonfiguration auf dem Gerät zu aktualisieren.  
Ändern Sie die IP-Adressen der Fabric-Domäne, Domäne Arbeitslast und HDInsight Domänen durch Bearbeiten der **AplianceInfo.xml** Datei und anschließend Setup ausführen. Dies ist ein Offlinevorgang. Sowohl die HDInsight (falls vorhanden) die PDW Regionen werden automatisch beendet werden, während die Änderung der IP-Adresse.  
  
> [!NOTE]  
> Domänennamen werden werden während des Setups bereitgestellt und bis zu 6 alphanumerische Zeichen, die mit einem Buchstaben beginnen. Einem häufiger Benennungssystem erstellt eine Fabric-Domäne, die beginnend mit F, einer PDW-arbeitsauslastung-Domäne P ab und einer HDInsight-Domäne, beginnend mit h. Dieses Format wird davon ausgegangen, dass in den Hilfethemen für die Datei ist jedoch nicht erforderlich. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>So ändern Sie die IP-Adressen das Analytics Platform System  
  
1.  Mithilfe der **Remotedesktop** -Anwendung Herstellen einer Verbindung mit **HST01** mithilfe des Domänenadministratorkontos Arbeitslast.  
  
2.  Öffnen Sie auf den Knoten HST01 der Appliance-Infodatei am **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Wenn die Datei nicht vorhanden ist, müssen möglicherweise eine neue Datei erstellt werden.  
  
3.  Aktualisieren Sie die Ethernet-IP-Werte ein, nach Bedarf, und speichern Sie die Datei.  
  
4.  Führen Sie in einem Eingabeaufforderungsfenster den folgenden Setupbefehl zum Aktualisieren der IP-Adressen für die PDW-Region, die mit P/F/H-Domänennamen und die Administratorkennwörter.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Hersteller-Verweise  
Weitere Informationen über Dell-Einheiten finden Sie unter:  
  
-   PowerConnect Switch-Anweisungen [Dell PowerConnect 6200 Reihe System CLI-Referenzhandbuch](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [integrierte Dell Remote Access Controller 7 (iDRAC7) Version 1.30.30-Benutzerhandbuch](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   Die Stromverteilereinheit **Dell gemessene Gestell-PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Siehe auch  
[Starten Sie den Konfigurations-Manager &#40; Analyseplattformsystem &#41;](launch-the-configuration-manager.md)  
  
