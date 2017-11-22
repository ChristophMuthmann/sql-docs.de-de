---
title: Execute-Methode (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b42de5e1548cc7fd68c7b71182034df7e9f97f3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="execute-method-rds"></a>Execute-Methode (RDS)
Führt die Anforderung aus und erstellt ein ADO-Recordset für die Verwendung in ADO, 2.5 und höher.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>Parameter  
 *"ConnectionString"*  
 Eine Zeichenfolge verwendet, um mit dem OLE DB-Anbieter hergestellt, in dem die Anforderung für die Ausführung gesendet werden. Wenn ein Ereignishandler mithilfe des Parameters *HandlerString* es bearbeiten oder die Verbindungszeichenfolge ersetzen kann.  
  
 *HandlerString*  
 Eine zweiteilige-Zeichenfolge, die identifiziert den Handler, die mit dieser Ausführung verwendet werden. Die Zeichenfolge besteht aus zwei Teilen. Der erste Teil enthält den Namen (ProgID) des Handlers verwendet werden. Der zweite Teil enthält Argumente, die an den Ereignishandler übergeben werden. Die Details der Interpretation der Argumentzeichenfolge sind spezifisch für jeden Handler. Die beiden Teile werden durch die erste Instanz eines Kommas in der Zeichenfolge getrennt. Die Argumentzeichenfolge kann zusätzliche Kommas enthalten. Die Argumente sind optional.  
  
 *Abfragezeichenfolge*  
 Ein Befehl in der Befehlssprache unterstützt die OLE DB-Anbieter, die in der Verbindungszeichenfolge angegeben wird. Für SQL-basierte Anbieter *QueryString* möglicherweise eine Transact-SQL Command-Anweisung enthalten, jedoch für nicht-SQL-Anbieter (z. B. MSDataShape) dies u. u. keine [!INCLUDE[tsql](../../../includes/tsql_md.md)] abfrageanweisung.  
  
 Wenn ein Ereignishandler verwendet wird, kann der Handler ändern oder Ersetzen Sie den hier angegebenen Wert. Der Ereignishandler beispielsweise in der Regel ersetzt *QueryString* mit einer Abfragezeichenfolge aus der INI-Datei. Standardmäßig wird die Datei "Msdfmap.ini" verwendet.  
  
 *lFetchOptions*  
 Gibt den Typ des asynchronen abrufen.  
  
 Weitere Informationen finden Sie unter [FetchOptions-Eigenschaft (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md).  
  
 *TableID*  
 Ein **Variant** des Typs VT_EMPTY oder "VT_BSTR". Wenn dieser Wert des Typs VT_EMPTY ist, wird es ignoriert. Ist vom Typ "VT_BSTR", wird das Recordset mithilfe erstellt **AdCmdTableDirect** und dem hier angegebenen Wert und die *QueryString* Parameter wird ignoriert.  
  
 *lExecuteOptions*  
 Eine Bitmaske von Ausführungsoptionen:  
  
 1 =*ReadOnly* Öffnen des Recordsets mit **AdLockReadOnly**.  
  
 2 =*NoBatch* Öffnen des Recordsets mit **AdLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* der Aufrufer gewährleistet ist, dass Parameterinformationen für alle Parameter, in angegeben wird *pParameters*.  
  
 8 =*GetInfo* Parameterinformationen für die Abfrage wird vom OLE DB-Anbieter abgerufen und zurückgegeben, die der *pParameters* Parameter. Die Abfrage wird nicht ausgeführt, und kein Recordset wird zurückgegeben.  
  
 16 =*GetHiddenColumns* Öffnen des Recordsets mit **AdLockBatchOptimistic** und ausgeblendeten Spalten werden in das Recordset enthalten sein.  
  
 *ReadOnly*, *NoBatch* und *GetHiddenColumns* sind sich gegenseitig ausschließende Optionen; es nicht erzeugt jedoch einen Fehler, um mehr als einer davon festgelegt. Wenn mehrere Optionen festgelegt werden, *GetHiddenColumns* hat Vorrang vor allen anderen, gefolgt von *ReadOnly*. Wenn keine Optionen, wird standardmäßig angegeben sind Öffnen des Recordsets mit **AdLockBatchOptimistic** und ausgeblendete Spalten nicht in das Recordset enthalten sind.  
  
 *pParameters*  
 Ein **Variant** , ein sicheres Array von Parameterdefinitionen enthält. Wenn die *GetInfo* Option wurde im angegebenen *lExecuteOptions*, dieser Parameter wird verwendet, um die vom OLE DB-Anbieter abgerufen Parameterdefinitionen zurückgeben. Andernfalls kann dieser Parameter leer sein.  
  
 *lcid*  
 Die LCID verwendet, um Fehler zu erstellen, die zurückgegeben werden *pInformation*.  
  
 *pInformation*  
 Ein Zeiger auf Informationsfehler zurückgegebenes ausführen. Wenn der Wert NULL ist, wird keine Fehlerinformationen zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 Die *HandlerString* Parameter kann null sein. Was in diesem Fall geschieht, hängt davon ab, wie die RDS-Server konfiguriert ist. Eine Zeichenfolge Handler "MSDFMAP.handler" gibt an, dass der Microsoft bereitgestellter Handler (Msdfmap.dll) verwendet werden soll. Eine Zeichenfolge Handler "MASDFMAP.handler,sample.ini" gibt an, dass der Msdfmap.dll-Handler verwendet werden soll, und dass das Argument "sample.ini" an den Ereignishandler übergeben werden sollen. MSDFMAP.dll interpretiert das Argument als eine Richtung, in der sample.ini verwenden, um die Verbindung und den Abfragezeichenfolgen zu überprüfen.  
  
## <a name="applies-to"></a>Gilt für  
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


