---
title: OPENROWSET (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET
dev_langs:
- DMX
helpviewer_keywords:
- OPENROWSET statement
ms.assetid: 8c8b61b4-2bf6-46c7-8976-51484004dc22
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 914e1be70255414373fd758301ef0682f3aba6e7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;quelldatenabfrage&gt; -OPENROWSET
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ersetzt die Quelldatenabfrage durch eine Abfrage an einen externen Anbieter. Die Anweisungen INSERT, SELECT FROM PREDICTION JOIN und SELECT FROM NATURAL PREDICTION JOIN unterstützen **OPENROWSET**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>Argumente  
 *provider_name*  
 Der Name eines OLE DB-Anbieters.  
  
 *provider_string*  
 Die OLE DB-Verbindungszeichenfolge für den angegebenen Anbieter.  
  
 *query_syntax*  
 Eine Abfragesyntax, die ein Rowset zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die Datamining-Anbieter Herstellen einer Verbindung mit dem Datenquellenobjekt mit *Provider_name* und *Provider_string,* und führt die Abfrage, die im angegebenen *Query_syntax* um das Rowset aus den Quelldaten abzurufen.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel kann in einer PREDICTION JOIN-Anweisung verwendet werden, um Daten mit einer [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]-SELECT-Anweisung aus der [!INCLUDE[tsql](../includes/tsql-md.md)]-Datenbank abzurufen.  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [&#60; quelldatenabfrage &#62;](../dmx/source-data-query.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

