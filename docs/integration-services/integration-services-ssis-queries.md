---
title: "Integration Services-Abfragen (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.querybuilder.f1"
helpviewer_keywords: 
  - "Abfrage-Generator [Integration Services]"
  - "Abfragen [Integration Services]"
  - "Anweisungen [Integration Services]"
  - "Abfragen [Integration Services], Informationen zu Abfragen in Paketen"
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Integration Services-Abfragen (SSIS)
  Der Task SQL ausführen, die OLE DB-Quelle, das OLE DB-Ziel und die Transformation für die Suche können SQL-Abfragen verwenden. In dem Task SQL ausführen können von SQL-Anweisungen Datenbankobjekte und Daten erstellt, aktualisiert und gelöscht sowie gespeicherte Prozeduren und SELECT-Anweisungen ausgeführt werden. In der OLE DB-Quelle und der Nachschlagetransformation sind die SQL-Anweisungen normalerweise SELECT- oder ECEC-Anweisungen. Von den letzteren werden am häufigsten gespeicherte Prozeduren ausgeführt, die Resultsets zurückgeben.  
  
 Eine Abfrage kann analysiert werden, um festzustellen, ob sie gültig ist. Beim Analysieren einer Abfrage, die eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet, wird die Abfrage analysiert, ausgeführt, und das Ausführungsergebnis (Erfolg oder Fehlgeschlagen) wird dem Analyseergebnis zugeordnet. Wenn die Abfrage eine Verbindung mit einer Datenquelle verwendet, die nicht zu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]gehört, wird nur die Anweisung analysiert.  
  
 Die SQL-Anweisung kann entweder durch direktes Eingeben in den Designer oder durch Angeben einer Dateiverbindung oder einer Variable, die eine Anweisung enthält, definiert werden.  
  
## Direkteingabe-SQL  
 Der Query-Generator steht für den Task SQL ausführen, die OLE DB-Quelle, das OLE DB-Ziel und die Transformation für die Suche zur Verfügung. Der Query-Generator bietet die folgenden Vorteile:  
  
-   Visuell oder mit SQL-Befehlen arbeiten.  
  
     Der Abfrage-Generator enthält grafische Bereiche, die eine Abfrage visuell darstellen, und einen Textbereich, der den SQL-Text der jeweiligen Abfrage anzeigt. Sie können entweder in grafischen oder in Textbereichen arbeiten. Der Abfrage-Generator synchronisiert die Sichten, sodass der Abfragetext und die grafische Darstellung immer übereinstimmen.  
  
-   Verknüpfen von verbundenen Tabellen.  
  
     Wenn Sie der Abfrage mehrere Tabellen hinzufügen, bestimmt der Abfrage-Generator automatisch, wie die Tabellen miteinander in Beziehung stehen, und erstellt den geeigneten Joinbefehl.  
  
-   Abfragen oder Aktualisieren von Datenbanken.  
  
     Sie können den Abfrage-Generator verwenden, um mithilfe von SELECT-Anweisungen von Transact-SQL Daten zurückzugeben und um Abfragen zu erstellen, die Datensätze einer Datenbank aktualisieren, einer Datenbank hinzufügen oder aus einer Datenbank löschen.  
  
-   Sofortiges Anzeigen und Bearbeiten der Ergebnisse.  
  
     Sie können die Abfrage ausführen und ein Recordset in einem Raster verwenden, das Ihnen das Durchführen eines Bildlaufs und Bearbeiten der Datensätze in der Datenbank ermöglicht.  
  
 Obwohl der Abfrage-Generator visuell auf das Erstellen von SELECT-Abfragen beschränkt ist, können Sie den SQL-Code für andere Typen von Anweisungen wie z. B. DELETE und UPDATE in den Textbereich eingeben. Der grafische Bereich wird automatisch entsprechend der eingegebenen SQL-Anweisung aktualisiert.  
  
 Die Direkteingabe kann auch durch Eingeben der Abfrage in das Dialogfeld des Tasks oder der Datenflusskomponente oder in das Eigenschaften-Fenster erfolgen.  
  
 Weitere Informationen finden Sie unter [Query Builder](../Topic/Query%20Builder.md).  
  
## SQL in Dateien  
 Die SQL-Anweisung für den Task "SQL ausführen" kann sich auch in einer getrennten Datei befinden. Sie können z. B. Abfragen mithilfe von Tools wie beispielsweise dem Abfrage-Editor in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]schreiben, die Abfrage in einer Datei speichern und dann die Abfrage aus dieser Datei auslesen, wenn ein Paket ausgeführt wird. Die Datei darf nur die auszuführenden SQL-Anweisungen sowie Kommentare enthalten. Zum Verwenden einer in einer Datei gespeicherten SQL-Anweisung müssen Sie eine Dateiverbindung bereitstellen, die den Dateinamen und den Speicherort der Datei angibt. Weitere Informationen finden Sie unter [File Connection Manager](../integration-services/connection-manager/file-connection-manager.md).  
  
## SQL in Variablen  
 Wenn die Quelle der SQL-Anweisung im Task "SQL ausführen" eine Variable ist, geben Sie den Namen der Variablen an, die die Abfrage enthält. Die „Value“-Eigenschaft der Variablen enthält den Abfragetext. Sie legen die „ValueType“-Eigenschaft der Variablen auf einen Zeichenfolgendatentyp fest. Geben dann die SQL-Anweisung in die „Value“-Eigenschaft ein, oder kopieren Sie sie in die Eigenschaft. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md).  
  
  