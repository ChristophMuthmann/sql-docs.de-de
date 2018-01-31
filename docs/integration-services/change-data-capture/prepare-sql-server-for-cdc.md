---
title: "Vorbereiten von SQL Server für CDC | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- prepSqlSrv
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 598c626e94eecce208c880fd48c4aa2b6c16d793
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="prepare-sql-server-for-cdc"></a>Vorbereiten von SQL Server für CDC
  Der Oracle CDC Service erfordert, dass alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanzen die MSXDBCDC-Datenbank enthalten. Sie erstellen diese Datenbank mithilfe der Aktion Prepare SQL Server in der CDC Service Configuration Console. Dabei wird ein spezielles Skript erstellt, das ausgeführt wird, um die erforderlichen Tabellen, gespeicherten Prozeduren und anderen erforderlichen Artefakte für diese Datenbank zu erstellen. Dieser Task wird für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz nur einmal ausgeführt.  
  
 Weitere Informationen zur MSXDBCDC-Datenbank finden Sie unter MSXDBCDC-Datenbank.  
  
 Klicken Sie in der CDC Service Configuration Console auf **Prepare SQL Server**. Wenn diese Option nicht verfügbar ist, sollten Sie sicherstellen, dass **Local CDC Services** im linken Bereich der Konsole aktiviert ist.  
  
## <a name="options"></a>Tastatur  
  
### <a name="server-name"></a>Servername  
 Geben Sie den Namen des Servers ein, auf dem sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet.  
  
### <a name="authentication"></a>Authentifizierung  
 Wählen Sie eine der folgenden Optionen aus:  
  
-   **Windows-Authentifizierung**  
  
-   **SQL Server-Authentifizierung**: Wenn Sie diese Option aktivieren, müssen Sie **Benutzername** und **Kennwort** für den Benutzer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingeben, mit dem Sie eine Verbindung herstellen.  
  
 Um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für Oracle CDC vorzubereiten, muss die Anmeldung über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügen. Geben Sie die Anmeldeinformationen für eine Anmeldung ein, die über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügt, z. B. als Mitglied der Rolle `sysasmin` .  
  
### <a name="options"></a>Tastatur  
 Klicken Sie auf den Pfeil, um die verfügbaren Optionen anzuzeigen, die konfiguriert werden sollen. Sie können für diese Optionen auch die Standardwerte unverändert lassen. Verfügbare Optionen:  
  
-   **Verbindungstimeout**: Geben Sie den Zeitraum (in Sekunden) ein, wie lange der CDC Service für Oracle auf eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] warten soll, bevor ein Timeout eintritt. Der Standardwert lautet **15**.  
  
-   **Ausführungstimeout**: Geben Sie den Zeitraum (in Sekunden) ein, wie lange der Oracle CDC-Windows-Dienst auf die Ausführung eines Befehls warten soll, bevor ein Timeout eintritt. Der Standardwert ist **30**.  
  
-   **Verbindung verschlüsseln**: Wählen Sie **Verbindung verschlüsseln** für die Kommunikation zwischen dem Oracle CDC Service und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz aus, bei der eine verschlüsselte Verbindung verwendet werden soll.  
  
-   **Erweitert**: Geben Sie zusätzliche Verbindungseigenschaften ein, falls erforderlich.  
  
### <a name="view-script"></a>Skript anzeigen  
 Klicken Sie auf **Skript anzeigen** , um eine schreibgeschützte Version des Setupskripts anzuzeigen. Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministrator kann dieses Skript bei Bedarf in die SQL Server Management Console kopieren, um sie zu bearbeiten. Weitere Informationen über Prepare SQL Server Script finden Sie unter [Vorbereiten von SQL Server für Oracle CDC – Skript anzeigen](../../integration-services/change-data-capture/prepare-sql-server-for-oracle-cdc-view-script.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden von CDC Services](../../integration-services/change-data-capture/how-to-work-with-cdc-services.md)   
 [Vorbereiten von SQL Server für CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  
