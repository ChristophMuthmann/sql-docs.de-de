---
title: Synchronize-Methode (RDS) | Microsoft Docs
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d223df00d0b32c3f608bcd61207de23da77e15cf
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="synchronize-method-rds"></a>Synchronize-Methode (RDS)
Synchronisieren Sie das angegebene Recordset, mit der Datenbank, die durch die Verbindungszeichenfolge für die Verwendung in ADO 2.5 und höher angegeben.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Parameter  
 *ConnectionString*  
 Eine Zeichenfolge verwendet, um mit dem OLE DB-Anbieter hergestellt, in dem die Anforderung gesendet werden. Wenn ein Ereignishandler verwendet wird, kann der Ereignishandler bearbeiten oder Ersetzen Sie die Verbindungszeichenfolge.  
  
 *HandlerString*  
 Die Zeichenfolge identifiziert den Handler, die mit dieser Ausführung verwendet werden. Die Zeichenfolge besteht aus zwei Teilen. Der erste Teil enthält den Namen (ProgID) des Handlers verwendet werden. Der zweite Teil der Zeichenfolge enthält Argumente, die an den Ereignishandler übergeben werden. Wie die Argumentzeichenfolge interpretiert wird, ist bestimmten Handler. Die beiden Teile werden durch die erste Instanz eines Kommas in der Zeichenfolge getrennt, (obwohl die Argumentzeichenfolge zusätzliche Kommas enthalten kann). Die Argumente sind optional.  
  
 *lSynchronizeOptions*  
 Eine Bitmaske der Synchronisierungsoptionen.  
  
 1 =*UpdateTransact* Aktualisierungen der Datenbank in einer Transaktion zusammengefasst werden. Die Transaktion wird abgebrochen, wenn eines der Updates ein Fehler auftritt.  
  
 2 =*RefreshWithUpdate* Ursachen Zeile Status zurückgegeben werden, wenn weder *aktualisieren* noch *RefreshConflicts* festgelegt ist.  
  
 4 =*aktualisieren* das Recordset mit aktuellen Daten aus der Datenbank aktualisiert wird. Ausstehende Updates werden nicht auf die Datenbank übertragen. Wenn dieses Bit nicht festgelegt ist, das Recordset wird nicht aktualisiert, und alle ausstehenden Updates auf die Datenbank verschoben werden.  
  
 8 =*RefreshConflicts* keine Zeilen mit ausstehenden Änderungen zu aktualisieren. Die Fehler beim Aktualisieren der Zeilen werden mit aktuellen Daten aus der Datenbank aktualisiert.  
  
 *ppRecordset*  
 Ein Zeiger auf das Recordset synchronisiert werden.  
  
 *pStatusArray*  
 Synchronisieren Sie eine Variante ein sicheren Arrays der Status der Zeile für die betroffenen Zeilen zurückgegeben. Nicht festgelegt, wenn keines der folgenden Synchronisierungsoptionen festgelegt werden: *RefreshWithUpdate*, *aktualisieren* und *RefreshConflicts*.  
  
 *lcid*  
 Die LCID verwendet, um Fehler zu erstellen, die zurückgegeben werden *pInformation*.  
  
 *pInformation*  
 Ein Zeiger auf Informationsfehler zurückgegebenes **Execute**. Wenn der Wert NULL ist, wird keine Fehlerinformationen zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 Die *HandlerString* Parameter kann null sein. Was in diesem Fall geschieht, hängt davon ab, wie die RDS-Server konfiguriert ist. Eine Zeichenfolge Handler "MSDFMAP.handler" gibt an, dass der Microsoft bereitgestellter Handler (Msdfmap.dll) verwendet werden soll. Eine Zeichenfolge Handler "MASDFMAP.handler,sample.ini" gibt an, dass der Msdfmap.dll-Handler verwendet werden soll, und dass das Argument "sample.ini" an den Ereignishandler übergeben werden sollen. Msdfmap.dll interpretiert klicken Sie dann das Argument als eine Richtung, in der sample.ini verwenden, um die Verbindung und den Abfragezeichenfolgen zu überprüfen.  
  
## <a name="applies-to"></a>Gilt für  
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


