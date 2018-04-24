---
title: Datenbankspiegelungsverlauf | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.dbmmonitor.databasemirroringhistory.f1
ms.assetid: 1d6e4b10-4a23-47d7-9918-c417992f09d3
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8d4d344a8901fcfcf6caa537d4b3fbc6b6891ee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-mirroring-history"></a>Datenbankspiegelungsverlauf
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Verwenden Sie dieses Dialogfeld, um den Verlauf des Spiegelungsstatus für eine gespiegelte Datenbank auf einer angegebenen Serverinstanz anzuzeigen.  
  
 **So verwenden Sie SQL Server Management Studio zum Überwachen der Datenbankspiegelung**  
  
-   [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Tastatur  
 **Serverinstanz**  
 Der Name der Serverinstanz, von der der Verlauf gemeldet wird.  
  
 **Datenbank**  
 Der Name der Datenbank, deren Verlauf angezeigt wird.  
  
 **Liste filtern nach**  
 Listet Filterwerte auf. Durch Auswählen eines neuen Werts wird das Raster automatisch aktualisiert.  
  
 Die folgenden Filterwerte sind möglich:  
  
-   Letzten zwei Stunden  
  
-   Letzten vier Stunden  
  
-   Letzten acht Stunden  
  
-   Letzter Tag  
  
-   Letzten zwei Tage  
  
-   Letzten 100 Datensätze  
  
-   Letzten 500 Datensätze  
  
-   Letzten 1000 Datensätze  
  
-   Alle Datensätze  
  
 **Aktualisieren**  
 Klicken Sie auf diese Schaltfläche, um die Verlaufsliste zu aktualisieren.  
  
> [!NOTE]  
>  Die Verlaufsliste in diesem Dialogfeld wird nicht automatisch aktualisiert. Klicken Sie entweder auf **Aktualisieren** , oder wählen Sie eine andere Filteroption aus, um die Liste zu aktualisieren. Nur Mitglieder der festen Serverrolle **sysadmin** können den Spiegelungsverlauf aktualisieren.  
  
 **Verlauf**  
 Zeigt die Verlaufsliste an. Wenn Sie auf einen Spaltenheader klicken, wird das Raster nach der entsprechenden Spalte sortiert. Die Liste enthält folgende Spalten:  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**Aufgezeichnete Zeit**|Timestamp der Verlaufszeile.|  
|**Rolle**|Die aktuelle Spiegelungsrolle der Serverinstanz für diese Datenbank: Prinzipal oder Spiegel.|  
|**Spiegelungsstatus**|Status der Datenbank:<br /><br /> Getrennt<br /><br /> Ausstehendes Failover<br /><br /> Angehalten<br /><br /> Synchronisiert<br /><br /> Wird synchronisiert<br /><br /> Unknown|  
|**Zeugenverbindung**|Status der Zeugenverbindung in der Spiegelungssitzung der Datenbank: Verbunden oder Getrennt. Wenn kein Zeuge vorhanden ist, ist der Wert NULL.|  
|**Nicht gesendetes Protokoll**|Größe, in Kilobyte (KB), des nicht gesendeten Protokolls in der Sendewarteschlange auf der Prinzipalserverinstanz.|  
|**Sendezeit**|Die ungefähre Dauer der Zeit, die die Prinzipalserverinstanz benötigt, um das derzeit in der Sendewarteschlange befindliche Protokoll an die Spiegelserverinstanz zu senden (die *Senderate*). Da die Rate der eingehenden Transaktionen erheblich schwanken kann, handelt es sich bei der Protokollsendezeit um einen Schätzwert. Die Senderate kann jedoch nützlich sein, um die für ein manuelles Failover erforderliche Zeit grob zu schätzen.|  
|**Send Rate**|Rate, in KB pro Sekunde, mit der Transaktionen an die Spiegelserverinstanz gesendet werden.|  
|**Neue Transaktionsrate**|Rate, in KB pro Sekunde, mit der eingehende Transaktionen in das Protokoll des Prinzipals eingegeben werden. Vergleichen Sie diesen Wert mit dem Wert **Sendezeit** , um zu bestimmen, ob die Spiegelung im Rückstand ist, einen Vorsprung hat oder auf dem aktuellen Stand ist.|  
|**Älteste, nicht gesendete Transaktion**|Alter der ältesten, nicht gesendeten Transaktion in der Sendewarteschlange. Das Alter dieser Transaktion gibt an, wie viele Minuten an Transaktionen noch nicht an die Spiegelserverinstanz gesendet wurden. Dieser Wert hilft, das Datenverlustrisiko in Bezug auf die Zeit zu messen.|  
|**Nicht wiederhergestelltes Protokoll**|Die Menge der Protokolldaten in KB, die sich in der Wiederholungswarteschlange befinden.|  
|**Wiederherstellungszeit**|Die geschätzte Anzahl von Minuten, die erforderlich ist, um das Protokoll, das sich derzeit in der Wiederholungswarteschlange befindet, auf die Spiegeldatenbank anzuwenden.|  
|**Wiederherstellungsrate**|Rate, in KB pro Sekunde, mit der Transaktionen in der Spiegeldatenbank wiederhergestellt werden.|  
|**Spiegelungscommitaufwand**|Durchschnittliche Verzögerung pro Transaktion in Millisekunden (nur im synchronen Modi). Hierbei handelt es sich um die Verzögerung, die entsteht, während die Prinzipalserverinstanz darauf wartet, dass die Spiegelserverinstanz den Transaktionsprotokolldatensatz in die Wiederholungswarteschlange schreibt.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Starten des Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
