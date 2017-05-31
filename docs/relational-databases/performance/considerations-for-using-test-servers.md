---
title: Gesichtspunkte bei der Verwendung von Testservern | Microsoft-Dokumentation
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
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d23b44d09b5b1b38a1020ba9a04388f92119c28d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="considerations-for-using-test-servers"></a>Gesichtspunkte bei der Verwendung von Testservern
  Die Verwendung eines Testservers zur Optimierung einer Datenbank auf einem Produktionsserver ist ein wesentlicher Vorteil des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers. Mit dieser Funktion können Sie den Verarbeitungsaufwand für die Optimierung auf einen Testserver auslagern, ohne die tatsächlichen Daten vom Produktionsserver auf den Testserver zu kopieren.  
  
> [!NOTE]  
>  Die Funktion der Optimierung mit einem Testserver wird auf der grafischen Benutzeroberfläche (Graphical User Interface, GUI) des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers nicht unterstützt.  
  
 Lesen Sie die in den folgenden Abschnitten aufgeführten Punkte sorgfältig durch, um diese Funktion optimal einzusetzen.  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>Einrichten der Testserver-/Produktionsserverumgebung  
  
-   Der Benutzer, der mit einem Testserver eine Datenbank auf einem Produktionsserver optimieren möchte, muss auf beiden Servern einen Anmeldenamen besitzen. Andernfalls kann das Szenario nicht verwendet werden.  
  
-   Die erweiterte gespeicherte Prozedur **xp_msver**muss für die Verwendung des Testserver/Produktionsserver-Szenarios aktiviert sein. [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber ruft mit dieser erweiterten gespeicherten Prozedur die Anzahl der Prozessoren und den verfügbaren Arbeitsspeicher des Produktionsservers ab, die für die Optimierung des Testservers verwendet werden sollen. Ist **xp_msver** nicht aktiviert, verwendet der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber die Hardwaremerkmale des Computers, auf dem der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber ausgeführt wird. Sind die Hardwaremerkmale des Computers, auf dem der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber ausgeführt wird, nicht verfügbar, wird von einem Prozessor und 1024 MB Arbeitsspeicher ausgegangen. Diese erweiterte gespeicherte Prozedur wird standardmäßig aktiviert, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren. Weitere Informationen finden Sie unter [Oberflächenkonfiguration](../../relational-databases/security/surface-area-configuration.md) und [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber geht davon aus, dass die Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sowohl auf dem Testserver als auch auf dem Produktionsserver identisch sind. Bei verschiedenen Editionen hat die Edition auf dem Testserver Vorrang. Wird beispielsweise auf dem Testserver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard , ausgeführt, schließt der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber keine indizierten Sichten, Partitionierungen und Onlinevorgänge in seine Empfehlungen ein, selbst wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise auf dem Produktionsserver ausgeführt wird.  
  
## <a name="about-test-serverproduction-server-behavior"></a>Informationen zum Verhalten von Testserver und Produktionsserver  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber berücksichtigt Hardwareunterschiede zwischen dem Produktions- und dem Testserver beim Erstellen von Empfehlungen. Die Empfehlung lautet genau so, als wenn die Optimierung auf dem Produktionsserver erfolgt wäre.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber kann durch das Sammeln der Metadaten und die Erstellung der erforderlichen Statistiken für die Optimierung zusätzliche Arbeitsauslastung auf dem Produktionsserver verursachen.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber kopiert keine tatsächlichen Daten vom Produktionsserver auf den Testserver. Er kopiert lediglich die Metadaten der Datenbanken und die erforderlichen Statistiken.  
  
-   Alle Sitzungsinformationen werden in **msdb** auf dem Produktionsserver gespeichert. So können Sie einen beliebigen verfügbaren Testserver für die Optimierung verwenden, und die Informationen zu allen Sitzungen stehen an einer Stelle (auf dem Produktionsserver) zur Verfügung.  
  
## <a name="issues-related-to-the-shell-database"></a>Aspekte im Zusammenhang mit der Shelldatenbank  
  
-   Nach der Optimierung entfernt der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber alle Metadaten, die er während der Optimierung auf dem Testserver erstellt hat. Dazu gehört auch die Shelldatenbank. Wenn Sie eine Reihe von Optimierungssitzungen mit demselben Produktions- und demselben Testserver ausführen, ist es sinnvoll, die Shelldatenbank beizubehalten, um Zeit zu sparen. Geben Sie dazu in der XML-Eingabedatei das untergeordnete **RetainShellDB** -Element zusammen mit den anderen untergeordneten Elementen des übergeordneten **TuningOptions** -Elements an. Mit diesen Optionen wird der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Optimierungsratgeber veranlasst, die Shelldatenbank beizubehalten. Weitere Informationen finden Sie unter [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
-   Nach einer erfolgreichen Optimierungssitzung für einen Testserver/Produktionsserver können Shelldatenbanken auf dem Testserver verbleiben, selbst wenn Sie das Unterelement **RetainShellDB** nicht angegeben haben. Diese unerwünschten Shelldatenbanken können nachfolgende Optimierungssitzungen beeinträchtigen und sollten gelöscht werden, bevor Sie eine weitere Optimierungssitzung für einen Testserver/Produktionsserver ausführen. Wenn darüber hinaus eine Optimierungssitzung unerwartet beendet wird, verbleiben die Shelldatenbanken auf dem Testserver und die Objekte innerhalb dieser Datenbanken möglicherweise auf dem Testserver. Sie sollten auch diese Datenbanken und Objekte löschen, bevor Sie eine neue Optimierungssitzung für den Testserver/Produktionsserver starten.  
  
## <a name="issues-related-to-the-tuning-process"></a>Aspekte im Zusammenhang mit dem Optimierungsprozess  
  
-   Der Benutzer muss das Optimierungsprotokoll auf Optimierungsfehler überprüfen, die durch Unterschiede zwischen dem Produktions- und dem Testserver verursacht werden, und auf Fehler, die beim Kopieren von Metadaten vom Produktions- auf den Testserver entstehen. Beispielsweise ist ein Benutzeranmeldename auf dem Testserver nicht vorhanden. Ist ein Benutzeranmeldename auf dem Testserver nicht vorhanden, können die Ereignisse in der Arbeitsauslastung, die von diesem Benutzer ausgelöst werden, möglicherweise nicht optimiert werden. Verwenden Sie die grafische Benutzeroberfläche des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers, um das Optimierungsprotokoll anzuzeigen. Weitere Informationen finden Sie unter [Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  
  
-   Wenn der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber viele Ereignisse nicht optimieren kann, weil Objekte in der Shelldatenbank fehlen, die vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber auf dem Testserver erstellt wird, muss der Benutzer das Optimierungsprotokoll überprüfen. Ereignisse, die nicht optimiert werden können, sind im Protokoll aufgeführt. Um die Datenbank auf dem Testserver erfolgreich optimieren zu können, muss der Benutzer die fehlenden Objekte in der Shelldatenbank erstellen und dann eine neue Optimierungssitzung starten.  
  
-   Ist auf dem Testserver eine Datenbank mit demselben Namen bereits vorhanden, kopiert der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber keine Metadaten, sondern setzt die Optimierung fort und sammelt die erforderlichen Statistiken. Dies ist nützlich, wenn der Benutzer bereits eine Datenbank auf dem Testserver erstellt hat und vor dem Aufruf des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers die entsprechenden Metadaten kopiert hat.  
  
-   Ist die DATE_CORRELATION_OPTIMIZATION-Option für eine Datenbank auf dem Produktionsserver aktiviert, wird bei der Optimierung des Testservers kein vollständiges Skript für die Metadaten und die Daten zu dieser Option erstellt. Bei der Optimierung in einem Testserver/Produktionsserver-Szenario können die folgenden Probleme auftreten:  
  
    -   Benutzer können auf den Servern unterschiedliche Abfragepläne für Abfragen besitzen, die die DATE_CORRELATION_OPTIMIZATION-Option verwenden.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Möglicherweise schlägt der Optimierungsratgeber im Empfehlungsskript das Löschen von indizierten Sichten vor, die die DATE_CORRELATION_OPTIMIZATION-Option erzwingen.  
  
     Daher ist es unter Umständen sinnvoll, Empfehlungen des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers zu den indizierten Sichten, die Korrelationsstatistiken enthalten, zu ignorieren. Der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber kennt deren Kosten, aber nicht deren Vorteile. [!INCLUDE[ssDE](../../includes/ssde-md.md)] Der Optimierungsratgeber empfiehlt möglicherweise nicht die Auswahl bestimmter Indizes, wie z.B. gruppierter Indizes für **datetime** -Spalten, die jedoch bei aktivierter DATE_CORRELATION_OPTIMIZATION vorteilhaft sein könnten.  
  
     Wählen Sie die **is_date_correlation_view** -Spalte der [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md) -Katalogsicht aus, um zu bestimmen, ob eine Sicht auf Korrelationsstatistiken basiert.  
  
  
