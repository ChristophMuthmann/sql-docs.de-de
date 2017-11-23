---
title: OPENROWSET (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OPENROWSET
dev_langs: DMX
helpviewer_keywords: OPENROWSET statement
ms.assetid: 8c8b61b4-2bf6-46c7-8976-51484004dc22
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a95fc508806d4653228caf5a72bac0109646a5f8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;quelldatenabfrage&gt; -OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
