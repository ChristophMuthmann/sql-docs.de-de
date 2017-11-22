---
title: Aktualisieren des DQS-Datenbankschemas nach der Installation eines SQL Server-Updates | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9d269cd8caad4c07fd8e1676dac36f9436db037a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>Aktualisieren des DQS-Datenbankschemas nach der Installation eines SQL Server-Updates
  Nachdem Sie ein SQL Server-Update (Patch, Hotfix oder kumulatives Update) auf einer zuvor konfigurierten DQS-Instanz installiert haben, muss das DQS-Datenbankschema u. U. aktualisiert werden, indem Sie die Datei DQSInstaller.exe mit dem Befehlszeilenparameter **upgrade** ausführen. Andernfalls kann beim Versuch, über den Data Quality-Client eine Verbindung mit dem Data Quality-Server herzustellen, der folgende Fehler ausgegeben werden:  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 Für das DQS-Datenbankschema ausgeführte Upgrades haben keine Auswirkungen auf vorhandene Daten in den DQS-Datenbanken (Wissensdatenbanken, Data Quality-Projekte und exportierte Ergebnisse in der DQS_STAGING_DATA-Datenbank). Sie müssen die DQS-Datenbanken jedoch sichern, bevor Sie das DQS-Datenbankschema aktualisieren, um versehentliche Datenverluste während des Schemaupgrades zu verhindern. Informationen zum Sichern von DQS-Datenbanken finden Sie unter [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
> [!NOTE]  
>  Die meisten SQL Server-Updates erfordern ein Upgrade auf das DQS-Datenbankschema. Informationen zu den SQL Server-Updates, die ein Upgrade auf das DQS-Datenbankschema erfordern, finden Sie im Diagramm in Schritt 1.A unter [Aktualisieren von DQS: Installieren von kumulativen Updates oder Hotfixpatches für Data Quality Services](http://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen als Mitglied der Administratorgruppe auf dem [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] -Computer angemeldet sein.  
  
-   Ihr Windows-Benutzerkonto muss Mitglied der festen Serverrolle sysadmin auf der SQL Server-Instanz sein, auf der der [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] installiert ist.  
  
### <a name="to-upgrade-dqs-databases-schema"></a>So aktualisieren Sie das DQS-Datenbankschema  
  
1.  (Empfohlen) Sichern Sie die DQS-Datenbanken, bevor Sie das Schemaupgrade fortsetzen. Informationen zum Sichern von DQS-Datenbanken finden Sie unter [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Öffnen Sie die Eingabeaufforderung.  
  
3.  Wechseln Sie an der Eingabeaufforderung zu dem Verzeichnis, in dem DQSInstaller.exe enthalten ist. Wenn Sie z. B. die Standardinstanz von SQL Server installiert haben, steht die Datei DQSInstaller.exe in der Regel unter C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn zur Verfügung:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  Sie werden vom Installationsprogramm aufgefordert, die DQS-Datenbanken zu sichern, bevor Sie den Vorgang fortsetzen. Wenn Sie die DQS-Datenbanken bereits gesichert haben, geben Sie **Y** oder **Yes** ein und drücken die EINGABETASTE, um das Upgrade fortzusetzen.  
  
6.  Nach dem erfolgreichen Upgrade des DQS-Datenbankschemas wird eine Abschlussmeldung angezeigt.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Melden Sie sich in einer Data Quality-Clientanwendung beim aktualisierten Data Quality-Server an.  
  
 Weitere Informationen zum Aktualisieren des DQS-Datenbankschemas nach der Installation von SQL Server-Updates sowie Schritte zur Problembehandlung finden Sie unter [Aktualisieren von DQS: Installieren von kumulativen Updates oder Hotfixpatches für Data Quality Services](http://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Aktualisieren der SQLCLR-Assemblys nach dem Aktualisieren von .NET Framework](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
