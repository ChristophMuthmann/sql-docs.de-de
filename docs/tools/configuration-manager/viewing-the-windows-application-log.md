---
title: "Anzeigen des Windows-Anwendungsprotokolls | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anwendungsprotokolle [SQL Server]"
  - "Windows-Anwendungsprotokolle [SQL Server]"
  - "Ansehen von Windows-Anwendungsprotokollen"
  - "Fehler [SQL Server], Protokolle"
  - "Systemprotokolle [SQL Server]"
  - "Sicherheitsprotokolle [SQL Server]"
  - "Anzeigen von Windows-Anwendungsprotokollen"
  - "Protokolle [SQL Server], Windows-Anwendungsprotokolle"
ms.assetid: f9853b74-7db7-47cc-b957-e49ed5bc0a1a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Anzeigen des Windows-Anwendungsprotokolls
  Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] so konfiguriert wurde, dass das Microsoft Windows-Anwendungsprotokoll verwendet wird, schreibt jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sitzung neue Ereignisse in dieses Protokoll. Im Gegensatz zum Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird beim Starten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz nicht jedes Mal ein neues Anwendungsprotokoll erstellt.  
  
 Das Windows-Anwendungsprotokoll können Sie mit der Windows-Ereignisanzeige oder dem Protokoll-Viewer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen und verwalten.  
  
 Es gibt drei Protokolle, die mit der Ereignisanzeige angezeigt werden können.  
  
|Windows-Protokolltyp|Description|  
|----------------------|-----------------|  
|Systemprotokoll|Zeichnet Ereignisse auf, die von den Windows-Betriebssystemkomponenten protokolliert werden. Wenn beispielsweise ein Treiber oder eine andere Systemkomponente beim Starten nicht geladen wird, wird dies im Systemprotokoll aufgezeichnet.|  
|Sicherheitsprotokoll|Zeichnet Sicherheitsereignisse auf, wie z. B. fehlgeschlagene Anmeldeversuche. Dadurch können Änderungen am Sicherheitssystem nachverfolgt und mögliche Verstöße gegen die Sicherheit erkannt werden. So können z. B. Versuche einer Anmeldung am System im Sicherheitsprotokoll aufgezeichnet werden, je nach Überwachungseinstellungen im Benutzer-Manager.<br /><br /> Ausschließlich Mitglieder der festen Serverrolle **sysadmin** können das Sicherheitsprotokoll anzeigen.|  
|Anwendungsprotokoll|Zeichnet Ereignisse auf, die von Anwendungen protokolliert werden. So kann eine Datenbankanwendung beispielsweise einen Dateifehler im Anwendungsprotokoll aufzeichnen.|  
  
 Weitere Informationen zum Verwenden der Ereignisanzeige und zum Verwalten des Anwendungsprotokolls sowie Erklärungen zu den angezeigten Informationen finden Sie in der Windows-Dokumentation.  
  
 **So zeigen Sie das Anwendungsprotokoll von Windows an**  
  
 [Anzeigen des Anwendungsprotokolls von Windows &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows.md)  
  
  