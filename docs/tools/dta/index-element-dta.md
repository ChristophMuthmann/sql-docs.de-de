---
title: Index-Element (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca17a222eb07926c89283ce1cc2f47f9412af59d
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="index-element-dta"></a>Index-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Enthält Informationen über einen Index, den für eine benutzerspezifische Konfiguration erstellt oder gelöscht werden sollen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>Elementattribute  
  
|Indexattribut|Datentyp|Description|  
|---------------------|---------------|-----------------|  
|**Gruppiert**|**boolean**|Optional. Gibt einen gruppierten Index an. Auf "true" oder "false" festgelegt, z. B.:<br /><br /> `<Index Clustered="true">`<br /><br /> Standardmäßig ist dieses Attribut auf "false" festgelegt.|  
|**Eindeutig**|**boolean**|Optional. Gibt einen eindeutigen Index an. Auf "true" oder "false" festgelegt, z. B.:<br /><br /> `<Index Unique="true">`<br /><br /> Standardmäßig ist dieses Attribut auf "false" festgelegt.|  
|**Online**|**boolean**|Optional. Gibt einen Index an, der Vorgänge ausführen kann, wenn der Server online ist. Dadurch ist temporärer Speicherplatz erforderlich. Auf "true" oder "false" festgelegt, z. B.:<br /><br /> `<Index Online="true">`<br /><br /> Standardmäßig ist dieses Attribut auf "false" festgelegt.<br /><br /> Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).|  
|**IndexSizeInMB**|**double**|Optional. Gibt die maximale Indexgröße in Megabyte an, z. B.:<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> Keine Standardeinstellung.|  
|**NumberOfRows**|**integer**|Optional. Simuliert unterschiedliche Indexgrößen zur effektiven Simulation unterschiedlicher Tabellengrößen, z. B.:<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> Keine Standardeinstellung.|  
|**QUOTED_IDENTIFIER**|**boolean**|Optional. Bewirkt, dass [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die ISO-Regeln für das Setzen von Anführungszeichen als Trennzeichen bei Bezeichnern und Literalzeichenfolgen befolgt. Dieses Attribut muss aktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt. So wird dieses Attribut beispielsweise durch die folgende Syntax aktiviert:<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).|  
|**ARITHABORT**|**boolean**|Optional. Bewirkt die Beendigung einer Abfrage, wenn beim Ausführen der Abfrage ein Überlauffehler oder ein Fehler aufgrund einer Division durch 0 auftritt. Dieses Attribut muss aktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt. So wird dieses Attribut beispielsweise durch die folgende Syntax aktiviert:<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).|  
|**CONCAT_NULL_YIELDS_**<br /><br /> **NULL**|**boolean**|Optional. Steuert die Behandlung von Verkettungsergebnissen als NULL-Werte oder als leere Zeichenfolgenwerte. Dieses Attribut muss aktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt. So wird dieses Attribut beispielsweise durch die folgende Syntax aktiviert:<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).|  
|**ANSI_NULLS**|**boolean**|Optional. Gibt an, dass sich die Vergleichsoperatoren "gleich" (=) und "ungleich" (<>) bei Verwendung mit NULL-Werten ISO-konform verhalten müssen. Dieses Attribut muss aktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt. So wird dieses Attribut beispielsweise durch die folgende Syntax aktiviert:<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).|  
|**ANSI_PADDING**|**boolean**|Optional. Steuert das Speichern von Werten in der Spalte, wenn die Werte kürzer als die definierte Spaltengröße sind. Dieses Attribut muss aktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt. So wird dieses Attribut beispielsweise durch die folgende Syntax aktiviert:<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).|  
|**ANSI_WARNINGS**|**boolean**|Optional. Gibt das ISO-Standardverhalten für verschiedene Fehlerbedingungen an. Dieses Attribut muss aktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt. So wird dieses Attribut beispielsweise durch die folgende Syntax aktiviert:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md).|  
|**NUMERIC_ROUNDABORT**|**boolean**|Optional. Gibt an, welche Fehlerberichtsstufe generiert wird, wenn beim Runden in einem Ausdruck Genauigkeitsverluste entstehen. Dieses Attribut muss deaktiviert sein, wenn der Index für eine berechnete Spalte oder eine Sicht gilt.<br /><br /> Dieses Attribut wird durch die folgende Syntax aktiviert:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Standardmäßig ist dieses Attribut deaktiviert.<br /><br /> Weitere Informationen finden Sie unter [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md).|  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmalig erforderlich pro **Create** - oder **Drop** -Element, wenn keine andere physische Entwurfsstruktur anhand des **Statistics** - oder **Heap** -Elements angegeben ist.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Create-Element &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** -Element. Weitere Informationen finden Sie im XML-Schema des Datenbankoptimierungsratgebers.|  
|**Untergeordnete Elemente**|[Name-Element für Index &#40; DTA &#41;](../../tools/dta/name-element-for-index-dta.md)<br /><br /> [Column-Element für Index &#40; DTA &#41;](../../tools/dta/column-element-for-index-dta.md)<br /><br /> **PartitionScheme** -Element. Weitere Informationen finden Sie im XML-Schema des Datenbankoptimierungsratgebers.<br /><br /> **PartitionColumn** -Element. Weitere Informationen finden Sie im XML-Schema des Datenbankoptimierungsratgebers.<br /><br /> [Filegroup-Element für Index &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)<br /><br /> **NumberOfReferences** -Element. Weitere Informationen finden Sie im XML-Schema des Datenbankoptimierungsratgebers.<br /><br /> **PercentUsage** -Element. Weitere Informationen finden Sie im XML-Schema des Datenbankoptimierungsratgebers.|  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
