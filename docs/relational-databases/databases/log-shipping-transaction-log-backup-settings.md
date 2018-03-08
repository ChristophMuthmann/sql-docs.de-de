---
title: "Sicherungseinstellungen für den Transaktionsprotokollversand | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: log-shipping
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.logshipping.settings.tlogback.f1
ms.assetid: 9a6e6c16-7f71-412b-bba6-7bffac001277
caps.latest.revision: "27"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01a15e3ebf54cae459aad00052e009774d125c56
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="log-shipping-transaction-log-backup-settings"></a>Sicherungseinstellungen für den Transaktionsprotokollversand
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe dieses Dialogfelds können Sie die Sicherungseinstellungen des Transaktionsprotokolls für eine Protokollversandkonfiguration konfigurieren und ändern.  
  
 Eine Erläuterung zu den Konzepten des Protokollversands finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Tastatur  
 **Netzwerkpfad zu diesem Sicherungsordner**  
 Geben Sie in dieses Feld die Netzwerkfreigabe für den Sicherungsordner ein. Der lokale Ordner, in dem die Transaktionsprotokollsicherungen gespeichert sind, muss freigegeben werden, damit diese Dateien mithilfe der Protokollversand-Kopieraufträge kopiert werden können. Außerdem müssen Sie für das Proxykonto dieser Netzwerkfreigabe, unter dem die Kopieraufträge auf den sekundären Serverinstanzen ausgeführt werden, Lese- und Schreibberechtigungen erteilen. Standardmäßig ist dies das SQLServerAgent-Dienstkonto der sekundären Serverinstanz. Ein Administrator kann jedoch für den Auftrag ein anderes Proxykonto auswählen.  
  
 **Wenn sich der Sicherungsordner auf dem primären Server befindet, geben Sie den lokalen Pfad zum Ordner ein**  
 Geben Sie den Buchstaben des lokalen Datenträgers und den Pfad zum Sicherungsordner ein, wenn sich der Sicherungsordner auf dem primären Server befindet. Wenn sich der Sicherungsordner nicht auf dem primären Server befindet, können Sie dieses Feld leer lassen.  
  
 Wenn Sie hier einen lokalen Pfad angeben, wird dieser vom BACKUP-Befehl zum Erstellen der Transaktionsprotokollsicherungen verwendet. Ist kein lokaler Pfad angegeben, verwendet der BACKUP-Befehl den Netzwerkpfad, der unter **Netzwerkpfad zu diesem Sicherungsordner** angegeben ist.  
  
> [!NOTE]  
>  Wenn das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto unter dem lokalen Systemkonto auf dem primären Server ausgeführt wird, müssen Sie den Sicherungsordner auf dem primären Server erstellen und den lokalen Pfad zu diesem Ordner hier angeben. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto der primären Serverinstanz muss über Lese- und Schreibberechtigungen für diesen Ordner verfügen.  
  
 **Dateien löschen, die älter sind als**  
 Geben Sie die Zeitdauer an, für die Transaktionsprotokolle im Sicherungsverzeichnis erhalten werden sollen, bevor sie gelöscht werden.  
  
 **Warnen, wenn keine Sicherung erfolgt in**  
 Geben Sie die Zeitspanne an, die beim Protokollversand gewartet werden soll, bevor eine Warnung ausgelöst wird, weil keine Sicherung von Transaktionsprotokollen erfolgt ist.  
  
 **Auftragsname**  
 Zeigt den Namen des SQL Server-Agentauftrags an, der verwendet wird, um die Transaktionsprotokollsicherungen für den Protokollversand zu erstellen. Wenn Sie den Auftrag erstmalig erstellen, können Sie den Namen durch Eingabe in das entsprechende Feld ändern.  
  
 **Zeitplan**  
 Zeigt den aktuellen Zeitplan für die Sicherung der Transaktionsprotokolle der primären Datenbank an. Vor dem Erstellen des Sicherungsauftrags können Sie diesen Zeitplan ändern, indem Sie auf **Zeitplan...**klicken. Nachdem der Sicherungsauftrag erstellt wurde, können Sie den Zeitplan ändern, indem Sie auf **Auftrag bearbeiten...**klicken.  
  
### <a name="backup-job"></a>Sicherungsauftrag  
 **Zeitplan...**  
 Ändern Sie den Zeitplan, der beim Erstellen des SQL Server-Agentauftrags erstellt wird.  
  
 **Auftrag bearbeiten...**  
 Ändern Sie die Parameter des SQL Server-Agentauftrags für den Auftrag, der Transaktionssicherungsprotokolle in der primären Datenbank ausführt.  
  
 **Diesen Auftrag deaktivieren**  
 Deaktivieren Sie den SQL Server-Agentauftrag zum Erstellen von Transaktionsprotokollsicherungen.  
  
### <a name="compression"></a>Komprimierung  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder höher) unterstützt die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Sicherungskomprimierung festlegen**  
 Wählen Sie in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder höher) einen der folgenden Werte für die Sicherungskomprimierung der Protokollsicherungen dieser Protokollversandkonfiguration aus:  
  
|||  
|-|-|  
|**Standardservereinstellungen verwenden**|Klicken Sie hier, um die Standardeinstellung auf Serverebene zu verwenden.<br /><br /> Diese Standardeinstellung wird durch die Serverkonfigurationsoption **Komprimierungsstandard für Sicherung** festgelegt. Informationen zum Anzeigen der aktuellen Einstellung dieser Option finden Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption „Standardeinstellung für die Sicherungskomprimierung“](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Sicherung komprimieren**|Klicken Sie hier, um die Sicherung unabhängig von der Standardeinstellung auf Serverebene zu komprimieren.<br /><br /> **\*\* Wichtig \*\*** Standardmäßig steigt die CPU-Nutzung durch die Komprimierung erheblich, und die durch die Komprimierung zusätzlich genutzten CPU-Ressourcen können sich negativ auf gleichzeitige Vorgänge auswirken. Daher ist es möglicherweise sinnvoll, in einer Sitzung, bei der die CPU-Nutzung durch den [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen. Weitere Informationen finden Sie unter [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen.|  
|**Sicherung nicht komprimieren**|Klicken Sie hier, um unabhängig von der Standardeinstellung auf Serverebene eine nicht komprimierte Sicherung zu erstellen.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren eines Benutzers zum Erstellen und Verwalten von SQL Server-Agent-Aufträgen](http://msdn.microsoft.com/library/67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef)   
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
