---
title: Anzeigen oder Ändern von Modellierungsflags (Datamining) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1ef76a3783251647771e55811722a9303795d23b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="view-or-change-modeling-flags-data-mining"></a>Anzeigen oder Ändern von Modellierungsflags (Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Modellierungsflags sind Eigenschaften, die Sie für eine Miningstrukturspalte oder für Miningmodellspalten festlegen, um zu steuern, wie der Algorithmus die Daten während der Analyse verarbeitet.  
  
 Im Data Mining-Designer können Sie die Modellierungsflags, die einer Miningstruktur oder Miningspalte zugeordnet sind, betrachten und ändern, indem Sie die Eigenschaften der Struktur oder des Modells anzeigen. Sie können Modellierungsflags auch mit DMX, AMO oder XMLA festlegen.  
  
 Diese Prozedur beschreibt, wie die Modellierungsflags im Designer geändert werden.  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>Anzeigen oder Ändern des Modellierungsflags für eine Strukturspalte oder eine Modellspalte  
  
1.  Öffnen Sie in SQL Server Design Studio den Projektmappen-Explorer, und doppelklicken Sie dann auf die Miningstruktur.  
  
2.  Um das NOT NULL-Modellierungsflag festzulegen, klicken Sie auf die Registerkarte **Miningstruktur** . Um das REGRESSOR-Flag oder das MODEL_EXISTENCE_ONLY-Flag festzulegen, klicken Sie auf die Registerkarte **Miningmodell** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Spalte, die Sie anzeigen oder ändern möchten, und wählen Sie **Eigenschaften**aus.  
  
4.  Um ein neues Modellierungsflag hinzuzufügen, klicken Sie auf das Textfeld neben der Eigenschaft **ModelingFlags** , und aktivieren Sie das bzw. die Kontrollkästchen für die Modellierungsflags, die Sie verwenden möchten.  
  
     Modellierungsflags werden nur angezeigt, wenn sie für den Datentyp der Spalte geeignet sind.  
  
    > [!NOTE]  
    >  Nachdem ein Modellierungsflag geändert wurde, muss das Modell erneut verarbeitet werden.  
  
### <a name="get-the-modeling-flags-used-in-the-model"></a>Abrufen der im Modell verwendeten Modellierungsflags  
  
-   Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ein DMX-Abfragefenster, und geben Sie eine Anweisung ähnlich der folgenden ein:  
  
    ```  
    SELECT COLUMN_NAME, CONTENT_TYPE, MODELING_FLAG  
    FROM $system.DMSCHEMA_MINING_COLUMNS  
    WHERE MODEL_NAME = 'Forecasting'  
  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Modellieren von Ablaufverfolgungsflags & #40; Datamining & #41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
