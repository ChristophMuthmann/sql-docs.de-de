---
title: "Schreiben von SQL-Serverüberwachungsereignissen in das Sicherheitsprotokoll | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 268f1fbd8ea57db8626c84999a3454e4c4459511
ms.lasthandoff: 04/11/2017

---
# <a name="write-sql-server-audit-events-to-the-security-log"></a>Schreiben von SQL-Serverüberwachungsereignissen in das Sicherheitsprotokoll
  In einer Umgebung mit hoher Sicherheit ist das Windows-Sicherheitsprotokoll der geeignete Speicherort für Ereignisse, die Objektzugriffe aufzeichnen. Andere Überwachungsspeicherorte werden unterstützt, können aber leichter manipuliert werden.  
  
 Es gibt zwei Hauptanforderungen für das Schreiben von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Serverüberwachungen in das Windows-Sicherheitsprotokoll:  
  
-   Die Einstellungen für die Überwachung von Objektzugriffsversuchen müssen so konfiguriert sein, dass die Ereignisse aufgezeichnet werden. Das Tool für Überwachungsrichtlinien (`auditpol.exe`) macht eine Vielzahl von Einstellungen für Unterrichtlinien in der Kategorie **Überwachung von Objektzugriffsversuchen** verfügbar. Um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Überwachung des Objektzugriffs zu ermöglichen, konfigurieren Sie die Einstellung **automatisch generiert** .  
  
-   Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss über die Berechtigung zum **Generieren von Sicherheitsüberwachungen** verfügen, um in das Windows-Sicherheitsprotokoll schreiben zu können. Standardmäßig verfügen die Konten LOCAL SERVICE und NETWORK SERVICE über diese Berechtigung. Dieser Schritt ist nicht erforderlich, wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unter einem dieser Konten ausgeführt wird.  
  
 Die Windows-Überwachungsrichtlinie kann sich auf die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Überwachung auswirken, wenn sie so konfiguriert wurde, dass sie in das Windows-Sicherheitsprotokoll schreibt. In diesem Fall besteht bei einer falschen Konfiguration der Überwachungsrichtlinie die Gefahr, dass Ereignisse verloren gehen. Das Windows-Sicherheitsprotokoll ist standardmäßig so konfiguriert, dass ältere Ereignisse überschrieben werden. Hierdurch werden immer die neuesten Ereignisse beibehalten. Wurde das Windows-Sicherheitsprotokoll jedoch so festgelegt, dass ältere Ereignisse nicht überschrieben werden, löst das System das Windows-Ereignis 1104 aus, sobald das Sicherheitsprotokoll voll ist. In diesem Fall geschieht Folgendes:  
  
-   Es werden keine weiteren Sicherheitsereignisse aufgezeichnet.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kann nicht erkennen, dass das System keine Ereignisse mehr im Sicherheitsprotokoll aufzeichnen kann, sodass Überwachungsereignisse möglicherweise verloren gehen.  
  
-   Nachdem der Administrator das Sicherheitsprotokoll korrigiert hat, wird die Protokollierung wieder wie gewohnt ausgeführt.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So schreiben Sie SQL-Serverüberwachungsereignisse in das Sicherheitsprotokoll**  
  
     [Konfigurieren der Einstellung für die Überwachung von Objektzugriffsversuchen in Windows mit "auditpol"](#auditpolAccess)  
  
     [Konfigurieren der Einstellung für die Überwachung von Objektzugriffsversuchen in Windows mit "secpol"](#secpolAccess)  
  
     [Erteilen von Berechtigungen zum Generieren von Sicherheitsüberwachungen für ein Konto mit "secpol"](#secpolPermission)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Administratoren des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Computers sollten sich bewusst sein, dass lokale Einstellungen für das Sicherheitsprotokoll durch eine Domänenrichtlinie überschrieben werden können. In diesem Fall überschreibt die Domänenrichtlinie möglicherweise die Einstellung für die Unterkategorie (**auditpol /get /subcategory:"application generated"**). Dies kann sich auf die Fähigkeit von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auswirken, Ereignisse zu protokollieren. Dabei kann nicht nachvollzogen werden, dass die Ereignisse, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zu überwachen versucht, nicht aufgezeichnet werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen Windows-Administrator sein, um diese Einstellungen konfigurieren zu können.  
  
##  <a name="auditpolAccess"></a> So konfigurieren Sie die Einstellung für die Überwachung von Objektzugriffsversuchen in Windows mit "auditpol"  
  
1.  Öffnen Sie eine Eingabeaufforderung mit Administratorberechtigungen.  
  
    1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf **Zubehör**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
    2.  Wenn das Dialogfeld **Benutzerkontensteuerung** geöffnet wird, klicken Sie auf **Weiter**.  
  
2.  Führen Sie die folgende Anweisung aus, um die Überwachung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu aktivieren.  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  Schließen Sie das Eingabeaufforderungsfenster.  
  
##  <a name="secpolAccess"></a> So erteilen Sie die Berechtigung zum Generieren von Sicherheitsüberwachungen für ein Konto mit "secpol"  
  
1.  Klicken Sie in allen Windows-Betriebssystemen im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie **secpol.msc** ein, und klicken Sie dann auf **OK**. Wenn das Dialogfeld **Benutzerzugriffssteuerung** angezeigt wird, klicken Sie auf **Weiter**.  
  
3.  Erweitern Sie im Tool "Lokale Sicherheitsrichtlinie" die **Sicherheitseinstellungen**, erweitern Sie **Lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
4.  Doppelklicken Sie im Ergebnisbereich auf **Generieren von Sicherheitsüberwachungen**.  
  
5.  Klicken Sie auf der Registerkarte **Lokale Sicherheitseinstellung** auf **Benutzer oder Gruppe hinzufügen**.  
  
6.  Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** entweder den Namen des Benutzerkontos, z. B. **Domäne1\Benutzer1** ein, und klicken Sie dann auf **OK**, oder klicken Sie auf **Erweitert** , und suchen Sie nach dem Konto.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  Schließen Sie das Tool "Sicherheitsrichtlinie".  
  
9. Starten Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] neu, um diese Einstellung zu aktivieren.  
  
##  <a name="secpolPermission"></a> So konfigurieren Sie die Einstellung für die Überwachung von Objektzugriffsversuchen in Windows mit "secpol"  
  
1.  Wenn das Betriebssystem eine frühere Version als [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] oder Windows Server 2008 ist, klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie **secpol.msc** ein, und klicken Sie dann auf **OK**. Wenn das Dialogfeld **Benutzerzugriffssteuerung** angezeigt wird, klicken Sie auf **Weiter**.  
  
3.  Erweitern Sie im Tool "Lokale Sicherheitsrichtlinie" die **Sicherheitseinstellungen**, erweitern Sie **Lokale Richtlinien**, und klicken Sie dann auf **Überwachungsrichtlinie**.  
  
4.  Doppelklicken Sie im Ergebnisbereich auf **Objektzugriffsversuche überwachen**.  
  
5.  Wählen Sie im Bereich **Diese Versuche überwachen** auf der Registerkarte **Lokale Sicherheitseinstellung** sowohl **Erfolg** als auch **Fehler**aus.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Schließen Sie das Tool "Sicherheitsrichtlinie".  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Audit &#40;Datenbankmodul&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
