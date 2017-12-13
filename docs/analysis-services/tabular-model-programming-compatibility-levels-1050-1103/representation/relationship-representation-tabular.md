---
title: Beziehungsdarstellung (tabellarisch) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 86a5eff8-4e07-444b-ac15-5695f09aa105
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3204dee0af5235847920c41d9738a1c2ecdcfb9c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="relationship-representation-tabular"></a>Beziehungsdarstellung (tabellarisch)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Eine Beziehung ist eine Verbindung zwischen zwei Tabellen mit Daten. Die Beziehung legt fest, wie die Daten in den beiden Tabellen korreliert werden sollen.  
  
 Finden Sie unter [Beziehungsdarstellung (tabellarisch)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/relationship-representation-tabular.md) für eine ausführliche Erläuterung zum Erstellen und Bearbeiten der beziehungsdarstellung.  
  
## <a name="relationship-representation"></a>Beziehungsdarstellung  
 In tabellarischen Modellen können mehrere Beziehungen zwischen zwei Tabellen definiert werden. Wenn mehrere Beziehungen zwischen zwei Tabellen definiert werden, kann nur eine als Standardbeziehung für das Modell definiert werden und wird als aktive Beziehung bezeichnet. Alle anderen Beziehungen werden als inaktive Beziehungen bezeichnet.  
  
### <a name="relationship-in-amo"></a>Beziehung in AMO  
 Im Hinblick auf AMO-Objekte verfügen alle inaktiven Beziehungen über eine Darstellung einer 1:1-Zuordnungsbeziehung zu <xref:Microsoft.AnalysisServices.Relationship>, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Für die aktive Beziehung gelten andere Anforderungen, und es ist zusätzlich eine Zuordnung zu <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> erforderlich.  
  
 Die folgenden Codeausschnitte veranschaulichen, wie eine Beziehung in tabellarischen Modellen erstellt, wie eine Beziehung aktiviert und wie ein Primärschlüssel (abweichend von "RowNumber") in einer Tabelle definiert wird. Um eine aktive Beziehung zu erstellen, muss ein Primärschlüssel in der Primärschlüsseltabelle PKTableName der Beziehung (der 1-Seite der Beziehung) definiert werden. Im hier gezeigten Beispiel wird der Primärschlüssel für PKColumnName erstellt, sofern kein Primärschlüssel in dieser Spalte definiert ist. Beim Erstellen inaktiver Beziehungen ist kein Primärschlüssel in der Primärschlüsselspalte erforderlich.  
  
```  
  
private Boolean createRelationship(string PKTableName, string PKColumnName, string MVTableName, string MVColumnName, AMO.Database tabularDb, string cubeName, Boolean forceActive)  
{  
    //verify input parameters  
    if(     string.IsNullOrEmpty(PKTableName) || string.IsNullOrWhiteSpace(PKTableName)  
        ||  string.IsNullOrEmpty(PKColumnName) || string.IsNullOrWhiteSpace(PKColumnName)  
        ||  string.IsNullOrEmpty(MVTableName) || string.IsNullOrWhiteSpace(MVTableName)  
        ||  string.IsNullOrEmpty(MVColumnName) || string.IsNullOrWhiteSpace(MVColumnName)  
        ||  (tabularDb == null)  
        ) return false;  
    if(!tabularDb.Dimensions.ContainsName(PKTableName) || !tabularDb.Dimensions.ContainsName(MVTableName)) return false;  
    if(!tabularDb.Dimensions[PKTableName].Attributes.ContainsName(PKColumnName) || !tabularDb.Dimensions[MVTableName].Attributes.ContainsName(MVColumnName)) return false;  
  
    //Verify underlying cube structure  
    if (!tabularDb.Cubes[cubeName].Dimensions.ContainsName(PKTableName) || !tabularDb.Cubes[cubeName].Dimensions.ContainsName(MVTableName)) return false; //Should return an exception!!  
    if (!tabularDb.Cubes[cubeName].MeasureGroups.ContainsName(PKTableName) || !tabularDb.Cubes[cubeName].MeasureGroups.ContainsName(MVTableName)) return false; //Should return an exception!!  
  
    //Make sure PKTableName.PKColumnName  is set as PK ==> <attribute>.usage == AMO.AttributeUsage.Key  
    if (tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].Usage != AMO.AttributeUsage.Key)  
    {  
        //... here we are 'fixing', if there is an issue with PKTableName.PKColumnName not beeing the PK of the table  
        setPKColumn(tabularDb, PKTableName, PKColumnName);  
    }  
  
    //Terminology note:   
    // -   the many side of the relationship is named the From end in AMO  
    // -   the PK side of the relationship in named the To end in AMO  
    //  
    //It seems relationships flow FROM the many side of the relationship in TO the primary key side of the relationship in AMO  
    //              
    //Verify the relationship we are creating does not exist, regardless of name.  
    //if it exists, return true (no need to recreate it)  
    //if it doesn't exists it will be created after this validation  
  
    //   
    foreach (AMO.Relationship currentRelationship in tabularDb.Dimensions[MVTableName].Relationships)  
    {  
        if ((currentRelationship.FromRelationshipEnd.Attributes[0].AttributeID == MVColumnName)  
            && (currentRelationship.ToRelationshipEnd.DimensionID == PKTableName)  
            && (currentRelationship.ToRelationshipEnd.Attributes[0].AttributeID == PKColumnName))  
        {  
            if (forceActive)  
            {  
                //Activate the relationship   
                setActiveRelationship(tabularDb.Cubes[cubeName], MVTableName, MVColumnName, PKTableName, currentRelationship.ID);  
                //Update server with changes made here  
                tabularDb.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.CreateOrReplace);  
                tabularDb.Cubes[cubeName].MeasureGroups[MVTableName].Process(AMO.ProcessType.ProcessFull);  
            }  
            return true;  
        }  
    }  
  
    //A relationship like the one to be created does not exist; ergo, let's create it:  
  
    //First, create the INACTIVE relationship definitions in the MultipleValues end of the relationship  
    #region define unique name for relationship  
    string newRelationshipID = string.Format("Relationship _{0}_{1}_ to _{2}_{3}_", MVTableName, MVColumnName, PKTableName, PKColumnName);  
    int rootLen = newRelationshipID.Length;  
    for (int i = 0; tabularDb.Dimensions[MVTableName].Relationships.Contains(newRelationshipID); )  
    {  
        newRelationshipID = string.Format("{0}_{1,8:0}", newRelationshipID.Substring(0, rootLen), i);  
    }  
    #endregion  
    AMO.Relationship newRelationship = tabularDb.Dimensions[MVTableName].Relationships.Add(newRelationshipID);  
  
    newRelationship.FromRelationshipEnd.DimensionID = MVTableName;  
    newRelationship.FromRelationshipEnd.Attributes.Add(MVColumnName);  
    newRelationship.FromRelationshipEnd.Multiplicity = AMO.Multiplicity.Many;  
    newRelationship.FromRelationshipEnd.Role = string.Empty;  
    newRelationship.ToRelationshipEnd.DimensionID = PKTableName;  
    newRelationship.ToRelationshipEnd.Attributes.Add(PKColumnName);  
    newRelationship.ToRelationshipEnd.Multiplicity = AMO.Multiplicity.One;  
    newRelationship.ToRelationshipEnd.Role = string.Empty;  
  
    //Update server to create relationship  
    tabularDb.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    tabularDb.Dimensions[MVTableName].Process(AMO.ProcessType.ProcessDefault);  
    tabularDb.Dimensions[PKTableName].Process(AMO.ProcessType.ProcessDefault);  
  
    //Second, activate the relationship if relationship is to be set as the active relationship: 'forceActive==true'  
    //... an inactive relationship needs only to be created on the dimensions object  
    if (forceActive)  
    {  
        //Activate the relationship   
        setActiveRelationship(tabularDb.Cubes[cubeName], MVTableName, MVColumnName, PKTableName, newRelationshipID);                  
    }             
    return true;  
}  
  
private void setActiveRelationship(AMO.Cube currentCube, string MVTableName, string MVColumnName, string PKTableName, string relationshipID)  
{  
    if (!currentCube.MeasureGroups.Contains(MVTableName))  
    {  
        throw new AMO.AmoException(string.Format("Cube [{0}] does not contain Measure Group [{1}]\nError activating relationship [{2}]: [{4}] <--- [{1}].[{3}]"  
                                                , currentCube.Name, MVTableName, relationshipID, MVColumnName, PKTableName));  
    }  
    AMO.MeasureGroup currentMG = currentCube.MeasureGroups[MVTableName];  
  
    if (!currentMG.Dimensions.Contains(PKTableName))  
    {  
        AMO.ReferenceMeasureGroupDimension newReferenceMGDim = new AMO.ReferenceMeasureGroupDimension();  
        newReferenceMGDim.CubeDimensionID = PKTableName;  
        newReferenceMGDim.IntermediateCubeDimensionID = MVTableName;  
        newReferenceMGDim.IntermediateGranularityAttributeID = MVColumnName;  
        newReferenceMGDim.Materialization = AMO.ReferenceDimensionMaterialization.Regular;  
        newReferenceMGDim.RelationshipID = relationshipID;  
        foreach (AMO.CubeAttribute PKAttribute in currentCube.Dimensions[PKTableName].Attributes)  
        {  
            AMO.MeasureGroupAttribute PKMGAttribute = newReferenceMGDim.Attributes.Add(PKAttribute.AttributeID);  
            OleDbType PKMGAttributeType = PKAttribute.Attribute.KeyColumns[0].DataType;  
            PKMGAttribute.KeyColumns.Add(new AMO.DataItem(PKTableName, PKAttribute.AttributeID, PKMGAttributeType));  
            PKMGAttribute.KeyColumns[0].Source = new AMO.ColumnBinding(PKTableName, PKAttribute.AttributeID);  
        }  
        currentMG.Dimensions.Add(newReferenceMGDim);  
  
        AMO.ValidationErrorCollection errors = new AMO.ValidationErrorCollection();  
  
        newReferenceMGDim.Validate(errors, true);  
        if (errors.Count > 0)  
        {  
            StringBuilder errorMessages = new StringBuilder();  
            foreach (AMO.ValidationError err in errors)  
            {  
                errorMessages.AppendLine(string.Format("At {2}: # {0} : {1}", err.ErrorCode, err.FullErrorText, err.Source));  
            }  
            throw new AMO.AmoException(errorMessages.ToString());  
        }  
        //Update changes in the server  
        currentMG.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.CreateOrReplace);  
    }  
    else  
    {  
        AMO.ReferenceMeasureGroupDimension currentReferenceMGDim = (AMO.ReferenceMeasureGroupDimension)currentMG.Dimensions[PKTableName];  
        currentReferenceMGDim.RelationshipID = relationshipID;  
        currentReferenceMGDim.IntermediateGranularityAttributeID = MVColumnName;  
        //Update changes in the server  
        currentMG.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    }  
    //process MG to activate relationship  
    currentMG.Process(AMO.ProcessType.ProcessFull);  
  
}  
  
private void setPKColumn(AMO.Database tabularDb, string PKTableName, string PKColumnName)  
{  
        //Find all 'unwanted' Key attributes, remove their Key definitions and include the attributes in the ["RowNumber"].AttributeRelationships  
        foreach (AMO.DimensionAttribute currentDimAttribute in tabularDb.Dimensions[PKTableName].Attributes)  
        {  
            if ((currentDimAttribute.Usage == AMO.AttributeUsage.Key) && (currentDimAttribute.ID != PKColumnName))  
            {  
                currentDimAttribute.Usage = AMO.AttributeUsage.Regular;  
                if (currentDimAttribute.ID != "RowNumber")  
                {  
                    currentDimAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Preserve;  
                    currentDimAttribute.AttributeRelationships.Clear();  
                    if (!tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.ContainsName(currentDimAttribute.ID))  
                    {  
                        AMO.DimensionAttribute currentAttribute = tabularDb.Dimensions[PKTableName].Attributes[currentDimAttribute.ID];  
                        AMO.AttributeRelationship currentAttributeRelationship = tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.Add(currentAttribute.ID);  
                        currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
                    }  
                    tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships[currentDimAttribute.ID].Cardinality = AMO.Cardinality.Many;  
                }  
            }  
        }  
  
        //Remove PKColumnName from ["RowNumber"].AttributeRelationships  
        int PKAtribRelationshipPosition = tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.IndexOf(PKColumnName);  
        if (PKAtribRelationshipPosition != -1) tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.RemoveAt(PKAtribRelationshipPosition, true);  
  
        //Define PKColumnName as Key and add ["RowNumber"] to PKColumnName.AttributeRelationships with cardinality of One  
        tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].Usage = AMO.AttributeUsage.Key;  
        tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].KeyColumns[0].NullProcessing = AMO.NullProcessing.Error;  
        if (!tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].AttributeRelationships.ContainsName("RowNumber"))  
        {  
            AMO.DimensionAttribute currentAttribute = tabularDb.Dimensions[PKTableName].Attributes["RowNumber"];  
            AMO.AttributeRelationship currentAttributeRelationship = tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].AttributeRelationships.Add(currentAttribute.ID);  
            currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
        }  
        tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].AttributeRelationships["RowNumber"].Cardinality = AMO.Cardinality.One;  
  
        //Update Table before going creating the relationship  
        tabularDb.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        tabularDb.Dimensions[PKTableName].Process(AMO.ProcessType.ProcessDefault);                
  
}  
  
```  
  
## <a name="amo2tabular-sample"></a>AMO2Tabular-Beispiel  
 Um jedoch einen Einblick in die Verwendung von AMO zur Erstellung und Bearbeitung von Beziehungsdarstellungen zu gewinnen, können Sie den Quellcode im AMO2Tabular-Beispiel einsehen. Das Beispiel ist auf Codeplex verfügbar. Ein wichtiger Hinweis zum Code: Der Code wird nur zur Verdeutlichung für die logischen Konzepte bereitgestellt, die hier erläutert werden, und sollte nicht in einer Produktionsumgebung verwendet oder zu anderen als Lehrzwecken eingesetzt werden.  
  
  
