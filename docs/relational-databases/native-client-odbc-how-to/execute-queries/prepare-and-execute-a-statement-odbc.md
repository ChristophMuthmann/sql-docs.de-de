---
title: "Vorbereiten und Ausführen eine Anweisung (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- statement execution
- statement preparation
ms.assetid: 0adecc63-4da5-486c-bc48-09a004a2fae6
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd945fdf098773bea47fa6a0f2d395e7841a0459
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="prepare-and-execute-a-statement-odbc"></a>Vorbereiten und Ausführen von Anweisungen (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-prepare-a-statement-once-and-then-execute-it-multiple-times"></a>So bereiten Sie eine Anweisung vor und führen sie dann mehrmals aus  
  
1.  Rufen Sie [SQLPrepare-Funktion](http://go.microsoft.com/fwlink/?LinkId=59360) , die Anweisung vorzubereiten.  
  
2.  Rufen Sie optional [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) bestimmt die Anzahl von Parametern in der vorbereiteten Anweisung.  
  
3.  Optional führen Sie für jeden Parameter in der vorbereiteten Anweisung Folgendes aus:  
  
    -   Rufen Sie [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) um Parameterinformationen abzurufen.  
  
    -   Jeder Parameter an eine Programmvariable zu binden, indem [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md). Richten Sie alle Data-at-Execution-Parameter ein.  
  
4.  Für jede Ausführung einer vorbereiteten Anweisung gilt:  
  
    -   Wenn die Anweisung über Parametermarkierungen verfügt, fügen Sie die Datenwerte in den gebundenen Parameterpuffer ein.  
  
    -   Rufen Sie [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) zum Ausführen der vorbereiteten Anweisung.  
  
    -   Wenn Data-at-Execution-Eingabeparameter verwendet werden, [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) wird SQL_NEED_DATA zurückgegeben. Senden Sie die Daten in Segmenten mit [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405) und [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md).  
  
### <a name="to-prepare-a-statement-with-column-wise-parameter-binding"></a>So bereiten Sie eine Anweisung mit spaltenweiser Parameterbindung vor  
  
1.  Rufen Sie [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) um die folgenden Attribute festzulegen:  
  
    -   Legen Sie SQL_ATTR_PARAMSET_SIZE auf die Anzahl von Sätzen (S) von Parametern fest.  
  
    -   Legen Sie SQL_ATTR_PARAM_BIND_TYPE auf SQL_PARAMETER_BIND_BY_COLUMN fest.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_PROCESSED_PTR-Attribut fest, um auf eine SQLUINTEGER-Variable zu zeigen und die Anzahl der verarbeiteten Parameter zu halten.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_STATUS_PTR-Attribut fest, sodass es auf ein Array mit S SQLUSSMALLINT-Variablen zeigt, welche die Parameterstatusindikatoren enthalten.  
  
2.  Rufen Sie SQLPrepare, um die Anweisung vorzubereiten.  
  
3.  Rufen Sie optional [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) bestimmt die Anzahl von Parametern in der vorbereiteten Anweisung.  
  
4.  Rufen Sie optional für jeden Parameter in der vorbereiteten Anweisung SQLDescribeParam auf, um Parameterinformationen abzurufen.  
  
5.  Führen Sie folgende Aktionen für jeden Parametermarker durch:  
  
    -   Weisen Sie ein Array mit S-Parameterpuffern zu, um Datenwerte zu speichern.  
  
    -   Weisen Sie ein Array mit S-Parameterpuffern zu, um Datenlängen zu speichern.  
  
    -   Rufen Sie SQLBindParameter, um die Parameter-die Wert und die datenlängenarrays an den Anweisungsparameter zu binden.  
  
    -   Falls der Parameter ein Data-at-Execution-Textparameter oder –Imageparameter ist, richten Sie ihn ein.  
  
    -   Wenn Data-at-Execution-Parameter verwendet werden, richten Sie sie ein.  
  
6.  Für jede Ausführung einer vorbereiteten Anweisung gilt:  
  
    -   Fügen Sie die S Datenwerte und S Datenlängen in die gebundenen Parameterarrays ein.  
  
    -   Rufen Sie SQLExecute auf, um die vorbereitete Anweisung auszuführen.  
  
    -   Wenn Data-at-Execution-Eingabeparameter verwendet werden, gibt SQLExecute SQL_NEED_DATA zurück. Mithilfe von SQLParamData und SQLPutData, senden Sie die Daten in Segmenten.  
  
### <a name="to-prepare-a-statement-with-row-wise-bound-parameters"></a>So bereiten Sie eine Anweisung mit zeilenweiser Parameterbindung vor  
  
1.  Ordnen Sie ein Array [S] von Strukturen zu, wobei S der Anzahl von Parametersätzen entspricht. Die Struktur verfügt über ein Element für jeden Parameter, und jedes Element verfügt über zwei Teile:  
  
    -   Der erste Teil ist eine Variable des entsprechenden Datentyps zum Speichern der Parameterdaten.  
  
    -   Der zweite Teil ist eine SQLINTEGER-Variable zum Speichern des Statusindikators.  
  
2.  Rufen Sie [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) um die folgenden Attribute festzulegen:  
  
    -   Legen Sie SQL_ATTR_PARAMSET_SIZE auf die Anzahl von Sätzen (S) von Parametern fest.  
  
    -   Legen Sie SQL_ATTR_PARAM_BIND_TYPE auf die Größe der in Schritt 1 zugeordneten Struktur fest.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_PROCESSED_PTR-Attribut fest, um auf eine SQLUINTEGER-Variable zu zeigen und die Anzahl der verarbeiteten Parameter zu halten.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_STATUS_PTR-Attribut fest, sodass es auf ein Array mit S SQLUSSMALLINT-Variablen zeigt, welche die Parameterstatusindikatoren enthalten.  
  
3.  Rufen Sie SQLPrepare, um die Anweisung vorzubereiten.  
  
4.  Rufen Sie für jeden Parametermarker SQLBindParameter, um die Parameter Daten Wert datenlängenzeiger zeigen Sie auf die Variablen im ersten Element des Arrays von Strukturen, die in Schritt 1 zugewiesen wurden. Falls der Parameter ein Data-at-Execution-Parameter ist, richten Sie ihn ein.  
  
5.  Für jede Ausführung einer vorbereiteten Anweisung gilt:  
  
    -   Füllen Sie das gebundene Parameterpufferarray mit Datenwerten.  
  
    -   Rufen Sie SQLExecute auf, um die vorbereitete Anweisung auszuführen. Der Treiber führt die SQL-Anweisung S Mal aus, einmal für jeden Parametersatz.  
  
    -   Wenn Data-at-Execution-Eingabeparameter verwendet werden, gibt SQLExecute SQL_NEED_DATA zurück. Mithilfe von SQLParamData und SQLPutData, senden Sie die Daten in Segmenten.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Abfragen Gewusst-wie-Themen zur Vorgehensweise &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
