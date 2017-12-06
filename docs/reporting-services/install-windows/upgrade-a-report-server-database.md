---
title: Upgraden der Berichtsserver-Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- report server database
- upgrading Reporting Services
ms.assetid: 4091cf87-9d97-4048-a393-67f1f9207401
caps.latest.revision: "44"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 55aed4c570c7b83e5c462550e1a0a63adef097c7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="upgrade-a-report-server-database"></a>Aktualisieren der Berichtsserver-Datenbank

Die Berichtsserver-Datenbank ermöglicht die Speicherung für mindestens eine Berichtsserverinstanz. Da sich das Berichtsserver-Datenbankschema mit jeder neuen Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ändern kann, muss die Datenbankversion mit der Version der verwendeten Berichtsserverinstanz übereinstimmen. In den meisten Fällen kann eine Berichtsserver-Datenbank automatisch aktualisiert werden, ohne dass Sie aktiv werden müssen.  
  
 **Einheitlicher Modus:** Bei [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus besteht die Berichtsserver-Datenbank tatsächlich aus zwei Datenbanken mit dem Standardnamen „ReportServer“ und „ReportServerTempDB“.  
  
 **SharePoint-Modus:** Im Reporting Services SharePoint-Modus von SQL Server 2016 entspricht die Berichtsserver-Datenbank tatsächlich einer Sammlung von Datenbanken, die für die einzelnen Instanzen der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung erstellt werden.  

## <a name="ways-to-upgrade-a-native-mode-report-server-database"></a>Methoden zum Aktualisieren einer Berichtsserver-Datenbank im einheitlichen Modus

 Die folgende Liste gibt die Bedingungen an, unter denen ein Upgrade einer Berichtsserver-Datenbank durchgeführt wird:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Das Setup aktualisiert eine einzelne Instanz eines Berichtsservers. Das Berichtsserver-Datenbankschema wird automatisch aktualisiert, nachdem der Dienst gestartet und vom Berichtsserver festgestellt wurde, dass die Datenbankschemaversion nicht mit der Serverversion übereinstimmt.  
  
     Bei Dienststart überprüft der Berichtsserver die Datenbankschemaversion, um zu verifizieren, dass sie mit der Serverversion übereinstimmt. Falls die Datenbankschemaversion in einer älteren Version vorliegt, wird sie automatisch auf die Schemaversion aktualisiert, die der Berichtsserver benötigt. Das automatische Upgrade ist besonders nützlich, wenn Sie eine ältere Berichtsserver-Datenbank wiederhergestellt oder angefügt haben. Eine Meldung wird in die Ablaufverfolgungsprotokolldatei des Berichtsservers eingegeben, die angibt, dass die Datenbankschemaversion aktualisiert wurde.  
  
-   Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager aktualisiert eine lokale oder Remoteberichtsserver-Datenbank, wenn Sie eine ältere Version mit einer neueren Berichtsserver-Instanz verwenden möchten. In diesem Fall müssen Sie die Upgradeaktion bestätigen, bevor dieser Vorgang ausgeführt wird.  
  
     Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager stellt keine separate Schaltfläche zum Aktualisieren und kein Upgradeskript mehr bereit. Diese Funktionen sind beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] aufgrund der Funktion zum automatischen Upgrade des Berichtsserverdiensts veraltet.  
  
 Nach Upgrade des Schemas können Sie kein Rollback zum Upgrade einer früheren Version ausführen. Sichern Sie immer die Berichtsserver-Datenbank für den Fall, dass Sie eine vorherige Installation wiederherstellen müssen.  
  
## <a name="how-the-schema-metadata-and-report-server-content-is-updated"></a>Aktualisieren von Schema, Metadaten und Berichtsserverinhalt  
 Die Berichtsserver-Datenbank wird in drei Phasen aktualisiert:  
  
1.  Das Schema wird nach dem Setup und dem Starten des Diensts oder bei Auswahl einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Berichtsserver-Datenbank im einheitlichen Modus im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager, die in einer älteren Version vorliegt, automatisch aktualisiert. Außerdem überprüft der Berichtsserverdienst die Datenbankversion beim Start. Wenn der Berichtsserver mit einer Datenbank einer früheren Version verbunden wird, aktualisiert der Berichtsserver die Datenbank beim Start.  
  
2.  Sicherheitsbeschreibungen werden bei der ersten Verwendung der Berichtsserver-Datenbank nach der Aktualisierung des Schemas aktualisiert.  
  
3.  Veröffentlichte Berichte und kompilierte Berichtsmomentaufnahmen werden bei der ersten Verwendung aktualisiert. Weitere Informationen finden Sie unter [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
 Neben der Berichtsserver-Datenbank verwendet ein Berichtsserver auch eine temporäre Datenbank. Die temporäre Datenbank wird automatisch aktualisiert, wenn Sie die Berichtsserver-Datenbank aktualisieren.  
  
## <a name="permissions-required-to-upgrade-a-report-server-database"></a>Erforderliche Berechtigungen, um eine Berichtsserverdatenbank zu aktualisieren  
 Wenn Sie eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation aktualisieren, die eine Berichtsserver-Datenbank enthält, wird möglicherweise eine Fehlermeldung angezeigt, wenn das Datenbankupgrade mit ungenügenden Berechtigungen ausgeführt wird. Standardmäßig wird vom Setup das Sicherheitstoken des Benutzers, der das Setupprogramm ausführt, verwendet, um eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Remoteinstanz herzustellen und das Schema zu aktualisieren. Wenn Sie für den Datenbankserver, der die Berichtsserver-Datenbanken hostet, über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** permissions on the database server that hosts the report server databases, the database upgrade will succeed. Wenn Sie das Setup von der Eingabeaufforderung ausführen und die Argumente RSUPGRADEDATABASEACCOUNT und RSUPGRADEPASSWORD für ein Konto angeben, das über die **sysadmin** -Berechtigung zum Ändern des Schemas auf dem Remotecomputer verfügt, kann das Datenbankupgrade ebenfalls erfolgreich ausgeführt werden.  
  
 Wenn Sie jedoch keine **sysadmin** -Berechtigung für die Datenbank auf dem Remotecomputer haben, wird die Verbindung mit folgender Fehlermeldung abgelehnt:  
  
 `"Setup was not able to upgrade the report server database schema. You must update the database schema manually after setup is finished. To update the schema, run the Reporting Services Configuration Manager, open the Database Setup page, re-select the database, and click Apply. The database will be upgraded automatically."`  
  
 Zu diesem Zeitpunkt werden die Berichtsserver-Programmdateien aktualisiert, aber die Berichtsserver-Datenbank behält das Format der vorherigen Version bei. Der Berichtsserver ist nicht verfügbar, bis Sie den Upgradevorgang beenden, indem Sie ein Upgrade der Datenbank manuell durchführen.  
  
#### <a name="to-upgrade-a-native-mode-database-with-scripts"></a>So aktualisieren Sie eine Datenbank im einheitlichen Modus mithilfe von Skripts  
 Sie können mithilfe von WMI-Skripts eine Berichtsserverdatenbank aktualisieren. Weitere Informationen finden Sie unter [GenerateDatabaseUpgradeScript Method &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md).  
  
## <a name="next-steps"></a>Nächste Schritte

[Konfigurations-Manager für Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
[Erstellen einer Berichtsserver-Datenbank](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
[Assistent zum Ändern der Datenbank](http://msdn.microsoft.com/library/1a2e8d18-5997-482f-a9c1-87d99f7407b8)   
[Aktualisieren und Migrieren von Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Migrieren einer Installation von Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
