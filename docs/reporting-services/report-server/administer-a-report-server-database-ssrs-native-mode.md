---
title: Verwalten einer Berichtsserver-Datenbank (einheitlicher SSRS-Modus) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], databases
- renaming databases
- report server database
- databases [Reporting Services], administering
- reportservertempdb
- reportserver database
ms.assetid: 97b2e1b5-3869-4766-97b9-9bf206b52262
caps.latest.revision: "63"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4e8fe9877ea3e30466652a1cd4db8f4af53ba396
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="administer-a-report-server-database-ssrs-native-mode"></a>Verwalten einer Berichtsserver-Datenbank (einheitlicher SSRS-Modus)
  Eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung verwendet zwei relationale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken für den Zentralspeicher. Die Namen der Datenbanken lauten standardmäßig ReportServer und ReportServerTempdb. ReportServerTempdb wird mit der primären Berichtsserver-Datenbank erstellt und dient zur Speicherung von temporären Daten, Sitzungsinformationen und zwischengespeicherten Berichten.  
  
 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]umfassen die Aufgaben der Datenbankverwaltung das Sichern und Wiederherstellen der Berichtsserver-Datenbanken sowie das Verwalten der Verschlüsselungsschlüssel, mit denen vertrauliche Daten verschlüsselt und entschlüsselt werden.  
  
 Für die Verwaltung der Berichtsserver-Datenbanken enthält [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Reihe von Tools.  
  
-   Zum Sichern oder Wiederherstellen der Berichtsserver-Datenbank, zum Verschieben einer Berichtsserver-Datenbank oder zum Wiederherstellen einer Berichtsserver-Datenbank können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehle oder die Eingabeaufforderungs-Hilfsprogramme für Datenbanken verwenden. Weitere Informationen finden Sie unter [Verschieben von Berichtsserver-Datenbanken auf einen anderen Computer (einheitlicher SSRS-Modus)](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md) in der SQL Server-Onlinedokumentation.  
  
-   Um vorhandene Datenbankinhalte in eine andere Berichtsserver-Datenbank zu kopieren, können Sie eine Kopie einer Berichtsserver-Datenbank anfügen und sie mit einer anderen Berichtsserverinstanz verwenden. Oder Sie können ein Skript erstellen und ausführen, das SOAP-Aufrufe verwendet, um Berichtsserverinhalte in einer neuen Datenbank neu zu erstellen. Sie können das Hilfsprogramm **rs** verwenden, um das Skript auszuführen.  
  
-   Um Verbindungen zwischen dem Berichtsserver und der Berichtsserver-Datenbank zu verwalten und um festzustellen, welche Berichtsserver-Datenbank von einer bestimmten Berichtsserverinstanz verwendet wird, steht Ihnen die Seite "Setup" der Datenbank im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Konfigurationstool zur Verfügung. Weitere Informationen zur Berichtsserververbindung mit der Datenbank finden Sie unter [Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="sql-server-login-and-database-permissions"></a>SQL Server-Anmelde- und Datenbankberechtigungen  
 Die Berichtsserver-Datenbanken werden intern vom Berichtserver verwendet. Die Verbindungen zu Datenbanken werden durch den Berichtsserverdienst hergestellt. Mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool können Sie die Berichtsserververbindung zur Berichtsserver-Datenbank konfigurieren.  
  
 Bei den Anmeldeinformationen für die Berichtsserververbindung zur Datenbank kann es sich um das Dienstkonto, ein lokales Benutzerkonto oder Domänenbenutzerkonto unter Windows oder einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankbenutzer handeln. Sie müssen ein vorhandenes Konto für die Verbindung auswählen; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erstellt keine Konten für Sie.  
  
 Eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung für die Berichtsserver-Datenbank wird automatisch für das von Ihnen angegebene Konto erstellt.  
  
 Berechtigungen für die Datenbank werden auch automatisch konfiguriert. Das Reporting Services-Konfigurationstool weist das Konto oder den Datenbankbenutzer der **Public** -Rolle und der **RSExecRole** -Rolle für die Berichtsserver-Datenbanken hinzu. **RSExecRole** bietet Berechtigungen für den Zugriff auf die Datenbanktabellen und für das Ausführen von gespeicherten Prozeduren. **RSExecRole** wird in master und msdb erstellt, wenn Sie die Berichtsserver-Datenbank erstellen. **RSExecRole** ist ein Mitglied der **db_owner** -Rolle für die Berichtsserver-Datenbanken, mit der der Berichtsserver sein eigenes Schema zur Unterstützung eines automatischen Upgradeprozesses aktualisieren kann.  
  
## <a name="naming-conventions-for-the-report-server-databases"></a>Benennungskonventionen für die Berichtsserver-Datenbanken  
 Beim Erstellen der primären Datenbank muss der Name der Datenbank den Regeln für [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md)entsprechen. Der Name der temporären Datenbank besteht immer aus dem Namen der primären Berichtsserver-Datenbank und dem Suffix Tempdb. Sie können keinen anderen Namen für die temporäre Datenbank auswählen.  
  
 Das Umbenennen einer Berichtsserver-Datenbank wird nicht unterstützt, da die Berichtsserver-Datenbanken als interne Komponenten betrachtet werden. Das Umbenennen der Berichtsserver-Datenbanken führt zu Fehlern. Besonders wenn Sie die primäre Datenbank umbenennen, wird in einer Fehlermeldung darauf hingewiesen, dass die Datenbanknamen nicht synchronisiert sind. Wenn Sie die ReportServerTempdb-Datenbank umbenennen, tritt später beim Ausführen von Berichten der folgende interne Fehler auf:  
  
 "Interner Fehler beim Berichtsserver. Weitere Informationen finden Sie im Fehlerprotokoll. (rsInternalError)  
  
 Ungültiger Objektname 'ReportServerTempDB.dbo.PersistedStream'."  
  
 Dieser Fehler tritt auf, weil der ReportServerTempdb-Name intern gespeichert und von gespeicherten Prozeduren zum Ausführen interner Vorgänge verwendet wird. Nach dem Umbenennen der temporären Datenbank können die gespeicherten Prozeduren nicht mehr ordnungsgemäß ausgeführt werden.  
  
## <a name="enabling-snapshot-isolation-on-the-report-server-database"></a>Aktivieren von Momentaufnahmeisolation auf der Berichtsserver-Datenbank  
 Sie können keine Momentaufnahmeisolation auf der Berichtsserver-Datenbank aktivieren. Wenn die Momentaufnahmeisolation nicht aktiviert ist, tritt folgender Fehler auf: "Der ausgewählte Bericht ist nicht bereit für die Anzeige. Der Bericht wird immer noch gerendert, oder eine Berichtsmomentaufnahme ist nicht verfügbar."  
  
 Wenn Sie die Momentaufnahmeisolation nicht absichtlich aktiviert haben, wurde das Attribut unter Umständen von einer anderen Anwendung festgelegt oder für die **model** -Datenbank ist die Momentaufnahmeisolation aktiviert, sodass alle neuen Datenbanken diese Einstellung übernehmen.  
  
 Um die Momentaufnahmeisolation auf der Berichtsserver-Datenbank zu deaktivieren, starten Sie Management Studio, öffnen Sie ein neues Abfragefenster, fügen Sie den Skripttext ein, und führen Sie das Skript aus:  
  
```  
ALTER DATABASE ReportServer  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServerTempdb  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServer  
SET READ_COMMITTED_SNAPSHOT OFF  
ALTER DATABASE ReportServerTempDb  
SET READ_COMMITTED_SNAPSHOT OFF  
```  
  
## <a name="about-database-versions"></a>Informationen zu Datenbankversionen  
 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]stehen keine expliziten Informationen zur Datenbankversion zur Verfügung. Da Datenbankversionen jedoch immer mit Produktversionen synchronisiert werden, können Sie anhand der Informationen zur Produktversion erkennen, wenn sich die Datenbankversion geändert hat. Die Informationen zur Produktversion für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] werden über die Dateiversionsinformationen in den Protokolldateien, in den Headern aller SOAP-Aufrufe und beim Herstellen einer Verbindung mit der Berichtsserver-URL angezeigt (z.B. beim Öffnen eines Browsers und Eingabe von `http://localhost/reportserver`).  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Erstellen einer Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Sicherungs- und Wiederherstellungsvorgänge für Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)   
 [Berichtsserver-Datenbank &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Speichern verschlüsselter Berichtsserverdaten (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
