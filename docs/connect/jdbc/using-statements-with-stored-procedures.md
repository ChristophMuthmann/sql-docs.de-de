---
title: Using-Anweisungen mit gespeicherten Prozeduren | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eef81eed0bafd9ea342bc483de0130dcb60a81f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-statements-with-stored-procedures"></a>Verwenden von Anweisungen mit gespeicherten Prozeduren
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei einer gespeicherten Prozedur handelt es sich um eine Datenbankprozedur, ähnlich einer Prozedur in anderen Programmiersprachen, die in der eigentlichen Datenbank enthalten ist. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], gespeicherte Prozeduren können erstellt werden, mithilfe von [!INCLUDE[tsql](../../includes/tsql_md.md)], oder die common Language Runtime (CLR) und einer der Visual Studio mit Programmiersprachen wie Visual Basic oder c#. Im allgemeinen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherte Prozeduren können Folgendes tun:  
  
-   Annehmen von Eingabeparametern und Zurückgeben mehrerer Werte in Form von Ausgabeparametern an die aufrufende Prozedur oder den aufrufenden Batch.  
  
-   Aufnehmen von Programmierungsanweisungen, die Operationen in der Datenbank ausführen, einschließlich des Aufrufens anderer Prozeduren.  
  
-   Zurückgeben eines Statuswertes an eine aufrufende Prozedur oder einen aufrufenden Batch, der Erfolg oder Fehlschlagen (sowie die Ursache für das Fehlschlagen) anzeigt.  
  
> [!NOTE]  
>  Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherte Prozeduren finden Sie unter "Grundlegendes zu gespeicherten Prozeduren" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
 Arbeiten mit Daten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] her, indem Sie eine gespeicherte Prozedur die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), und [ SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klassen. Welche Klasse verwendet wird, hängt davon ab, ob von der gespeicherten Prozedur IN- (Eingabe) oder OUT-Parameter (Ausgabe) benötigt werden. Wenn die gespeicherte Prozedur keine in-erfordert oder OUT-Parameter, Sie die SQLServerStatement-Klasse können. Wenn die gespeicherte Prozedur mehrmals aufgerufen werden wird, oder nur IN-Parameter benötigt, können Sie die SQLServerPreparedStatement-Klasse. Wenn die gespeicherte Prozedur erfordert in- und OUT-Parameter, sollten Sie die SQLServerCallableStatement-Klasse verwenden. Es ist nur wenn die gespeicherte Prozedur OUT-Parameter erfordert, dass Sie den Aufwand für das Verwenden der SQLServerCallableStatement-Klasse benötigen.  
  
> [!NOTE]  
>  Gespeicherte Prozeduren können auch Updatezählungen und mehrere Resultsets zurückgeben. Weitere Informationen finden Sie unter [mithilfe einer gespeicherten Prozedur mit einer Updatezählung](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) und [mehrere Resultsets mithilfe von](../../connect/jdbc/using-multiple-result-sets.md).  
  
 Wenn Sie den JDBC-Treiber verwenden, um eine gespeicherte Prozedur mit Parametern aufzurufen, müssen Sie mithilfe der `call` SQL-Escapesequenz zusammen mit den [PrepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Die vollständige Syntax für die `call` -Escapesequenz lautet wie folgt:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Weitere Informationen zu den `call` und anderen SQL-Escapesequenzen, finden Sie unter [mithilfe von SQL-Escapesequenzen](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Die Themen in diesem Abschnitt beschreibt die Methoden, die Sie aufrufen können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherte Prozeduren mithilfe des JDBC-Treibers und der `call` SQL-Escapesequenz.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwenden von gespeicherten Prozeduren ohne Parameter](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|Beschreibt die Verwendung des JDBC-Treibers zum Ausführen von gespeicherten Prozeduren, die keine Eingabe- oder Ausgabeparameter enthalten.|  
|[Verwenden von gespeicherten Prozeduren mit Eingabeparametern](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|Beschreibt die Verwendung des JDBC-Treibers zum Ausführen von gespeicherten Prozeduren, die Eingabeparameter enthalten.|  
|[Verwenden von gespeicherten Prozeduren mit Ausgabeparametern](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|Beschreibt die Verwendung des JDBC-Treibers zum Ausführen von gespeicherten Prozeduren, die Ausgabeparameter enthalten.|  
|[Verwenden von gespeicherten Prozeduren mit einem Rückgabestatus](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|Beschreibt die Verwendung des JDBC-Treibers zum Ausführen von gespeicherten Prozeduren, die Rückgabestatuswerte enthalten.|  
|[Verwenden von gespeicherten Prozeduren mit einer Updatezählung](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|Beschreibt die Verwendung des JDBC-Treibers zum Ausführen von gespeicherten Prozeduren, die Updatezählungen enthalten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit dem JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
