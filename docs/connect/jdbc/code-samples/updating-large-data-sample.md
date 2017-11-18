---
title: "Aktualisieren von großen Datenbeispiel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8df6738cb6913261bebfd5ea469a483328c6678b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updating-large-data-sample"></a>Beispiel zum Aktualisieren umfangreicher Daten
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht, wie eine umfangreiche Spalte in einer Datenbank aktualisiert.  
  
 Die Codedatei für dieses Beispiel heißt "updateLargeData.java" und befindet sich unter folgendem Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\adaptive  
  
## <a name="requirements"></a>Anforderungen  
 Zum Ausführen dieser beispielanwendung benötigen Sie Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Außerdem müssen Sie die Datei "sqljdbc4.jar" in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für "sqljdbc4.jar" vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar", "sqljdbc4.jar", "sqljdbc41.jar" oder "sqljdbc42.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Dieses Beispiel verwendet die [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) und [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) Methoden, die in der JDBC 4.0-API zum Zugriff auf die treiberspezifischen antwortpuffermethoden vorgestellt werden. Zum Kompilieren und Ausführen dieses Beispiels benötigen Sie die "sqljdbc4.jar"-Klassenbibliothek, die die Unterstützung für JDBC 4.0 bereitstellt. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] Datenbank. Klicken Sie dann der Beispielcode ein Statement-Objekt erstellt und verwendet die [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) -Methode überprüft, ob das Statement-Objekt ein Wrapper für die angegebene ist [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) Methode wird verwendet, um Zugriff auf die treiberspezifischen antwortpuffermethoden.  
  
 Als Nächstes setzt der Beispielcode den antwortpuffermodus als "**adaptive**" mithilfe der [SetResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse sowie veranschaulicht, wie Modus für die adaptive Pufferung abgerufen.  
  
 Anschließend führt die SQL-Anweisung, und fügt die Daten werden in ein aktualisierbares [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
 Schließlich werden die Datenzeilen durchlaufen, die im Resultset enthalten sind. Wenn sie eine leere dokumentzusammenfassung, verwendet es die Kombination von [UpdateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) und [UpdateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) Methoden, um die Zeile der Daten zu aktualisieren und erneut in der Datenbank gespeichert. Wenn bereits Daten vorhanden sind, verwendet der [GetString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) Methode, um einige der Daten anzuzeigen, die es enthält.  
  
 Das Standardverhalten des Treibers ist "**adaptive.**" Für das aktualisierbare Resultset mit Vorwärtscursor und wenn die Daten im Resultset größer als der Arbeitsspeicher für die Anwendung ist, die Anwendung muss jedoch die adaptiven Pufferung Modus explizit festlegen, indem die [SetResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) die Methode von der [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse.  
  
 [!code[JDBC#UsingAdaptiveBuffering3](../../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit umfangreichen Daten](../../../connect/jdbc/working-with-large-data.md)  
  
  

