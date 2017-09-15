---
title: Andere Treiber Architekturen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a458ba0d7e83ab4e4c56ed40c34fae54e24c1b2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="other-driver-architectures"></a>Andere Treiber-Architekturen
Einige ODBC-Treiber übereinstimmen nicht streng auf die zuvor beschriebenen Architektur. Dies kann daran liegen die Treiber Aufgaben außer denen eines herkömmlichen ODBC-Treibers, oder sind keine Treiber in den normalen Sinn.  
  
## <a name="driver-as-a-middle-component"></a>Treiber als mittlere-Komponente  
 Der ODBC-Treiber kann zwischen der Treiber-Manager und eine oder mehrere andere ODBC-Treiber befinden. Wenn der Treiber in der Mitte mit mehreren Datenquellen funktionsfähig ist, fungiert er als Verteiler von ODBC-Aufrufe (oder entsprechend übersetzte aufrufen) auf andere Module, die tatsächlich die Datenquellen zugreifen. In dieser Architektur dauert der Treiber in der Mitte auf einigen der Rolle des Treiber-Managers.  
  
 Ein weiteres Beispiel für diese Art des Treibers ist ein Programm Spy++ für ODBC, der abfängt und kopiert ODBC-Funktionen, die zwischen der Treiber-Manager und der Treiber gesendet werden. Diese Ebene kann verwendet werden, um einen Treiber oder eine Anwendung zu emulieren. Auf den Treiber-Manager wird die Ebene der Treiber ist angezeigt. an den Treiber scheint die Ebene der Treiber-Manager sein.  
  
## <a name="heterogeneous-join-engines"></a>Heterogene Join-Datenbankmodulen enthält  
 Ein Abfragemodul zum Ausführen von heterogenen Joins sind einige ODBC-Treiber basiert. In einer Architektur eines heterogenen joinmoduls (siehe die folgende Abbildung), der Treiber wird die Anwendung als ein Treiber jedoch zu einem anderen Instanz des Treiber-Managers als Anwendung angezeigt wird. Dieser Treiber verarbeitet einen heterogene Join aus der Anwendung durch Aufrufen von separaten SQL-Anweisungen im Treiber für jedes verknüpfte Datenbank.  
  
 ![Architektur eines heterogenen joinmoduls](../../odbc/reference/media/fig3-4.gif "fig3 4")  
  
 Diese Architektur bietet eine allgemeine Schnittstelle für die Anwendung auf Daten aus verschiedenen Datenbanken zugreifen. Kann eine allgemeine Möglichkeit zum Abrufen von Metadaten, z. B. Informationen zu speziellen Spalten (Zeilen-IDs), und verwenden allgemeine Katalogfunktionen zum Abrufen von Daten Wörterbuchinformationen aufrufen. Durch Aufrufen der ODBC-Funktion **SQLStatistics**, z. B. kann die Anwendung Informationen zu den Indizes für die Tabellen verknüpft werden, abrufen, selbst wenn die Tabellen auf zwei unterschiedlichen Datenbanken sind. Der Abfrageprozessor ist keine Gedanken machen, wie die Datenbanken Metadaten speichern.  
  
 Die Anwendung bietet außerdem Zugriff auf die standard-Datentypen. ODBC definiert allgemeine SQL-Datentypen, denen DBMS-spezifische Datentypen zugeordnet werden. Eine Anwendung kann Aufrufen **SQLGetTypeInfo** zum Abrufen von Informationen zu Datentypen in anderen Datenbanken.  
  
 Wenn die Anwendung eine heterogene Join-Anweisung generiert, wird der Abfrageprozessor in dieser Architektur analysiert die SQL-Anweisung, und generiert dann separate SQL-Anweisungen für jede Datenbank verknüpft werden sollen. Mithilfe von Metadaten zu jedem Treiber kann der Abfrageprozessor den Join am effizientesten, intelligenten bestimmen. Z. B. wenn die Anweisung in einer Datenbank mit einer Tabelle auf eine andere Datenbank zwei Tabellen verknüpft werden, kann der Abfrageprozessor Verknüpfen der beiden Tabellen in einer Datenbank vor dem Eintritt in des Ergebnis mit der Tabelle aus der anderen Datenbank.  
  
## <a name="odbc-on-the-server"></a>ODBC auf dem Server  
 ODBC-Treiber können auf einem Server installiert werden, sodass sie von Anwendungen auf einer Reihe von Clientcomputern verwendet werden können. In dieser Architektur (siehe die folgende Abbildung), einen Treiber-Manager und einen einzelnen ODBC-Treiber auf jedem Client installiert sind, und ein anderer Treiber-Manager und eine Reihe von ODBC-Treiber auf dem Server installiert sind. Dadurch wird jeder Client beim Zugriff auf eine Vielzahl von Treibern verwendet und auf dem Server beibehalten.  
  
 ![Architektur der ODBC-Treiber auf einem Server](../../odbc/reference/media/fig3-5.gif "FIG3 5")  
  
 Ein Vorteil dieser Architektur ist effizient Software-Wartung und Konfiguration. Treiber müssen nur an einer Stelle aktualisiert werden: auf dem Server. Mithilfe von System-Datenquellen können Datenquellen auf dem Server für die Verwendung von allen Clients definiert werden. Die Datenquellen müssen nicht auf dem Client definiert werden. Verbindungspooling kann verwendet werden, zur Optimierung dieses Prozesses mit dem Clients eine Verbindung mit Datenquellen herstellen.  
  
 Der Treiber auf dem Client ist in der Regel eine sehr kleine Treiber, bei dem den Treiber-Manager-Aufruf an den Server übertragen. Seine Platzbedarf kann erheblich kleiner als die voll funktionsfähige ODBC-Treiber auf dem Server sein. In dieser Architektur können Clientressourcen freigegeben werden, wenn der Server mehr rechenleistung verfügt. Darüber hinaus können der Effizienz und Sicherheit des gesamten Systems verbessert werden, vom backup-Server installieren und Ausführen des Lastenausgleichs, um die Verwendung durch Posteingangsserver zu optimieren.
