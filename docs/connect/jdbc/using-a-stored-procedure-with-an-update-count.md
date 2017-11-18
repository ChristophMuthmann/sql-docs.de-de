---
title: "Mithilfe einer gespeicherten Prozedur mit einer Updatezählung | Microsoft Docs"
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
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb038eeb3b3b0f14ef0ace1076244bd64949ed81
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-an-update-count"></a>Verwenden von gespeicherten Prozeduren mit einer Updatezählung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zum Ändern von Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] her, indem Sie eine gespeicherte Prozedur die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse. Sie können mithilfe der SQLServerCallableStatement-Klasse aufrufen von gespeicherten Prozeduren, die Daten ändern, die in der Datenbank enthalten ist und die Anzahl der betroffenen Zeilen zurück, auch bezeichnet als die Anzahl der Updates.  
  
 Nachdem Sie den Aufruf der gespeicherten Prozedur mit der SQLServerCallableStatement-Klasse eingerichtet haben, können Sie klicken Sie dann die gespeicherte Prozedur aufrufen, indem Sie entweder die [ausführen](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) oder [ExecuteUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) Methode. Die ExecuteUpdate-Methode zurückgegeben wird ein **Int** Wert, der die Anzahl der von der gespeicherten Prozedur, aber die Execute-Methode betroffenen Zeilen nicht der Fall. Wenn Sie die Execute-Methode verwenden und die Anzahl der betroffenen Zeilen abgerufen werden soll, können Sie rufen die [GetUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) -Methode auf, nachdem Sie die gespeicherte Prozedur auszuführen.  
  
> [!NOTE]  
>  Wenn der JDBC-Treiber alle Updatezählungen zurückgeben soll, einschließlich der Updatezählungen, die von eventuell ausgelösten Triggern zurückgegeben werden, müssen Sie die lastUpdateCount-Verbindungseigenschaft auf "false" setzen. Weitere Informationen zur LastUpdateCount-Eigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Erstellen Sie beispielsweise die folgende Tabelle und die gespeicherte Prozedur, und fügen Sie Beispieldaten in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank:  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
  
CREATE PROCEDURE UpdateTestTable  
   @Col2 varchar(50),  
   @Col3 int  
AS  
BEGIN  
   UPDATE TestTable  
   SET Col2 = @Col2, Col3 = @Col3  
END;  
INSERT INTO dbo.TestTable (Col2, Col3) VALUES ('b', 10);  
```  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, die Execute-Methode wird verwendet, um die gespeicherte Prozedur UpdateTestTable aufgerufen und die GetUpdateCount-Methode wird dann verwendet, um die Anzahl der Zeilen zurück, die sind von der gespeicherten Prozedur betroffen.  
  
 [!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

