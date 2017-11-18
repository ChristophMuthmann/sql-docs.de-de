---
title: Verwenden von gespeicherten Prozeduren mit Eingabeparametern | Microsoft Docs
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
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49f92bf52ddf9c06906f42b81945ec3d630c8be4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-input-parameters"></a>Verwenden von gespeicherten Prozeduren mit Eingabeparametern
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherter Prozedur, die Sie aufrufen können, ist eine, die einen enthält oder mehr Parameter, sind die Parameter, die verwendet werden können, um Daten an die gespeicherte Prozedur übergeben. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -Klasse, die Sie verwenden können, um diese Art von gespeicherter Prozedur aufrufen und die zurückgegebenen Daten verarbeiten.  
  
 Wenn Sie den JDBC-Treiber zum Aufrufen einer gespeicherten Prozedur mit IN-Parameter verwenden, müssen Sie mithilfe der `call` SQL-Escapesequenz zusammen mit den [PrepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Die Syntax für die `call` -Escapesequenz mit IN-Parameter lautet wie folgt:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Weitere Informationen zu den SQL-Escapesequenzen finden Sie unter [mithilfe von SQL-Escapesequenzen](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Bei der Erstellung der `call` Escapesequenz, die IN-Parameter angeben, indem die? (?) an. das als Platzhalter für die Parameterwerte fungiert, die an die gespeicherte Prozedur übergeben werden. Um einen Wert für einen Parameter angeben, können Sie eine der Methoden Setter-Methode der SQLServerPreparedStatement-Klasse. Die verwendbare Festlegungsmethode hängt vom Datentyp des IN-Parameters ab.  
  
 Wenn Sie einen Wert an die Festlegungsmethode übergeben, müssen Sie nicht nur den Wert angeben, der im Parameter verwendet wird, sondern auch die ordinale Position des Parameters in der gespeicherten Prozedur. Wenn die gespeicherte Prozedur beispielsweise einen einzigen IN-Parameter enthält, ist der Ordinalwert "1". Wenn die gespeicherte Prozedur zwei Parameter enthält, ist der erste Ordinalwert "1" und der zweite Ordinalwert "2".  
  
 Verwenden Sie als Beispiel dafür, wie eine gespeicherte Prozedur aufrufen, die IN-Parameter enthält, die UspGetEmployeeManagers gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Diese gespeicherte Prozedur übernimmt einen einzelnen Eingabeparameter mit dem Namen "EmployeeID" (integer-Wert) und gibt abhängig von der angegebenen "EmployeeID" eine rekursive Liste der Mitarbeiter und deren Vorgesetzten zurück. Der Java-Code für den Aufruf dieser gespeicherten Prozedur sieht folgendermaßen aus:  
  
```  
public static void executeSprocInParams(Connection con) {  
   try {  
      PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}");  
      pstmt.setInt(1, 50);  
      ResultSet rs = pstmt.executeQuery();  
  
      while (rs.next()) {  
         System.out.println("EMPLOYEE:");  
         System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
         System.out.println("MANAGER:");  
         System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
         System.out.println();  
      }  
      rs.close();  
      pstmt.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

