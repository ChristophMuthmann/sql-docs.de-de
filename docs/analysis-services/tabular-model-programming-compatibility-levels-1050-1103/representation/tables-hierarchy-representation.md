---
title: Hierarchiedarstellung (tabellarisch) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 1d53dda1-f2c8-4a9b-8ec7-78f43ca1d7db
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 58ee908dc3dbf745a15c8dfa5f44d711f91c392b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="tables---hierarchy-representation"></a>Tabellen - Hierarchiedarstellung
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]In tabellarischen Modellen ist eine Hierarchie Navigationspfad von einem Attribut zu einem anderen basierend auf Werten, die vom Benutzer ausgewählt wurden.  
  
## <a name="hierarchy-representation"></a>Hierarchiedarstellung  
  
### <a name="hierarchy-in-amo"></a>Hierarchie in AMO  
 Wenn AMO zum Verwalten einer Tabelle für ein tabellarisches Modell verwendet wird, besteht eine 1:1-Objektentsprechung zu einer Hierarchie in AMO. Eine Hierarchie wird dargestellt, indem die <xref:Microsoft.AnalysisServices.Hierarchy> Objekt.  
  
 Der folgende Codeausschnitt veranschaulicht, wie einem vorhandenen tabellarischen Modell eine Hierarchie hinzugefügt wird. Im Code wird davon ausgegangen, dass Sie über das AMO-Datenbankobjekt newDatabase und das AMO-Cubeobjekt modelCube verfügen.  
  
```  
  
private void addHierarchy(  
                    AMO.Database newDatabase  
                 ,  AMO.Cube modelCube  
                 ,  string tableName  
                 ,  string hierarchyName  
                 ,  string levelsText  
             )  
{  
    //Validate input  
    if (string.IsNullOrEmpty(hierarchyName) || string.IsNullOrEmpty(levelsText))  
    {  
        MessageBox.Show(String.Format("Hierarchy Name or Layout must be provided."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
  
    if (!overwriteHierarchy.Checked && newDatabase.Dimensions[tableName].Hierarchies.Contains(hierarchyName))  
    {  
        MessageBox.Show(String.Format("Hierarchy already exists.\nGive a new name or enable overwriting"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
  
    try  
    {  
        if (newDatabase.Dimensions[tableName].Hierarchies.Contains(hierarchyName))  
        {  
            //Hierarchy exists... deleting it to write it later  
            newDatabase.Dimensions[tableName].Hierarchies.Remove(hierarchyName, true);  
            newDatabase.Dimensions[tableName].Update(AMO.UpdateOptions.AlterDependents);  
        }  
        AMO.Hierarchy currentHierarchy = newDatabase.Dimensions[tableName].Hierarchies.Add(hierarchyName, hierarchyName);  
        currentHierarchy.AllMemberName = string.Format("(All of {0})", hierarchyName);  
        //Parse hierarchyLayout  
        using (StringReader levels = new StringReader(levelsText))  
        {  
            //Each line:  
            //  must come with: The columnId of the attribute in the dimension --> this represents the SourceAttributeID  
            //  optional: A display name for the Level (if this argument doesn't come the default is the SourceAttributeID)  
            string line;  
            while ((line = levels.ReadLine()) != null)  
            {  
                if (string.IsNullOrEmpty(line) || string.IsNullOrWhiteSpace(line)) continue;  
                line = line.Trim();  
                string[] hierarchyData = line.Split(',');  
                if (string.IsNullOrEmpty(hierarchyData[0])) continue; //first argument cannot be empty or blank,   
                                                                      //assume is a blank line and ignore it  
                string levelSourceAttributeID = hierarchyData[0].Trim();  
                string levelID = (hierarchyData.Length > 1 && !string.IsNullOrEmpty(hierarchyData[1])) ? hierarchyData[1].Trim() : levelSourceAttributeID;  
                currentHierarchy.Levels.Add(levelID).SourceAttributeID = levelSourceAttributeID;  
            }  
        }  
        newDatabase.Dimensions[tableName].Update(AMO.UpdateOptions.AlterDependents);  
  
    }  
    catch (Exception ex)  
    {  
        MessageBox.Show(String.Format("Error creating hierarchy [{0}].\nError message: {1}", newHierarchyName.Text, ex.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        if (newDatabase.Dimensions[tableName].Hierarchies.Contains(hierarchyName))  
        {  
            //Hierarchy was created but exception prevented complete hierarchy to be written... deleting incomplete hierarchy  
            newDatabase.Dimensions[tableName].Hierarchies.Remove(hierarchyName, true);  
            newDatabase.Dimensions[tableName].Update(AMO.UpdateOptions.AlterDependents);  
        }  
  
    }  
    newDatabase.Dimensions[tableName].Process(AMO.ProcessType.ProcessFull);  
    modelCube.MeasureGroups[tableName].Process(AMO.ProcessType.ProcessFull);  
}  
  
```  
  
  
