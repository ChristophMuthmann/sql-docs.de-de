---
title: Verwenden eine gespeicherte Prozedur ohne Parameter | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4600b2cd527fdb6261ca700a19bf2e5c004bc31c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Verwenden von gespeicherten Prozeduren ohne Parameter
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die einfachste Art des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherter Prozedur, die Sie aufrufen können, ist ein Deskriptor, enthält keine Parameter und gibt ein einzelnes Resultset zurück. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Klasse, die Sie verwenden können, um diese Art von gespeicherter Prozedur aufrufen und die zurückgegebenen Daten verarbeiten.  
  
 Wenn Sie den JDBC-Treiber verwenden, um eine gespeicherte Prozedur ohne Parameter aufrufen, müssen Sie mithilfe der `call` SQL-Escapesequenz. Die Syntax für die `call` Escapesequenz ohne Parameter lautet wie folgt:  
  
 `{call procedure-name}`  
  
> [!NOTE]  
>  Weitere Informationen zu den SQL-Escapesequenzen finden Sie unter [mithilfe von SQL-Escapesequenzen](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Erstellen Sie beispielsweise die folgende gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank:  
  
```  
CREATE PROCEDURE GetContactFormalNames   
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName   
   FROM Person.Contact  
END  
```  
  
 Diese gespeicherte Prozedur gibt ein einzelnes Resultset zurück, das eine Datenspalte enthält, bei der es sich um eine Kombination aus Titel, Vorname und Nachname der ersten zehn Kontakte in der Tabelle "Person.Contact" handelt.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben und die [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) Methode wird verwendet, um die Prozedur "getcontactformalnames" mit gespeicherten aufrufen.  
  
```  
public static void executeSprocNoParams(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
  
      while (rs.next()) {  
         System.out.println(rs.getString("FormalName"));  
      }  
      rs.close();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
