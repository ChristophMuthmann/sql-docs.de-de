---
title: Verwenden von gespeicherten Prozeduren mit Ausgabeparametern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e5c3b945652c04cbbe75563d853703b5676b43f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-output-parameters"></a>Verwenden von gespeicherten Prozeduren mit Ausgabeparametern
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherter Prozedur, die Sie aufrufen können, ist die Rückgabe eines oder mehrere OUT-Parameter, Parameter, die die gespeicherte Prozedur verwendet wird, zum Zurückgeben von Daten an die aufrufende Anwendung zurück. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Klasse, die Sie verwenden können, um diese Art von gespeicherter Prozedur aufrufen und die zurückgegebenen Daten verarbeiten.  
  
 Wenn Sie diese Art von gespeicherter Prozedur aufrufen, mit dem JDBC-Treiber, müssen Sie mithilfe der `call` SQL-Escapesequenz zusammen mit den [PrepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Die Syntax für die `call` -Escapesequenz mit OUT-Parameter lautet wie folgt:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Weitere Informationen zu den SQL-Escapesequenzen finden Sie unter [mithilfe von SQL-Escapesequenzen](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Bei der Erstellung der `call` Escapesequenz, die OUT-Parameter angeben, indem die? (?) an. das als Platzhalter für die Parameterwerte fungiert, die von der gespeicherten Prozedur zurückgegeben werden. Um einen Wert für einen OUT-Parameter angeben, müssen Sie den Datentyp jedes Parameters angeben, mit der [RegisterOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) -Methode der SQLServerCallableStatement-Klasse, vor dem Ausführen der gespeicherten Prozedur.  
  
 Der Wert, den Sie angeben, für der OUT-Parameter in der RegisterOutParameter-Methode muss einem der JDBC-Datentypen enthalten, die in "java.SQL.Types", der wiederum einen systemeigenen zugeordnet sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentypen. Weitere Informationen zu JDBC und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentypen finden Sie unter [Grundlegendes zu den Datentypen des JDBC-Treiber](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
 Wenn Sie einen Wert an der RegisterOutParameter-Methode für einen OUT-Parameter übergeben, müssen Sie nicht nur den Datentyp für den Parameter, aber auch ordinale Position des Parameters oder der Name des Parameters in der gespeicherten Prozedur zu verwendende angeben. Wenn die gespeicherte Prozedur beispielsweise einen einzigen OUT-Parameter enthält, ist der Ordinalwert 1. Wenn die gespeicherte Prozedur zwei Parameter enthält, ist der erste Ordinalwert 1 und der zweite Ordinalwert 2.  
  
> [!NOTE]  
>  Der JDBC-Treiber unterstützt nicht die Verwendung der CURSOR, SQLVARIANT, Tabellen- und Zeitstempel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen als AUSGABEPARAMETER.  
  
 Erstellen Sie beispielsweise die folgende gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank:  
  
```  
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID   
   FROM HumanResources.Employee   
   WHERE EmployeeID = @employeeID  
END  
```  
  
 Diese gespeicherte Prozedur gibt abhängig vom angegebenen IN-Parameter "employeeID" (ein integer-Wert) einen einzigen OUT-Parameter "managerID" zurück (ebenfalls ein integer-Wert). Bei dem im OUT-Parameter zurückgegebenen Wert handelt es sich um die auf "EmployeeID" basierende "ManagerID", die in der Tabelle "HumanResources.Employee" enthalten ist.  
  
 Im folgenden Beispiel wird eine offene Verbindung zur der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben und die [ausführen](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) Methode wird verwendet, um die Prozedur "getimmediatemanager" mit gespeicherten aufrufen:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt(1, 5);  
      cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt(2));  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
 In diesem Beispiel werden die Ordnungspositionen verwendet, um die Parameter zu identifizieren. Alternativ können Sie einen Parameter mit seinem Namen anstelle der Ordnungsposition identifizieren. Im folgenden Codebeispiel wird das vorhergehende Beispiel geändert, um die Verwendung von benannten Parametern in einer Java-Anwendung zu veranschaulichen. Beachten Sie, dass die Parameternamen den Parameternamen in der Definition der gespeicherten Prozedur entsprechen:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt("employeeID", 5);  
      cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
      cstmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
```  
  
 }  
  
> [!NOTE]  
>  Diese Beispiele verwenden die Execute-Methode der SQLServerCallableStatement-Klasse, die gespeicherte Prozedur auszuführen. da von der gespeicherten Prozedur nicht auch ein Resultset zurückgegeben wurde. Wenn dem so wäre, die [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) Methode verwendet werden würde.  
  
 Gespeicherte Prozeduren können Updatezählungen und mehrere Resultsets zurückgeben. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] folgt der JDBC 3.0-Spezifikation, der zufolge mehrere Resultsets und updatezählungen abgerufen werden soll, bevor die OUT-Parameter abgerufen werden. Die Anwendung sollte also Abrufen aller der ResultSet-Objekte und updatezählungen vor dem Abrufen der OUT-Parameter mit den Methoden CallableStatement.getter. Andernfalls verloren die ResultSet-Objekte und updatezählungen, die noch nicht abgerufenen, wenn die OUT-Parameter abgerufen werden. Weitere Informationen zu updatezählungen und mehrere Resultsets finden Sie unter [mithilfe einer gespeicherten Prozedur mit einer Anzahl aktualisieren](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) und [mehrere Resultsets mithilfe von](../../connect/jdbc/using-multiple-result-sets.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
