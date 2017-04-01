---
title: "Gespeicherte Prozeduren (Datenbankmodul) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-stored-Procs"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Speichern von Programmen als gespeicherte Prozeduren"
  - "Gespeicherte Prozeduren [SQL Server], Informationen zu gespeicherten Prozeduren"
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Gespeicherte Prozeduren (Datenbankmodul)
  Eine gespeicherte Prozedur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht einer oder mehreren [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen oder einem Verweis auf eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR-Methode (Common Language Runtime). Prozeduren sind mit Konstrukten anderer Programmiersprachen vergleichbar, da sie folgende Fähigkeiten aufweisen:  
  
-   Annehmen von Eingabeparametern und Zurückgeben mehrerer Werte in Form von Ausgabeparametern an das aufrufende Programm.  
  
-   Aufnehmen von Programmierungsanweisungen, die Vorgänge in der Datenbank ausführen. Dies schließt auch den Aufruf anderer Prozeduren ein.  
  
-   Zurückgeben eines Statuswerts an ein aufrufendes Programm, der Erfolg oder Misserfolg (sowie die Ursache für den Misserfolg) anzeigt.  
  
## <a name="benefits-of-using-stored-procedures"></a>Vorteile bei der Verwendung gespeicherter Prozeduren  
 In der folgenden Liste sind einige Vorteile bei der Verwendung von Prozeduren beschrieben.  
  
 Verringerter Netzwerkdatenverkehr zwischen Server und Client  
 Die Befehle in einer Prozedur werden als einzelner Codebatch ausgeführt. Dadurch lässt sich der Netzwerkdatenverkehr zwischen Server und Client erheblich reduzieren, da nur der Aufruf zum Ausführen der Prozedur über das Netzwerk gesendet wird. Wenn der Code nicht von einer Prozedur gekapselt würde, müsste jede einzelne Codezeile über das Netzwerk übertragen werden.  
  
 Höhere Sicherheit  
 Mithilfe einer Prozedur können mehrere Benutzer und Clientprogramme Vorgänge für zugrunde liegende Datenbankobjekte ausführen, selbst wenn die Benutzer und Programme keine direkte Berechtigungen für diese zugrunde liegenden Objekte aufweisen. Die Prozedur steuert, welche Prozesse und Aktivitäten ausgeführt werden, und schützt die zugrunde liegenden Datenbankobjekte. Dadurch ist es nicht erforderlich, Berechtigungen auf der individuellen Objektebene zu gewähren, was zu einer Vereinfachung der Sicherheitsebenen führt.  
  
 Die [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) -Klausel kann in der CREATE PROCEDURE-Anweisung angegeben werden, damit das Annehmen der Identität eines anderen Benutzers unterstützt wird, oder um Benutzern bzw. Anwendungen das Ausführen bestimmter Datenbankaktivitäten zu ermöglichen, ohne dass sie über direkte Berechtigungen für die zugrunde liegenden Objekte und Befehle verfügen. Einige Aktionen, wie beispielsweise TRUNCATE TABLE, besitzen keine erteilbaren Berechtigungen. Um TRUNCATE TABLE auszuführen, benötigt der Benutzer für die festgelegte Tabelle die ALTER-Berechtigungen. Die Erteilung der ALTER-Berechtigungen für eine Tabelle kann sich als nicht ideal erweisen, weil der Benutzer dann Berechtigungen besitzt, die über die Möglichkeit hinausgehen, die Tabelle abzuschneiden. Durch die Aufnahme der TRUNCATE TABLE-Anweisung in ein Modul und durch die Festlegung, dass das Modul als Benutzer mit der Berechtigung zur Tabellenänderung ausgeführt wird, können Sie die Berechtigungen zum Abschneiden der Tabelle auf alle Benutzer ausdehnen, denen Sie die EXECUTE-Berechtigungen für das Modul erteilen.  
  
 Wenn eine Prozedur über das Netzwerk aufgerufen wird, ist nur der Aufruf zum Ausführen der Prozedur sichtbar. Daher haben böswillige Benutzer keine Möglichkeit, die Namen von Tabellen- und Datenbankobjekten einzusehen, eigene [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen einzubetten oder wichtige Daten zu suchen.  
  
 Die Verwendung von Prozedurparametern bietet Schutz vor Angriffen durch Einschleusung von SQL-Befehlen. Da die Parametereingabe als Literalwert und nicht als ausführbarer Code behandelt wird, ist es für einen Angreifer schwieriger, einen Befehl in die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung(en) innerhalb der Prozedur einzufügen und die Sicherheit zu gefährden.  
  
 Prozeduren können verschlüsselt werden und helfen, den Quellcode zu verbergen. Weitere Informationen finden Sie unter [SQL Server Encryption](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Wiederverwendung von Code  
 Code für wiederholte Datenbankvorgänge ist besonders für die Kapselung in Prozeduren geeignet. Dies hat folgende Vorteile: Derselbe Code muss nicht ständig neu geschrieben werden, Codeinkonsistenzen werden verringert, und alle Benutzer oder Anwendungen, die über die notwendigen Berechtigungen verfügen, können auf den Code zugreifen und diesen ausführen.  
  
 Einfachere Wartung  
 Wenn Clientanwendungen Prozeduren aufrufen und Datenbankvorgänge auf die Datenebene beschränkt bleiben, müssen bei Änderungen in der zugrunde liegenden Datenbank nur die Prozeduren aktualisiert werden. Die Anwendungsebene bleibt von der Datenebene getrennt und ist von Änderungen an Datenbanklayouts, Beziehungen oder Prozessen nicht betroffen.  
  
 Verbesserte Leistung  
 Eine Prozedur wird standardmäßig bei der ersten Ausführung kompiliert. Gleichzeitig wird ein Ausführungsplan erstellt, der für nachfolgende Ausführungen wiederverwendet wird. Da vom Abfrageprozessor kein neuer Plan erstellt werden muss, wird für die Verarbeitung der Prozedur normalerweise weniger Zeit benötigt.  
  
 Nachdem an den Tabellen oder Daten, auf die die Prozedur verweist, umfangreichere Änderungen vorgenommen wurden, wird die Prozedur aufgrund des vorkompilierten Plans möglicherweise langsamer ausgeführt. In diesem Fall kann die Leistung durch eine Neukompilierung der Prozedur und eine erzwungene Neuerstellung des Ausführungsplans verbessert werden.  
  
## <a name="types-of-stored-procedures"></a>Typen von gespeicherten Prozeduren  
 Benutzerdefinierte Dateigruppe  
 Eine benutzerdefinierte Prozedur kann in einer benutzerdefinierten Datenbank sowie in allen Systemdatenbanken außer der **Ressourcendatenbank** erstellt werden. Die Prozedur kann entweder in [!INCLUDE[tsql](../../includes/tsql-md.md)] oder als Verweis auf eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR-Methode (Common Language Runtime) entwickelt werden.  
  
 Temporäre Prozeduren  
 Temporäre Prozeduren stellen eine Art benutzerdefinierter Prozedur dar. Temporäre Prozeduren verhalten sich wie dauerhafte Prozeduren, mit der Ausnahme, dass temporäre Prozeduren in **tempdb**gespeichert werden. Es gibt zwei Arten von temporären Prozeduren: lokale und globale temporäre Prozeduren. Sie unterscheiden sich hinsichtlich ihrer Namen, ihrer Sichtbarkeit und ihrer Verfügbarkeit. Die Namen lokaler temporärer Prozeduren beginnen mit einem einzelnen Nummernzeichen (#). Sie sind nur im Rahmen der aktuellen Benutzerverbindung sichtbar und werden gelöscht, sobald die Verbindung getrennt wird. Die Namen globaler temporärer Prozeduren beginnen mit zwei Nummernzeichen (##). Nachdem sie erstellt wurden, sind sie für jeden Benutzer sichtbar und werden am Ende der letzten Sitzung, in der die Prozedur verwendet wird, gelöscht.  
  
 System  
 Systemprozeduren sind in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthalten. Sie werden physisch in der internen, ausgeblendeten **Ressourcendatenbank** gespeichert und logisch im **sys** -Schema jeder system- und benutzerdefinierten Datenbank angezeigt. Außerdem verfügt die **msdb-Datenbank** über gespeicherte Systemprozeduren im **dbo** -Schema, die zum Planen von Warnungen und Aufträgen verwendet werden. Da Systemprozeduren mit dem Präfix **sp_** beginnen, wird davon abgeraten, dieses Präfix beim Benennen benutzerdefinierter Prozeduren zu verwenden. Eine vollständige Liste der systemgespeicherten Prozeduren finden Sie unter [Systemgespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Systemprozeduren, die eine Schnittstelle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu externen Programmen für verschiedene Wartungsaktivitäten bereitstellen. Diese erweiterten Prozeduren verwenden das Präfix xp_. Eine vollständige Liste der erweiterten Prozeduren finden Sie unter [Gespeicherte allgemeine erweiterte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md).  
  
 Erweiterte benutzerdefinierte Prozeduren  
 Mit erweiterten gespeicherten Prozeduren können externe Routinen in einer Programmiersprache wie C erstellt werden. Diese Prozeduren sind DLLs, die von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dynamisch geladen und ausgeführt werden können.  
  
> [!NOTE]  
>  Erweiterte gespeicherte Prozeduren werden in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Verwenden Sie dieses Feature nicht in einer neuen Entwicklungsarbeit, und ändern Sie Anwendungen, die dieses Feature verwenden, so schnell wie möglich. Erstellen Sie stattdessen CLR-Prozeduren. Diese Methode bietet eine robustere und sicherere Alternative zum Schreiben von erweiterten Prozeduren.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Taskbeschreibung**|**Thema**|  
|Beschreibt, wie eine gespeicherte Prozedur erstellt wird.|[Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)|  
|Beschreibt, wie eine gespeicherte Prozedur geändert wird.|[Ändern einer gespeicherten Prozedur](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)|  
|Beschreibt, wie eine gespeicherte Prozedur gelöscht wird.|[Löschen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)|  
|Beschreibt, wie eine gespeicherte Prozedur ausgeführt wird.|[Ausführen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)|  
|Beschreibt, wie Berechtigungen für eine gespeicherte Prozedur erteilt werden.|[Erteilen von Berechtigungen für eine gespeicherte Prozedur](../../relational-databases/stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|Beschreibt, wie Daten von einer gespeicherten Prozedur an eine Anwendung zurückgegeben werden.|[Zurückgeben von Daten von einer gespeicherten Prozedur](../../relational-databases/stored-procedures/return-data-from-a-stored-procedure.md)|  
|Beschreibt, wie eine gespeicherte Prozedur neu kompiliert wird.|[Erneutes Kompilieren einer gespeicherten Prozedur](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)|  
|Beschreibt, wie eine gespeicherte Prozedur umbenannt wird.|[Umbenennen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)|  
|Beschreibt, wie die Definition einer gespeicherten Prozedur angezeigt wird.|[Anzeigen der Definition einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)|  
|Beschreibt, wie die Abhängigkeiten von einer gespeicherten Prozedur angezeigt werden.|[Anzeigen der Abhängigkeiten einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)|  
|Beschreibt, wie Parameter in einer gespeicherten Prozedur verwendet werden.|[Parameter](../../relational-databases/stored-procedures/parameters.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [CLR-gespeicherte Prozeduren](../Topic/CLR%20Stored%20Procedures.md)  
  
  