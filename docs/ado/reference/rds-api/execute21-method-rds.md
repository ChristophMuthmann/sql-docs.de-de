---
title: Execute21-Methode (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1136e547d464f511aff92f4a6805da0262c7ed35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="execute21-method-rds"></a>Execute21-Methode (RDS)
Führt die Anforderung aus und erstellt ein ADO-Recordset für die Verwendung in ADO 2.1.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>Parameter  
 *ConnectionString*  
 Eine Zeichenfolge verwendet, um mit dem OLE DB-Anbieter hergestellt, in dem die Anforderung für die Ausführung gesendet werden. Wenn ein Ereignishandler mithilfe des Parameters *HandlerString*, es bearbeiten oder die Verbindungszeichenfolge ersetzen kann.  
  
 *HandlerString*  
 Die Zeichenfolge identifiziert den Handler, die mit dieser Ausführung verwendet werden. Die Zeichenfolge besteht aus zwei Teilen. Der erste Teil enthält den Namen (ProgID) des Handlers verwendet werden. Der zweite Teil der Zeichenfolge enthält Argumente, die an den Ereignishandler übergeben werden. Wie die Argumentzeichenfolge interpretiert wird, ist bestimmten Handler. Die beiden Teile werden durch die erste Instanz eines Kommas in der Zeichenfolge getrennt, (obwohl die Argumentzeichenfolge zusätzliche Kommas enthalten kann). Die Argumente sind optional.  
  
 *QueryString*  
 Ein Befehl in der Befehlssprache unterstützt die OLE DB-Anbieter, die in der Verbindungszeichenfolge angegeben wird. Für SQL-basierte Anbieter, er enthält möglicherweise eine [!INCLUDE[tsql](../../../includes/tsql_md.md)] Befehls-Anweisung, jedoch für nicht-SQL-Anbieter (z. B. MSDataShape) dies u. u. keine [!INCLUDE[tsql](../../../includes/tsql_md.md)] abfrageanweisung.  
  
 Wenn ein Ereignishandler verwendet wird (und es wird dringend empfohlen, dass ein Handler verwendet werden), kann der Handler auch, ändern oder Ersetzen Sie den Wert, der hier angegebenen. Der Ereignishandler beispielsweise in der Regel ersetzt *QueryString* mit einer Abfragezeichenfolge aus der INI-Datei. Standardmäßig wird die Datei "Msdfmap.ini" verwendet.  
  
 *lMarshalOptions*  
 Dient zum Festlegen von der Marshallen-Optionen für das Rowset/Recordset zurückgegeben wird.  
  
 *TableID*  
 Geben Sie eine Variante des VT_EMPTY oder "VT_BSTR". Wenn dieser Wert des Typs VT_EMPTY ist, wird es ignoriert. Ist vom Typ "VT_BSTR", wird das Recordset mithilfe erstellt **AdCmdTableDirect** mit den hier angegebenen Wert und die *QueryString* Parameter wird ignoriert.  
  
 *lExecuteOptions*  
 Eine Bitmaske von Ausführungsoptionen:  
  
 1 =*ReadOnly* Öffnen des Recordsets mit **AdLockReadOnly**.  
  
 2 =*NoBatch* Öffnen des Recordsets mit **AdLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* der Aufrufer gewährleistet ist, dass Parameterinformationen für alle Parameter, in angegeben wird *pParameters*.  
  
 8 =*GetInfo* Parameterinformationen für die Abfrage wird vom OLE DB-Anbieter abgerufen und zurückgegeben, die der *pParameters* Parameter. Die Abfrage wird nicht ausgeführt, und kein Recordset wird zurückgegeben.  
  
 16 = GetHiddenColumns Öffnen des Recordsets mit **AdLockBatchOptimistic** und ausgeblendeten Spalten werden in das Recordset enthalten sein.  
  
 Obwohl *ReadOnly*, *NoBatch* und *GetHiddenColumns* sind sich gegenseitig ausschließende Optionen, es ist kein Fehler mehr als einer davon festgelegt. Wenn mehrere Optionen festgelegt werden, *GetHiddenColumns* hat Vorrang vor allen anderen Optionen, gefolgt von *ReadOnly*. Wenn keine Optionen, wird standardmäßig angegeben sind Öffnen des Recordsets mit **AdLockBatchOptimistic** ausgeblendete Spalten nicht im Recordset enthalten sind.  
  
 *pParameters*  
 Eine Variante, die ein sicheres Array von Parameterdefinitionen enthält. Wenn die *GetInfo* Option wurde im angegebenen *lExecuteOptions*, dieser Parameter wird verwendet, um die vom OLE DB-Anbieter abgerufen Parameterdefinitionen zurückgeben. Andernfalls kann dieser Parameter leer sein.  
  
## <a name="remarks"></a>Hinweise  
 Die *HandlerString* Parameter kann null sein. Was in diesem Fall geschieht, hängt davon ab, wie die RDS-Server konfiguriert ist. Eine Zeichenfolge Handler "MSDFMAP.handler" gibt an, dass der Microsoft bereitgestellter Handler (Msdfmap.dll) verwendet werden soll. Eine Zeichenfolge Handler "MASDFMAP.handler,sample.ini" gibt an, dass der Msdfmap.dll-Handler verwendet werden soll, und dass das Argument "sample.ini" an den Ereignishandler übergeben werden sollen. MSDFMAP.dll interpretiert das Argument als eine Richtung, in der sample.ini verwenden, um die Verbindung und den Abfragezeichenfolgen zu überprüfen.  
  
> [!NOTE]
>  Die **Execute21** Methode ist eine Version von den [Execute-Methode (RDS)](../../../ado/reference/rds-api/execute-method-rds.md). Sie verwenden, müssen die **Execute** Methode für die Kommunikation mit ADO 2.1, die **Execute21** Methode kann stattdessen aufgerufen werden. Die Funktionen des die **Execute** Methode in ADO 2.5 und höher stellen eine Obermenge der Funktionen für die gleiche Methode in ADO 2.1.  
  
## <a name="applies-to"></a>Gilt für  
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


