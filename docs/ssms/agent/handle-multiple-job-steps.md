---
title: Handhaben mehrerer Auftragsschritte | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6c7474d555c03a9ce9d02afaf613146e7d638ba8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="handle-multiple-job-steps"></a>Handhaben mehrerer Auftragsschritte
Wenn Ihr Auftrag aus mehr als einem Auftragsschritt besteht, müssen Sie die Reihenfolge angeben, in der die Auftragsschritte ausgeführt werden. Dies wird *Ablaufsteuerung* genannt*.* Sie können jederzeit neue Auftragsschritte hinzufügen und den Ablauf der Auftragsschritte neu ordnen. Die Änderungen werden bei der nächsten Ausführung des Auftrags wirksam. In dieser Abbildung ist die Ablaufsteuerung eines Auftrags für die Datenbanksicherung dargestellt.  
  
![Ablaufsteuerung für SQL Server-Agent-Auftragsschritte](../../ssms/agent/media/dbflow01.gif "Ablaufsteuerung für SQL Server-Agent-Auftragsschritte")  
  
Der erste Schritt besteht in der Datenbanksicherung. Wenn dieser Schritt einen Fehler erzeugt, wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ein Fehler an den Ausführenden berichtet, der als Empfänger der Benachrichtigung definiert ist. Wenn der Schritt zur Datenbanksicherung erfolgreich ist, wird vom Auftrag der nächste Schritt ausgeführt, das "Bereinigen" der Kundendaten. Wenn dieser Schritt einen Fehler erzeugt, wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent der Ablauf mit der Datenbankwiederherstellung fortgesetzt. Wenn die Bereinigung der Benutzerdaten erfolgreich ist, wird der Auftrag mit dem nächsten Schritt fortgesetzt, beispielsweise Aktualisieren der Statistik und so weiter, bis der letzte Schritt entweder einen Erfolg oder einen Fehler des Berichts zum Ergebnis hat.  
  
Sie definieren eine Ablaufsteuerungsaktion für die erfolgreiche oder fehlgeschlagene Ausführung einzelner Auftragsschritte. Sie müssen eine Aktion angeben, die durchgeführt werden soll, wenn ein Auftragsschritt erfolgreich ausgeführt wird, und eine Aktion für den Fall, dass ein Auftragsschritt einen Fehler erzeugt. Sie können zudem die Anzahl der Wiederholungsversuche und der Intervalle zwischen diesen Versuchen bei fehlgeschlagenen Auftragsschritten definieren.  
  
> [!NOTE]  
> Wenn Sie einen oder mehrere Schritte über die grafische Benutzeroberfläche (Graphical User Interface, GUI) des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents aus einem Auftrag mit mehreren Schritten löschen, entfernt die GUI alle Auftragsschritte und fügt die verbleibenden Schritte mit den richtigen Verweisen bei Erfolg oder bei Fehler wieder hinzu. Angenommen, ein Auftrag besteht aus fünf Schritten, und der erste Schritt ist so konfiguriert, dass er bei erfolgreichem Abschluss zu Schritt 4 springt. Wenn Sie Schritt 3 löschen, entfernt die GUI alle Schritte für diesen Auftrag und fügt die verbleibenden Schritte (1, 2, 4 und 5) mit den korrigierten Verweisen wieder hinzu. In diesem Fall wird der Verweis in Schritt 1 neu konfiguriert, damit der Vorgang bei erfolgreichem Abschluss von Schritt 1 mit Schritt 3 fortgesetzt wird.  
  
Auftragsschritte müssen eigenständig sein. Ein Auftrag kann keine booleschen Werte, Daten oder numerischen Werte zwischen den Auftragsschritten übergeben. Sie können allerdings Werte von einem [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritt zu einem anderen mithilfe von dauerhaften Tabellen oder globalen temporären Tabellen übergeben. Sie können Werte von Auftragsschritten, die Programme von einem Auftragsschritt zum nächsten ausführen, mithilfe von Dateien übergeben. Von einer Datei, die von einem Auftragsschritt ausgeführt wird, kann beispielsweise in eine Datei geschrieben werden, und von einer Datei, die von einem nachfolgenden Auftragsschritt ausgeführt wird, kann die Datei gelesen werden.  
  
> [!NOTE]  
> Sollten Sie Auftragsschritte erstellen, die sich in einer Schleife gegenseitig aufrufen (auf Auftragsschritt 1 folgt Auftragsschritt 2, dann kehrt Auftragsschritt 2 zu Auftragsschritt 1 zurück), wird eine Warnmeldung angezeigt, wenn der Auftrag mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]erstellt wird.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent zeichnet die Informationen von Aufträgen und Auftragsschritten im Auftragsverlauf auf.  
  
## <a name="see-also"></a>Siehe auch  
[sp_add_job](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
[sysjobs (Transact-SQL)](http://msdn.microsoft.com/en-us/e244a6a5-54c2-47a6-8039-dd1852b0ae59)  
[sysjobsteps](http://msdn.microsoft.com/en-us/978b8205-535b-461c-91f3-af9b08eca467)  
[Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)  
[Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)  
  

