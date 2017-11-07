---
title: DMSCHEMA_MINING_MODEL_CONTENT-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_CONTENT
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7d48b47cc0ded0541380a4a9997b1cab13bd21a0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingmodelcontent-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT-Rowset
  Ermöglicht es der Clientanwendung, den Inhalt eines Data Mining-Modells zu durchsuchen. Clientanwendungen können spezielle Strukturvorgangseinschränkungen verwenden, die am Ende dieses Themas erläutert werden, um zum Inhalt des Miningmodells zu navigieren.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **DMSCHEMA_MINING_MODEL_CONTENT** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||Der Katalogname. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] füllt diese Spalte mit dem Namen der Datenbank, von denen das Modell ein Element ist.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||Der nicht gekennzeichnete Schemaname. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **VT_NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**||Der Name des Modells, dem der von dieser Zeile beschriebene Inhalt zugeordnet ist.|  
|**ATTRIBUTNAME**|**DBTYPE_WSTR**||Die Namen der Attribute, die diesem Knoten entsprechen.|  
|**KNOTENNAME**|**DBTYPE_WSTR**||Der Name des Knotens. Derzeit enthält diese Spalte den gleichen Wert wie **NODE_UNIQUE_NAME**, obwohl dies in zukünftigen Versionen ändern kann.|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**||Der eindeutige Name des Knotens.|  
|**NODE_TYPE**|**DBTYPE_I4**||Der Typ des Knotens. Erzeugt einen der folgenden Werte (diese Liste kann durch Data Mining-Algorithmen von Drittanbietern erweitert werden):<br /><br /> **DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT** (**2**)<br /><br /> **DM_NODE_TYPE_TREE_INTERIOR** (**3**)<br /><br /> **DM_NODE_TYPE_TREE_DISTRIBUTION** (**4**)<br /><br /> **DM_NODE_TYPE_CLUSTER** (**5**)<br /><br /> **DM_NODE_TYPE_UNKNOWN** (**6**)<br /><br /> **DM_NODE_TYPE_ITEMSET** (**7**)<br /><br /> **DM_NODE_TYPE_ASSOCIATION_RULE** (**8**)<br /><br /> **DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE** (**9**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE** (**10**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE** (**11**)<br /><br /> **DM_NODE_TYPE_SEQUENCE** (**13**)<br /><br /> **DM_NODE_TYPE_TRANSITION** (**14**)<br /><br /> **DM_NODE_TYPE_TIME_SERIES** (**15**)<br /><br /> **DM_NODE_TYPE_TS_TREE** (**16**)<br /><br /> **DM_NODE_TYPE_NN_SUBNETWORK** (**17**) neuronale Netzwerke, Subnetzwerke<br /><br /> **DM_NODE_TYPE_NN_INPUT_LAYER** (**18**) neuronale Netzwerke, eingabeebenen (übergeordnete Elemente der Eingabeknoten)<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_LAYER** (**19**) neuronale Netzwerke, verborgene Ebenen (übergeordnete Elemente von verborgenen Knoten)<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_LAYER** (**20**) neuronale Netzwerke, Ausgabeebenen (übergeordnete Elemente der Ausgabeknoten)<br /><br /> **DM_NODE_TYPE_NN_INPUT_NODE** (**21**) neuronale Netzwerke, Eingabeknoten<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_NODE** (**22**) neuronale Netzwerke, verborgene Knoten<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_NODE** (**23**) neuronale Netzwerke, Ausgabeknoten<br /><br /> **DM_NODE_TYPE_NN_MARGINAL_STAT_NODE** (**24**) neuronale Netzwerke, randstatistik<br /><br /> **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (**25**)<br /><br /> **DM_NODE_TYPE_NB_MARGINAL_STAT_NODE** (**26**) neuronale Netzwerke, randstatistik|  
|**NODE_GUID**|**DBTYPE_GUID**||Der GUID (Globally Unique Identifier) des Knotens. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**NODE_CAPTION**|**DBTYPE_WSTR**||Eine Bezeichnung oder Beschriftung, die dem Knoten zugeordnet ist. Diese Eigenschaft dient hauptsächlich zu Anzeigezwecken.|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||Eine Schätzung der Anzahl untergeordneter Elemente des Knotens.|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||Der eindeutige Name des dem Knoten übergeordneten Elements. **NULL** wird für alle Knoten auf der Stammebene zurückgegeben.|  
|**NODE_DESCRIPTION**|**DBTYPE_WSTR**||Eine benutzerfreundliche Beschreibung des Knotens.|  
|**NODE_RULE**|**DBTYPE_WSTR**||Eine XML-Beschreibung der Regel, die in den Knoten eingebettet ist.|  
|**MARGINAL_RULE**|**DBTYPE_WSTR**||Eine XML-Beschreibung der Regel, die vom übergeordneten Knoten zum Knoten verschoben wird.|  
|**NODE_PROBABILITY**|**DBTYPE_R8**||Die diesem Knoten zugeordnete Wahrscheinlichkeit.|  
|**MARGINAL_PROBABILITY**|**DBTYPE_R8**||Die Wahrscheinlichkeit für das Erreichen des Knotens vom übergeordneten Knoten aus.|  
|**NODE_DISTRIBUTION**|**DBTYPE_HCHAPTER**||Eine Tabelle, die das Wahrscheinlichkeitshistogramm des Knotens enthält.|  
|**NODE_SUPPORT**|**DBTYPE_R8**||Die Anzahl der Fälle, die diesen Knoten unterstützen.|  
|**MSOLAP_MODEL_COLUMN**|**DBTYPE_WSTR**||Der Name der Spalte aus der Modelldefinition, zu der dieser Knoten gehört.|  
|**MSOLAP_NODE_SCORE**|**DBTYPE_R8**||Das Ergebnis, das für diesen Knoten berechnet wurde.|  
|**MSOLAP_NODE_SHORT_CAPTION**|**DBTYPE_WSTR**||Eine Kurzbeschriftung für den Knoten, die zu Anzeigezwecken für eine bessere Lesbarkeit verwendet werden kann.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **DMSCHEMA_MINING_MODEL_CONTENT** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Optional.|  
|**ATTRIBUTNAME**|**DBTYPE_WSTR**|Optional.|  
|**KNOTENNAME**|**DBTYPE_WSTR**|Optional.|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**NODE_TYPE**|**DBTYPE_I4**|Optional.|  
|**NODE_GUID**|**DBTYPE_WSTR**|Optional.|  
|**NODE_CAPTION**|**DBTYPE_WSTR**|Optional.|  
|**TREE_OPERATION**|**DBTYPE_UI4**|Optional. Weitere Anmerkungen finden Sie unten.|  
  
 Die Einschränkung **TREE_OPERATION**, befindet sich nicht auf eine bestimmte Spalte des der **DMSCHEMA_MINING_MODEL_CONTENT** Rowsets, sondern gibt einen strukturoperator. Der Consumer festlegbaren eine **NODE_UNIQUE_NAME** Einschränkung und den strukturoperator (**VORGÄNGER**, **Kinder**, **gleichgeordnete Elemente**,  **ÜBERGEORDNETE**, **Nachfolger**, **SELF**) auf die angeforderte Menge von Elementen abzurufen. Die **SELF** -Operator fügt die Zeile für den Knoten selbst in der Liste der zurückgegebenen Zeilen. Die folgende Tabelle beschreibt die Konstanten, aus denen die bitmapdefinition für die **TREE_OPERATION** Einschränkung. Kombiniert werden mit dem logischen **oder** Operator.  
  
|Konstante|Wert|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|**0 x 00000020**|  
|**DMTREEOP_CHILDREN**|**0 x 00000001**|  
|**DMTREEOP_SIBLINGS**|**0 x 00000002**|  
|**DMTREEOP_PARENT**|**0 x 00000004**|  
|**DMTREEOP_SELF**|**0 x 00000008**|  
|**DMTREEOP_DESCENDANTS**|**0 x 00000010**|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Schemarowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

