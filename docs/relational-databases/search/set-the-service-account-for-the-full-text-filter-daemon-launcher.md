---
title: "Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemon | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4f860080278519f5c9a68619ee5a9e8c0a2292f9
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemon
 In diesem Thema wird beschrieben, wie Sie das Dienstkonto für den SQL-Volltextfilterdaemon-Startprogrammdienst (MSSQLFDLauncher) mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers festlegen oder ändern. Das Standarddienstkonto, das von SQL Server-Setup verwendet wird ist `NT Service\MSSQLFDLauncher`.
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>Über den Startprogrammdienst für SQL-Volltextfilterdaemon
Der SQL-Volltextfilterdaemon-Startprogrammdienst wird von der SQL Server-Volltextsuche zum Starten des Filterdaemon-Hostprozesses verwendet, der für das Filtern bei der Volltextsuche und die Wörtertrennung verantwortlich ist. Der Startprogrammdienst muss ausgeführt werden, damit die Volltextsuche verwendet werden kann.  
  
Der SQL-Volltextfilterdaemon-Startprogrammdienst ist ein instanzabhängiger Dienst, dem eine bestimmte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugeordnet ist. Das Startprogramm für SQL-Volltextfilterdaemon verteilt die Dienstkontoinformationen an jeden Filterdaemon-Hostprozess, den es startet.  

##  <a name="setting"></a>Legen Sie das Dienstkonto fest  
  
1.  Zeigen Sie im Menü **Start** auf **Programme**, erweitern Sie [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], und klicken Sie anschließend auf **SQL Server 2016-Konfigurations-Manager**.  
  
2.  Klicken Sie im **SQL Server-Konfigurations-Manager**auf **SQL Server-Dienste**, klicken Sie mit der rechten Maustaste auf **SQL-Volltextfilterdaemon-Startprogramm (***Instanzname***)**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld auf die Registerkarte **Anmelden**, und wählen Sie anschließend das Konto aus, unter dem die vom SQL-Volltextfilterdaemon-Startprogrammdienst erstellten Prozesse ausgeführt werden sollen, oder geben Sie das Konto ein.  
  
4.  Klicken Sie nach dem Schließen des Dialogfelds auf **Neu starten** , um den SQL-Volltextfilterdaemon-Startprogrammdienst neu zu starten.  
  
![Prozesseigenschaften des Startprogramms für SQL-Volltextfilterdaemon](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="error"></a>Beheben Sie den Fehler des SQL-Volltextfilterdaemon-Startprogrammdiensts, wenn er nicht startet  
 Wenn der Volltextfilterdaemon-Startprogrammdienst nicht startet, überprüfen Sie die folgenden möglichen Ursachen:  
  
### <a name="permissions-issues"></a>Berechtigungsprobleme
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstgruppe besitzt keine Berechtigung zum Starten des Startprogramms für SQL-Volltextfilterdaemon.  

     Stellen Sie sicher, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstgruppe über Berechtigungen für das Dienstkonto des SQL-Volltextfilterdaemon-Startprogramms verfügt. Bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstgruppe die Standardberechtigung zum Verwalten, Abfragen und Starten des SQL-Volltextfilterdaemon-Startprogrammdiensts erteilt. Wenn die Berechtigungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstgruppe für das Dienstkonto des SQL-Volltextfilterdaemon-Startprogramms nach der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt wurden, wird der SQL-Volltextfilterdaemon-Startprogrammdienst nicht gestartet und die Volltextsuche ist deaktiviert.     

-   Das Konto, das für die Anmeldung beim Dienst verwendet wird, besitzt keine entsprechenden Privilegien.  
  
     Sie verwenden möglicherweise ein Konto, das nicht über Anmelderechte auf dem Computer, auf dem die Instanz des Servers ausgeführt wird, verfügt. Stellen Sie sicher, dass Sie mit einem Konto angemeldet sind, das über Benutzerrechte und Berechtigungen auf dem lokalen Computer verfügt.  

### <a name="service-account-and-password-issues"></a>Dienstkonto- und Kennwort-Probleme
-   Das Benutzerkonto oder Kennwort des Dienstkontos ist falsch.  
  
     Stellen Sie sicher, dass der Dienst das richtige Konto und Kennwort in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 Konfigurations-Manager verwendet.  
  
-   Das Kennwort des Kontos für das Konto des SQL-Volltextfilterdaemon-Startprogrammdiensts ist abgelaufen.  
  
     Wenn Sie ein lokales Benutzerkonto für den SQL-Volltextfilterdaemon-Startprogrammdienst verwenden und das Kennwort abgelaufen ist, müssen Sie folgende Schritte ausführen:  
  
    1.  Legen Sie ein neues Windows-Kennwort für das Konto fest.  
  
    2.  Aktualisieren Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016-Konfigurations-Manager den SQL-Volltextfilterdaemon-Startprogrammdienst, damit dieser ebenfalls das neue Kennwort verwendet.  
  
### <a name="named-pipes-configuration-issues"></a>Probleme beim Konfigurieren von Named Pipes
-   Der SQL-Volltextfilterdaemon-Startprogrammdienst ist nicht ordnungsgemäß konfiguriert.  
  
     Wenn die Named Pipe-Funktion auf dem lokalen Computer deaktiviert wurde oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Verwendung einer anderen als der standardmäßigen Named Pipe konfiguriert wurde, wird das Startprogramm für SQL-Volltextfilterdaemon u. U. nicht gestartet.  
  
-   Eine andere Instanz der gleichen Named Pipe wird bereits ausgeführt.  
  
     Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst fungiert als Named Pipe-Server für den Client des SQL-Volltextfilterdaemon-Startprogrammdiensts. Wenn die Named Pipe bereits vor dem Starten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem anderen Prozess erstellt wurde, wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und im Windows-Ereignisprotokoll ein Fehler ausgegeben. Die Volltextsuche kann nicht ausgeführt werden.  Stellen Sie fest, welcher Prozess bzw. welche Anwendung versucht, die Named Pipe zu verwenden, und beenden Sie die betreffende Anwendung.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Diensten: Themen zur Vorgehensweise &#40;SQL Server-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
