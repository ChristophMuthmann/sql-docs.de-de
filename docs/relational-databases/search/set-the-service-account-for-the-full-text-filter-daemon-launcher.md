---
title: "Festlegen des Dienstkontos f&#252;r das Startprogramm des Volltextfilterdaemon | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Volltextsuche [SQL Server], Dienstkonto für das FDHOST-Startprogramm (MSSQLFDLauncher)"
  - "FDHOST-Startprogramm (MSSQLFDLauncher) [SQL Server]"
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
caps.latest.revision: 50
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 49
---
# Festlegen des Dienstkontos f&#252;r das Startprogramm des Volltextfilterdaemon
  In diesem Thema wird beschrieben, wie Sie das Dienstkonto für den SQL-Volltextfilterdaemon-Startprogrammdienst (MSSQLFDLauncher) mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers festlegen. Der SQL-Volltextfilterdaemon-Startprogrammdienst wird von der ssNoVersion-Volltextsuche zum Starten des Filterdaemon-Hostprozesses verwendet, der für das Filtern bei der Volltextsuche und die Wörtertrennung verantwortlich ist. Dieser Dienst muss ausgeführt werden, damit die Volltextsuche verwendet werden kann.  
  
 Der SQL-Volltextfilterdaemon-Startprogrammdienst ist ein instanzabhängiger Dienst, dem eine bestimmte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnet ist. Das Startprogramm für SQL-Volltextfilterdaemon verteilt die Dienstkontoinformationen an jeden Filterdaemon-Hostprozess.  
  
##  <a name="TOP"></a> In diesem Abschnitt  
  
-   [Empfehlungen zur Sicherheit](#rec)  
  
-   [Festlegen des Dienstkontos](#setting)  
  
-   [Wenn der SQL-Volltextfilterdaemon-Startprogrammdienst nicht startet](#error)  
  
##  <a name="setting"></a> Festlegen des Dienstkontos  
  
#### So legen Sie das Konto des SQL-Volltextfilterdaemon-Startprogrammdiensts für die Volltextsuche fest  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
2.  Klicken Sie im **SQL Server-Konfigurations-Manager** auf **SQL Server-Dienste**, klicken Sie mit der rechten Maustaste auf **SQL-Volltextfilterdaemon-Startprogramm (***Instanzname***)**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld auf die Registerkarte **Anmelden**, und wählen Sie anschließend das Konto aus, unter dem die vom SQL-Volltextfilterdaemon-Startprogrammdienst erstellten Prozesse ausgeführt werden sollen, oder geben Sie das Konto ein.  
  
4.  Klicken Sie nach dem Schließen des Dialogfelds auf **Neu starten**, um den SQL-Volltextfilterdaemon-Startprogrammdienst neu zu starten.  
  
 [In diesem Abschnitt](#TOP)  
  
##  <a name="error"></a> Wenn der SQL-Volltextfilterdaemon-Startprogrammdienst nicht startet  
 Wenn der SQL-Volltextfilterdaemon-Startprogrammdienst nicht startet, kann dies durch einen der folgenden Punkte bedingt sein:  
  
-   Das Kennwort des Kontos für das Konto des SQL-Volltextfilterdaemon-Startprogrammdiensts ist abgelaufen.  
  
     Wenn Sie ein lokales Benutzerkonto für den SQL-Volltextfilterdaemon-Startprogrammdienst verwenden und das Kennwort abgelaufen ist, müssen Sie folgende Schritte ausführen:  
  
    1.  Legen Sie ein neues Windows-Kennwort für das Konto fest.  
  
    2.  Aktualisieren Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager den SQL-Volltextfilterdaemon-Startprogrammdienst, damit dieser ebenfalls das neue Kennwort verwendet.  
  
-   Das Benutzerkonto oder Kennwort des Dienstkontos ist falsch.  
  
     Der SQL-Volltextfilterdaemon-Startprogrammdienst könnte versuchen, sich mit einem falschem Benutzerkonto und Kennwort anzumelden. Folgen Sie den oben stehenden Prozeduren, um zu überprüfen, ob das Benutzerkonto für den Dienst geändert wurde.  
  
-   Das Konto, das für die Anmeldung beim Dienst verwendet wird, besitzt keine entsprechenden Privilegien.  
  
     Sie verwenden möglicherweise ein Konto, das nicht über Anmelderechte auf dem Computer, auf dem die Instanz des Servers ausgeführt wird, verfügt. Stellen Sie sicher, dass Sie mit einem Konto angemeldet sind, das über Benutzerrechte und Berechtigungen auf dem lokalen Computer verfügt.  
  
-   Eine andere Instanz der gleichen Named Pipe wird bereits ausgeführt.  
  
     Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst fungiert als Named Pipe-Server für den Client des SQL-Volltextfilterdaemon-Startprogrammdiensts. Wenn die Named Pipe bereits vor dem Starten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem anderen Prozess erstellt wurde, wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll und im Windows-Ereignisprotokoll ein Fehler ausgegeben. Die Volltextsuche kann nicht ausgeführt werden.  Stellen Sie fest, welcher Prozess bzw. welche Anwendung versucht, die Named Pipe zu verwenden, und beenden Sie die betreffende Anwendung.  
  
-   Der SQL-Volltextfilterdaemon-Startprogrammdienst ist nicht ordnungsgemäß konfiguriert.  
  
     Der Dienst wurde möglicherweise nicht ordnungsgemäß auf dem lokalen Computer konfiguriert.  
  
     Wenn die Named Pipe-Funktion auf dem lokalen Computer deaktiviert wurde oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Verwendung einer anderen als der standardmäßigen Named Pipe konfiguriert wurde, wird das Startprogramm für SQL-Volltextfilterdaemon u. U. nicht gestartet.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstgruppe besitzt keine Berechtigung zum Starten des Startprogramms für SQL-Volltextfilterdaemon.  
  
     Bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstgruppe die Standardberechtigung zum Verwalten, Abfragen und Starten des SQL-Volltextfilterdaemon-Startprogrammdiensts erteilt. Wenn die Berechtigungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstgruppe für das Dienstkonto des SQL-Volltextfilterdaemon-Startprogramms nach der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt wurden, wird der SQL-Volltextfilterdaemon-Startprogrammdienst nicht gestartet und die Volltextsuche ist deaktiviert. Stellen Sie sicher, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstgruppe über Berechtigungen für das Dienstkonto des SQL-Volltextfilterdaemon-Startprogramms verfügt.  
  
 [In diesem Abschnitt](#TOP)  
  
## Siehe auch  
 [Verwalten von Diensten: Themen zur Vorgehensweise &#40;SQL Server-Konfigurations-Manager&#41;](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)   
 [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md)  
  
  