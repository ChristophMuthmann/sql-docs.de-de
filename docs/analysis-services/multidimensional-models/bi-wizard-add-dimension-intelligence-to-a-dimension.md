---
title: Hinzufügen von Dimensionsintelligenz zu einer Dimension | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1a2f25da5b783457bb22be62de181a391daab728
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bi-wizard---add-dimension-intelligence-to-a-dimension"></a>BI-Assistent – Hinzufügen von Dimensionsintelligenz zu einer Dimension
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Fügen Sie einem Cube oder einer Dimension die Erweiterung für die Dimensionsintelligenz hinzu, um einen Standardunternehmenstyp für eine Dimension anzugeben. Durch diese Erweiterung werden auch die entsprechenden Typen für Dimensionsattribute angegeben. Diese Typspezifikationen können von Clientanwendungen bei der Datenanalyse verwendet werden.  
  
 Verwenden Sie den Business Intelligence-Assistenten, und wählen Sie auf der Seite **Erweiterung auswählen** die Option **Dimensionsintelligenz definieren** aus, um die Dimensionsintelligenz hinzuzufügen. Anschließend führt Sie der Assistent durch die Schritte zum Auswählen einer Dimension, für die Sie die Dimensionsintelligenz anwenden möchten, und zum Identifizieren der Attribute für die ausgewählte Dimension.  
  
## <a name="selecting-a-dimension"></a>Auswählen einer Dimension  
 Auf der ersten Seite **Optionen für Dimensionsintelligenz festlegen** des Assistenten geben Sie die Dimension an, für die Sie die Dimensionsintelligenz anwenden möchten. Die Erweiterung für die Dimensionsintelligenz, die dieser ausgewählten Dimension hinzugefügt wurde, führt zu Änderungen an der Dimension. Diese Änderungen werden an alle Cubes vererbt, die die ausgewählte Dimension enthalten.  
  
> [!NOTE]  
>  Wenn Sie **Account** als Dimension auswählen, geben Sie die Kontointelligenz für die Dimension an. Weitere Informationen finden Sie unter [Hinzufügen von Kontointelligenz zu einer Dimension](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="specifying-dimension-attributes"></a>Angeben von Dimensionsattributen  
 Durch die Auswahl, die Sie auf der Seite **Dimensionsintelligenz definieren** im Listenfeld **Dimensionstyp** treffen, wird die **Type** -Eigenschaft der Dimension festgelegt. Die Einstellung der **Type** -Eigenschaft stellt Servern und Clientanwendungen Informationen zum Inhalt einer Dimension bereit. Einige Einstellungen stellen nur eine Richtlinie für Clientanwendungen bereit. Diese Einstellungen sind optional. Andere Einstellungen, wie Accounts oder Time, legen spezielle Verhaltensweisen fest und sind möglicherweise zum Implementieren bestimmter Business Intelligence-Erweiterungen erforderlich. In SQL Server Management Studio wird der Dimensionstyp beispielsweise verwendet, um eine Currency-Dimension zu identifizieren und die entsprechenden Währungsumrechnungsregeln festzulegen. Die Standardeinstellung für den **Dimensionstyp** ist **Regular**, womit keine Annahmen zum Inhalt der Dimension gemacht werden.  
  
 Nach dem Auswählen des Dimensionstyps aktivieren Sie in **Dimensionsattribute**in der Spalte **Einschließen** das Kontrollkästchen neben den einzelnen Standardattributtypen, für die ein entsprechendes Attribut in der Dimension vorhanden ist. Erweitern Sie dann die Dropdownliste in der Spalte **Dimensionsattribut** , und wählen Sie das Attribut in der Dimension aus, das dem ausgewählten Attributtyp entspricht. Durch das Auswählen des Attributs in der Liste wird die Attributeigenschaft **Type** für die Attribute festgelegt.  
  
 Sie möchten beispielsweise einer Accounts-Dimension die Dimensionsintelligenz hinzufügen. Hierzu wählen Sie unter **Dimensionstyp**die Option **Accounts**aus. Wenn für die Dimension die Attribute **Account Type** und **Account Description** angegeben sind, aktivieren Sie anschließend in der Spalte **Einschließen** die Kontrollkästchen für die Kontotypen **Kontoname** und **Kontotyp** . Verknüpfen Sie diese Kontotypen dann in der Spalte **Dimensionsattribut** jeweils mit den Attributen **Account Description** und **Account Type** in der Dimension.  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren von Zeitintelligenzberechnungen mithilfe des Business Intelligence-Assistenten](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  
