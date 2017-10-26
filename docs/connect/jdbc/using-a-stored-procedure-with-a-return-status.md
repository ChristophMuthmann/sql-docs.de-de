---
title: "Verwenden eine gespeicherte Prozedur mit einem Rückgabestatus | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8247f7f81e70aafac8d109abe7f8303c8e13f487
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-a-return-status"></a>Verwenden von gespeicherten Prozeduren mit einem Rückgabestatus
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherter Prozedur, die Sie aufrufen können, ist eine, die einen Status oder ein Ergebnisparameter zurückgibt. Damit wird normalerweise ermittelt, ob die gespeicherte Prozedur erfolgreich ausgeführt wurde oder fehlgeschlagen ist. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Klasse, die Sie verwenden können, um diese Art von gespeicherter Prozedur aufrufen und die zurückgegebenen Daten verarbeiten.  
  
 Wenn Sie diese Art von gespeicherter Prozedur aufrufen, mit dem JDBC-Treiber, müssen Sie die `call` SQL-Escapesequenz zusammen mit den [PrepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse . Die Syntax für die `call` -Escapesequenz mit einem rückgabestatusparameter lautet wie folgt:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Weitere Informationen zu den SQL-Escapesequenzen finden Sie unter [mithilfe von SQL-Escapesequenzen](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Bei der Erstellung der `call` Escapesequenz, geben Sie die rückgabestatusparameter mithilfe der? (?) an. das als Platzhalter für den Parameterwert fungiert, der von der gespeicherten Prozedur zurückgegeben wird. Um einen Wert für einen rückgabestatusparameter anzugeben, müssen Sie den Datentyp des Parameters angeben, mit der [RegisterOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) Methode der SQLServerCallableStatement-Klasse, vor dem Ausführen der gespeicherten Prozedur.  
  
> [!NOTE]  
>  Wird JDBC Driver mit einer SQL Server-Datenbank verwendet, werden der Wert an dem von Ihnen für den rückgabestatusparameter in der RegisterOutParameter-Methode immer eine ganze Zahl, die Sie mit dem Datentyp java.sql.Types.INTEGER angeben können.  
  
 Wenn Sie einen Wert an der RegisterOutParameter-Methode für einen rückgabestatusparameter übergeben, müssen Sie nicht nur den Datentyp für den Parameter, sondern auch ordinale Position des Parameters, im Aufruf gespeicherten Prozedur zu verwendende angeben. Für den Rückgabestatusparameter ist die ordinale Position immer 1, da es sich immer um den ersten Parameter im Aufruf der gespeicherten Prozedur handelt. Wird zwar von die SQLServerCallableStatement-Klasse Unterstützung für die Verwendung der Name des Parameters an, dass diesem Parameter bereitgestellt wird, können Sie für rückgabestatusparameter nur einen Parameter ordnungspositionsnummer verwenden.  
  
 Erstellen Sie beispielsweise die folgende gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank:  
  
```  
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```  
  
 Diese gespeicherte Prozedur gibt abhängig davon, ob der im cityName-Parameter angegebene Ort in der Person.Address-Tabelle gefunden wurde, den Statuswert 1 oder 0 zurück.  
  
 Im folgenden Beispiel wird eine offene Verbindung zur der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben und die [ausführen](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) Methode wird verwendet, um die Prozedur "checkcontactcity" mit gespeicherten aufrufen:  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

