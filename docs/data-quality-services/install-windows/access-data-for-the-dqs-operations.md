---
title: Zugriff auf Daten für DQS-Vorgänge | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 88dfb9ea-6321-4eaf-b9e4-45d36ef048f6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dac1d338d8a4a835099de086be4c162fdadafb0e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="access-data-for-the-dqs-operations"></a>Zugriff auf Daten für DQS-Vorgänge

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Sie haben die folgenden Möglichkeiten, um die Quelldaten für [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS)-Vorgänge zu verwenden und die verarbeiteten Daten zu exportieren:  
  
-   Kopieren Sie die Quelldaten in eine Tabelle/Sicht in der DQS_STAGING_DATA-Datenbank, und verwenden Sie sie dann für DQS-Vorgänge. Sie können die verarbeiteten Daten auch in eine neue Tabelle in der DQS_STAGING_DATA-Datenbank exportieren. Hierzu muss dem Windows-Benutzerkonto Lese-/Schreibzugriff auf die Datenbank DQS_STAGING_DATA gewährt werden.  
  
-   Verwenden Sie die eigene Datenbank als Datenquelle für die DQS-Vorgänge und als Ziel zum Exportieren der verarbeiteten Daten. Stellen Sie deswegen sicher, dass sich die Datenbank in der gleichen SQL Server-Instanz wie die Data Quality Server-Datenbanken befindet. Andernfalls steht die Datenbank nicht für DQS-Vorgänge im Data Quality-Client zur Verfügung. Außerdem muss dem Windows-Benutzerkonto Zugriff auf die Datenbank DQS_STAGING_DATA zum Exportieren der Abgleichsergebnisse gewährt werden, da der Export der Abgleichsergebnisse ein zweiphasiger Prozess ist: zuerst werden die Abgleichsergebnisse in die temporären Tabellen in der Datenbank DQS_STAGING_DATA exportiert und dann in die Tabelle in der Zieldatenbank verschoben.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen die Installation des [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] durch Ausführen der Datei DQSInstaller.exe abgeschlossen haben. Weitere Informationen finden Sie unter [Ausführen von DQSInstaller.exe zum Abschließen der Installation von Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
-   Das Windows-Benutzerkonto muss ein Element der entsprechenden festen Serverrolle (z. B. securityadmin, serveradmin oder sysadmin) in der Datenbankmodulinstanz sein, um Zugriff auf die SQL-Anmeldung in Datenbanken zu gewähren/zu ändern.  
  
### <a name="to-grant-readwrite-access-to-a-user-on-the-dqsstagingdata-database"></a>So gewähren Sie einem Benutzer Lese-/Schreibzugriff auf die DQS_STAGING_DATA-Datenbank  
  
1.  Starten Sie Microsoft SQL Server Management Studio.  
  
2.  Erweitern Sie in Microsoft SQL Server Management Studio die SQL Server-Instanz, und erweitern Sie anschließend **Sicherheit**und **Anmeldungen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf eine SQL-Anmeldung, und klicken Sie auf **Eigenschaften**.  
  
4.  Klicken Sie im Dialogfeld **Anmeldungseigenschaften** auf die Seite **Benutzerzuordnung** im linken Bereich.  
  
5.  Aktivieren Sie im rechten Bereich in der Spalte **Zuordnen** das Kontrollkästchen für die **DQS_STAGING_DATA** -Datenbank, und wählen Sie anschließend im Bereich **Mitgliedschaft in Datenbankrolle für: DQS_STAGING_DATA** die folgenden Rollen aus:  
  
    -   **db_datareader**: Lesen von Daten aus Tabellen/Sichten.  
  
    -   **db_datawriter**: Hinzufügen, Löschen oder Ändern von Daten in Tabellen.  
  
    -   **db_ddladmin**: Erstellen, Ändern oder Löschen von Tabellen/Sichten.  
  
6.  Klicken Sie im Dialogfeld **Anmeldungseigenschaften** auf **OK** , um die Änderungen zu übernehmen.  
  
## <a name="next-steps"></a>Next Steps  
 Versuchen Sie, DQS-Vorgänge auszuführen, die auf die Datenbank als Datenquelle für den DQS-Vorgang zugreifen, und exportieren Sie dann die verarbeiteten Daten in die Datenbank.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Installieren von Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)  
  
  
