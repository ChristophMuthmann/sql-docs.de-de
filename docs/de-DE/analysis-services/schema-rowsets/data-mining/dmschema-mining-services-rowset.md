---
title: DMSCHEMA_MINING_SERVICES-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_SERVICES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICES rowset
ms.assetid: 4a672f2f-d637-4def-a572-c18556f83d34
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71c95b5f3f1f2f8475659bf75c3f146e1cfdcdb0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dmschemaminingservices-rowset"></a>DMSCHEMA_MINING_SERVICES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Stellt eine Beschreibung jedes Data Mining-Algorithmus bereit, den der Anbieter unterstützt.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **DMSCHEMA_MINING_SERVICES** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**DIENSTNAME**|**DBTYPE_WSTR**|Name des Algorithmus Diese Spalte ist anbieterspezifisch.|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|Diese Spalte enthält eine Bitmap, die den Miningdienst beschreibt. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] füllt diese Spalte mit einem der folgenden Werte an:<br /><br /> **DM_SERVICETYPE_CLASSIFICATION** (**1**)<br /><br /> **DM_SERVICETYPE_CLUSTERING** (**2**)|  
|**SERVICE_DISPLAY_NAME**|**DBTYPE_WSTR**|Ein lokalisierbarer Anzeigename für den Algorithmus.|  
|**SERVICE_GUID**|**DBTYPE_GUID**|Der GUID für den Algorithmus.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine benutzerfreundliche Beschreibung des Algorithmus.|  
|**PREDICTION_LIMIT**|**DBTYPE_UI4**|Die maximale Anzahl der Vorhersagen, die von dem Modell und dem Algorithmus bereitgestellt werden können.|  
|**SUPPORTED_MODELING_FLAGS**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Flags, die die statistischen Verteilungen beschreibt, die vom Algorithmus unterstützt werden. Diese Spalte enthält mindestens einen der folgenden Werte:<br /><br /> "**NORMAL**"<br /><br /> "**LOG-NORMAL**"<br /><br /> "**UNIFORM**"|  
|**SUPPORTED_INPUT_CONTENT_TYPES**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Flags, die die Eingabeinhaltstypen beschreibt, die vom Algorithmus unterstützt werden. Diese Spalte enthält mindestens einen der folgenden Werte:<br /><br /> "**SCHLÜSSEL**"<br /><br /> "**DISKRETE**"<br /><br /> "**FORTLAUFEND**"<br /><br /> "**DISCRETIZED**"<br /><br /> "**ORDERED**"<br /><br /> "SCHLÜSSEL **SEQUENZ**"<br /><br /> "**ZYKLISCH**"<br /><br /> "**WAHRSCHEINLICHKEIT**"<br /><br /> "**VARIANZ**"<br /><br /> "**STDEV**"<br /><br /> "**UNTERSTÜTZUNG**"<br /><br /> "**WAHRSCHEINLICHKEITSVARIANZ**"<br /><br /> "**WAHRSCHEINLICHKEIT STDEV**"<br /><br /> "**SCHLÜSSELZEIT**"|  
|**SUPPORTED_PREDICTION_CONTENT_TYPES**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Flags, die die Vorhersageinhaltstypen beschreibt, die vom Algorithmus unterstützt werden. Diese Spalte enthält mindestens einen der folgenden Werte:<br /><br /> "**SCHLÜSSEL**"<br /><br /> "**DISKRETE**"<br /><br /> "**FORTLAUFEND**"<br /><br /> "**DISCRETIZED**"<br /><br /> "**ORDERED**"<br /><br /> "SCHLÜSSEL **SEQUENZ** "<br /><br /> "**ZYKLISCH**"<br /><br /> "**WAHRSCHEINLICHKEIT**"<br /><br /> "**VARIANZ**"<br /><br /> "**STDEV**"<br /><br /> "**UNTERSTÜTZUNG**"<br /><br /> "**WAHRSCHEINLICHKEITSVARIANZ**"<br /><br /> "**WAHRSCHEINLICHKEIT STDEV**"<br /><br /> "KEY TIME"|  
|**SUPPORTED_MODELING_FLAGS**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste der Modellierungsflags, die vom Algorithmus unterstützt werden. Diese Spalte enthält mindestens einen der folgenden Werte:<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**REGRESSOR**"<br /><br /> <br /><br /> Beachten Sie, dass auch anbieterspezifische Flags definiert werden können.|  
|**SUPPORTED_SOURCE_QUERY**|**DBTYPE_WSTR**|Diese Spalte wird aus Gründen der Abwärtskompatibilität unterstützt.|  
|**TRAINING_COMPLEXITY**|**DBTYPE_I4**|Die Zeitpanne, die das Training voraussichtlich dauern wird:<br /><br /> **DM_TRAINING_COMPLEXITY_LOW** gibt an, dass die Ausführungszeit relativ kurz und proportional zur Eingabe.<br /><br /> **DM_TRAINING_COMPLEXITY_MEDIUM** gibt an, dass die Ausführungszeit länger sein kann, aber es im Allgemeinen proportional zur Eingabe ist.<br /><br /> **DM_TRAINING_COMPLEXITY_HIGH** gibt an, dass die Ausführungszeit lang ist und es möglicherweise in Beziehung zu der Anzahl der Trainingsfälle exponentiell.|  
|**PREDICTION_COMPLEXITY**|**DBTYPE_I4**|Die Zeitpanne, die die Vorhersage voraussichtlich dauern wird:<br /><br /> **DM_PREDICTION_COMPLEXITY_LOW** gibt an, dass die Ausführungszeit relativ kurz und proportional zur Eingabe.<br /><br /> **DM_PREDICTION_COMPLEXITY_MEDIUM** gibt an, dass die Ausführungszeit länger sein kann, aber es im Allgemeinen proportional zur Eingabe ist.<br /><br /> **DM_PREDICTION_COMPLEXITY_HIGH** gibt an, dass die Ausführungszeit lang ist und es möglicherweise in Beziehung zu der Anzahl der Trainingsfälle exponentiell.|  
|**EXPECTED_QUALITY**|**DBTYPE_I4**|Die erwartete Qualität des mit diesem Algorithmus erstellten Modells:<br /><br /> **DM_EXPECTED_QUALITY_LOW**<br /><br /> **DM_EXPECTED_QUALITY_MEDIUM**<br /><br /> **DM_EXPECTED_QUALITY_HIGH**|  
|**SKALIERUNG**|**DBTYPE_I4**|Die Skalierbarkeit des Algorithmus:<br /><br /> **DM_SCALING_LOW**<br /><br /> **DM_SCALING_MEDIUM**<br /><br /> **DM_SCALING_HIGH**|  
|**ALLOW_INCREMENTAL_INSERT**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob der Algorithmus inkrementelles Training unterstützt, d. h. das Aktualisieren der erkannten Muster auf der Grundlage der neuen tatsächlichen Daten, anstatt die Muster vollständig neu zu erkennen.|  
|**ALLOW_PMML_INITIALIZATION**|**DBTYPE_BOOL**|Ein boolescher Wert, der anzeigt, ob Miningmodelle auf der Grundlage einer PMML 2.1-Zeichenfolge erstellt werden können.<br /><br /> Wenn **"true"**, unterstützt der Algorithmus die Initialisierung von PMML 2.1-Inhalten.|  
|**STEUERELEMENT**|**DBTYPE_I4**|Die vom Dienst bereitgestellte Unterstützung, wenn das Training unterbrochen wird:<br /><br /> **DM_CONTROL_NONE** gibt an, dass der Algorithmus nicht abgebrochen werden kann, nach dem Start zum Trainieren des Modells.<br /><br /> **DM_CONTROL_CANCEL** gibt an, dass der Algorithmus abgebrochen werden kann, nachdem es zum Trainieren des Modells beginnt, jedoch neu gestartet werden, muss um das Training fortzusetzen.<br /><br /> **DM_CONTROL_SUSPENDRESUME** gibt an, dass der Algorithmus abgebrochen und jederzeit fortgesetzt werden kann, aber auf die Ergebnisse nicht verfügbar, sind bis das Training abgeschlossen ist.<br /><br /> **DM_CONTROL_SUSPENDWITHRESULT** gibt an, dass der Algorithmus abgebrochen und jederzeit fortgesetzt werden kann, und alle inkrementellen Ergebnisse abgerufen werden können.|  
|**ALLOW_DUPLICATE_KEY**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob Fälle doppelte Schlüssel enthalten können.<br /><br /> Wenn **VARIANT_TRUE**, Fälle doppelte Schlüssel enthalten.|  
|**VIEWER_TYPE**|**DBTYPE_WSTR**|Der empfohlene Viewer für dieses Modell.|  
|**HELP_FILE**|**DBTYPE_WSTR**|(Optional) Der Name der Datei, die die Dokumentation für diesen Dienst enthält.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|(Optional) Die Hilfekontext-ID für diesen Dienst.|  
|**MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL**|**DBTYPE_WSTR**|Die unterstützte DDL-Version. 0 gibt an, dass DDL nicht unterstützt wird.|  
|**MSOLAP_SUPPORTS_OLAP_MINING_MODELS**|**DBTYPE_BOOL**|Ein boolescher Wert, der anzeigt, ob OLAP-Miningmodelle erstellt werden können.<br /><br /> Wenn **"true"**, OLAP-Miningmodelle erstellt werden können. Erfordert **MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL** ungleich NULL sein.|  
|**MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS**|**DBTYPE_BOOL**|Ein boolescher Wert, der anzeigt, ob Data Mining-Dimensionen erstellt werden können.<br /><br /> Wenn **"true"**, Datamining-Dimensionen erstellt werden können.|  
|**MSOLAP_SUPPORTS_DRILLTHROUGH**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob der Dienst Drillthroughfunktionen unterstützt.<br /><br /> Wenn **"true"**, der Dienst unterstützt Drillthrough Funktionen.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **DMSCHEMA_MINING_SERVICES** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**DIENSTNAME**|**DBTYPE_WSTR**|Optional.|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Schemarowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
