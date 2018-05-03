---
title: Befehlsparameter | Microsoft Docs
description: Befehlsparameter
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f32f4adf2bc4d969154741edc447d942e7b62d37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="command-parameters"></a>Befehlsparameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Parameter werden im Befehlstext durch ein Fragezeichen markiert. Zum Beispiel wurde die folgende SQL-Anweisung für einen einzelnen Eingabeparameter markiert:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Zum Verbessern der Leistung durch Reduzierung des Netzwerkverkehrs der OLE DB-Treiber für SQL Server wird nicht automatisch Parameterinformationen, wenn **ICommandWithParameters:: GetParameterInfo** oder **ICommandPrepare:: Bereiten Sie vor** aufgerufen wird, bevor die Ausführung eines Befehls. Dies bedeutet, dass der OLE DB-Treiber für SQL Server nicht automatisch ausgeführt wird:  
  
-   Überprüfen Sie die Richtigkeit des angegebenen Datentyps **ICommandWithParameters:: SetParameterInfo**.  
  
-   Zuordnen des in den Accessor-Bindungsinformationen angegebenen DBTYPE zum korrekten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp für den Parameter  
  
 Bei Einsatz dieser beiden Methoden können in Anwendungen möglicherweise Fehler oder Genauigkeitsverluste auftreten, wenn Datentypen angegeben werden, die nicht mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp des Parameters kompatibel sind.  
  
 Um dies zu vermeiden, sollte die Anwendung Folgendes tun:  
  
-   Sicherstellen, dass *PwszDataSourceType* entspricht der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp für den Parameter auf, wenn eine feste Programmierung **ICommandWithParameters:: SetParameterInfo**.  
  
-   Sicherstellen, dass der DBTYPE–Wert, der an den Parameter gebunden wird, vom gleichen Typ wie der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp des Parameters ist, wenn ein Accessor fest codiert wird.  
  
-   Code aufrufen **ICommandWithParameters:: GetParameterInfo** , damit der Anbieter abrufen, kann die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen der Parameter dynamisch. Beachten Sie, dass dies einen zusätzlichen Netzwerkroundtrip zum Server bedingt.  
  
> [!NOTE]  
>  Der Anbieter unterstützt keine Aufrufen **ICommandWithParameters:: GetParameterInfo** für eine beliebige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Update- oder DELETE-Anweisung mit einer FROM-Klausel; für jede SQL-Anweisung von einer Unterabfrage mit Parametern; für SQL-Anweisungen, wie z. B. mit der parametermarkierungen in beiden Ausdrücken eines Vergleichs oder quantifizierten Prädikats enthalten; oder Abfragen, wobei einer der Parameter einen Parameter an eine Funktion ist. Bei der Verarbeitung von Batches von SQL-Anweisungen, der Anbieter auch unterstützt keine Aufrufen **ICommandWithParameters:: GetParameterInfo** für parametermarkierungen in Anweisungen nach der ersten Anweisung im Batch. Kommentare (/ * \*/) sind nicht zulässig, der [!INCLUDE[tsql](../../../includes/tsql-md.md)] Befehl.  
  
 Der OLE DB-Treiber für SQL Server unterstützt Eingabeparameter in SQL-Anweisungsbefehlen. In prozeduraufrufbefehlen unterstützt der OLE DB-Treiber für SQL Server Eingabe-, Ausgabe- und Eingabe/Ausgabe-Parameter. Ausgabeparameterwerte werden entweder nach der Ausführung (nur wenn keine Rowsets zurückgegeben werden) oder nach Abschluss der Rowsetverarbeitung durch die Anwendung an die Anwendung zurückgegeben. Um sicherzustellen, dass zurückgegebene Werte gültig sind, verwenden Sie **IMultipleResults** um Rowsets zu erzwingen.  
  
 Die Namen der Parameter von gespeicherten Prozeduren müssen nicht in einer DBPARAMBINDINFO-Struktur angegeben werden. Verwenden Sie NULL für den Wert der *PwszName* Member, um anzugeben, dass der OLE DB-Treiber für SQL Server den Parameternamen ignorieren und nur die im angegebenen Ordinalzahl verwenden soll die *RgParamOrdinals* Mitglied  **ICommandWithParameters:: SetParameterInfo**. Wenn der Befehlstext sowohl benannte als auch unbenannte Parameter enthält, dann müssen alle unbenannten Parameter vor den benannten Parametern angegeben werden.  
  
 Wenn Sie der Namen der Parameter einer gespeicherten Prozedur angegeben wird, überprüft der OLE DB-Treiber für SQL Server den Namen, um sicherzustellen, dass er gültig ist. Der OLE DB-Treiber für SQL Server zurück einen Fehler, wenn er vom Consumer einen fehlerhaften Parameternamen erhält.  
  
> [!NOTE]  
>  Unterstützung für die bereitzustellenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML- und benutzerdefinierte Typen (UDT), implementiert der OLE DB-Treiber für SQL Server ein neues [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) Schnittstelle.  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle](../../oledb/ole-db-commands/commands.md)  
  
  
