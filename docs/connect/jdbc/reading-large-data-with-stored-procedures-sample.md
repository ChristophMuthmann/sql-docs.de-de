---
title: Zum Lesen umfangreicher Daten mit gespeicherten Prozeduren Beispiel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00387faec988fde6bdfa310ed96723f2bc226bfa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Beispiel zum Lesen umfangreicher Daten mit gespeicherten Prozeduren
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht, wie von einer gespeicherten Prozedur Abrufen eines großen OUT-Parameter.  
  
 Die Codedatei für dieses Beispiel heißt executeStoredProcedure.java und befindet sich unter folgendem Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\adaptive  
  
## <a name="requirements"></a>Anforderungen  
 Zum Ausführen dieser beispielanwendung benötigen Sie Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Außerdem müssen Sie die Datei sqljdbc.jar oder sqljdbc4.jar in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
 Sie müssen auch erstellen, die folgende gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank:  
  
```  
CREATE PROCEDURE GetLargeDataValue   
  (@Document_ID int,   
   @Document_ID_out int OUTPUT,   
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  
  
AS   
BEGIN    
   SELECT @Document_ID_out = DocumentID,   
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary   
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] Datenbank. Im Beispielcode werden anschließend Beispieldaten erstellt, und die Tabelle Production.Document wird mithilfe einer parametrisierten Abfrage aktualisiert. Anschließend ruft der Beispielcode den adaptiven Pufferung mithilfe der [GetResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse und führt die GetLargeDataValue-Prozedur. Beachten Sie, dass ab Version 2.0 des JDBC-Treibers die responseBuffering-Verbindungseigenschaft standardmäßig auf "adaptive" festgelegt ist.  
  
 Schließlich der Beispielcode zeigt die Daten, die mit der OUT-Parameter zurückgegeben, und auch veranschaulicht, wie die `mark` und `reset` Methoden auf der zu einem beliebigen Teil der Daten erneut zu lesende Stream.  
  
 [!code[JDBC#UsingAdaptiveBuffering2](../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit umfangreichen Daten](../../connect/jdbc/working-with-large-data.md)  
  
  
