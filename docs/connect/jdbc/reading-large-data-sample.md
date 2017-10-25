---
title: "Lesen große Datenbeispiel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4341d85ceced60ed2d108eb4e9f95251e6fdd33d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="reading-large-data-sample"></a>Beispiel zum Lesen umfangreicher Daten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht, wie zum Abrufen eines großen einspalten-Werts aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe der [GetCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) Methode.  
  
 Die Codedatei für dieses Beispiel heißt readLargeData.java und befindet sich unter folgendem Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\adaptive  
  
## <a name="requirements"></a>Anforderungen  
 Zum Ausführen dieser beispielanwendung benötigen Sie Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Außerdem müssen Sie die Datei sqljdbc.jar oder sqljdbc4.jar in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] Datenbank. Im Beispielcode werden anschließend Beispieldaten erstellt, und die Tabelle Production.Document wird mithilfe einer parametrisierten Abfrage aktualisiert.  
  
 Darüber hinaus wird der Beispielcode zum Abrufen der adaptiven Pufferung Modus mithilfe der [GetResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Beachten Sie, dass ab Version 2.0 des JDBC-Treibers die responseBuffering-Verbindungseigenschaft standardmäßig auf "adaptive" festgelegt ist.  
  
 Anschließend mithilfe einer SQL-Anweisung mit der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt, der Beispielcode führt die SQL-Anweisung und fügt die Daten werden in einem [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
 Schließlich der Code durchläuft die Datenzeilen im Resultset enthalten sind, und verwendet die [GetCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) Methode, um einige der Daten zugreifen, die es enthält.  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit umfangreichen Daten](../../connect/jdbc/working-with-large-data.md)  
  
  

