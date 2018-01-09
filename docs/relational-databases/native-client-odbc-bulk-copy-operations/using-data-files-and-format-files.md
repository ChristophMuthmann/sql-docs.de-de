---
title: Verwenden von Datendateien und Formatdateien | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5a880a6a344e08e586316b985683dbf2edf87de
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-data-files-and-format-files"></a>Verwenden von Datendateien und Formatdateien
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Das einfachste Massenkopierprogramm geht wie folgt vor:  
  
1.  Aufrufe [Bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) an Massenkopieren (Set BCP_OUT) aus einer Tabelle oder Sicht in eine Datendatei.  
  
2.  Aufrufe [Bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) um den Massenkopiervorgang auszuführen.  
  
 Die Datendatei wird im einheitlichen Modus erstellt. Daher werden Daten aus allen Spalten in der Tabelle oder Sicht in der Datendatei im gleichen Format wie in der Datenbank gespeichert. Die Datei kann dann mit derselben Vorgehensweise auf einen Server massenkopiert werden, mit der Ausnahme, dass DB_IN statt DB_OUT festgelegt wird. Dies funktioniert jedoch nur, wenn sowohl die Quell- als auch die Zieltabellen genau dieselbe Struktur aufweisen. Die resultierende Datendatei kann auch eingegeben werden, um die **Bcp** Utility mithilfe der  **/n**  Switch (einheitlicher Modus).  
  
 So führen Sie einen Massenkopiervorgang des Resultsets einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aus, anstatt direkt aus einer Tabelle oder Sicht zu kopieren:  
  
1.  Rufen Sie **Bcp_init** zum Massenkopieren anzugeben, aber geben Sie NULL für den Tabellennamen.  
  
2.  Rufen Sie [Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) mit *eOption* auf BCPHINTS festgelegt und *iValue* in einen Zeiger auf eine SQLTCHAR-Zeichenfolge, die mit Transact-SQL-Anweisung festgelegt.  
  
3.  Rufen Sie **Bcp_exec** um den Massenkopiervorgang auszuführen.  
  
 Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung kann jede Anweisung sein, die ein Resultset generiert. Die Datendatei wird mit dem ersten Resultset der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung erstellt. Beim Massenkopieren wird jedes Resultset nach dem ersten ignoriert, wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung mehrere Resultsets generiert.  
  
 Rufen Sie zum Erstellen einer Datendatei in der die Daten in einem anderen Format als in der Tabelle gespeichert ist [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) aufrufen, um anzugeben, wie viele Spalten geändert werden soll, klicken Sie dann [Bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) für jede Spalte, deren Format Sie möchten ändern. Dies erfolgt nach dem Aufruf **Bcp_init** aber vor dem Aufrufen **Bcp_exec**. **Bcp_colfmt** gibt das Format, in dem Daten in der Spalte in der Datendatei gespeichert ist. Es kann beim ein- oder ausgehenden Massenkopieren verwendet werden. Sie können auch **Bcp_colfmt** auf der Zeilen- und Spaltenabschlusszeichen festzulegen. Angenommen, wenn Ihre Daten keine Tabulatorzeichen enthalten, können Sie erstellen eine durch Tabstopps getrennte Datei mit **Bcp_colfmt** das Tabulatorzeichen als Abschlusszeichen für jede Spalte festgelegt.  
  
 Beim Massenkopieren und Verwenden von **Bcp_colfmt**, Sie können problemlos erstellen eine Formatdatei beschreiben die Datendatei, die Sie, durch den Aufruf erstellt haben [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) nach dem letzten Aufruf von **Bcp_colfmt**.  
  
 Beim Massenkopieren aus einer Datendatei, die von einer Formatdatei beschrieben wird, lesen Sie die Formatdatei durch Aufrufen von [Bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) nach **Bcp_init** aber vor **Bcp_exec**.  
  
 Die **Bcp_control** -Funktion steuert verschiedene Optionen beim Massenkopieren in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus einer Datendatei. **Bcp_control** Legt Optionen fest, wie z. B. die maximale Anzahl von Fehlern vor dem Beenden, wird die Zeile in der Datei auf dem das Massenkopieren, die Zeile auf Beenden und die Batchgröße zu beginnen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausführen von Massenkopiervorgängen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
