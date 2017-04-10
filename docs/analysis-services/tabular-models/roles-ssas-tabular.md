---
title: "Rollen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Rollen (SSAS – tabellarisch)
  Mit Rollen werden in tabellarischen Modellen Elementberechtigungen für ein Modell definiert. Jede Rolle enthält Mitglieder in Form von Windows-Benutzernamen oder Windows-Gruppen sowie Berechtigungen (Lese-, Verarbeitungs- und Administratorberechtigungen). Rollenmitglieder können die durch die Rollenberechtigung definierten Aktionen für das Modell ausführen. Rollen, die mit Leseberechtigungen definiert wurden, können zusätzliche Sicherheit auf Zeilenebene bieten, indem Filter auf Zeilenebene verwendet werden.  
  
> [!IMPORTANT]  
>  Damit Benutzer unter Verwendung einer Berichterstellungs- oder Datenanalyseclientanwendung eine Verbindung mit einem bereitgestellten Modell herstellen können, müssen Sie mindestens eine Rolle erstellen, die mindestens über eine Leseberechtigung verfügt, und die Benutzer als Mitglieder hinzufügen.  
  
 Die Informationen in diesem Thema richten sich an Entwickler von tabellarischen Modellen, die Rollen mit dem Dialogfeld "Rollen-Manager" in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]definieren. Während der Modellerstellung definierte Rollen gelten für die Arbeitsbereichsdatenbank des Modells. Nachdem eine Modelldatenbank bereitgestellt wurde, können Administratoren von Modelldatenbanken Rollenmitglieder mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwalten (hinzufügen, bearbeiten, löschen). Informationen zum Verwalten von Rollenmitgliedern in einer bereitgestellten Datenbank finden Sie unter [Rollen tabellarischer Modelle &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
 Unter [Tabellenmodellierung &#40;Adventure Works-Tutorial&#41;](../../analysis-services/tabular-modeling-adventure-works-tutorial.md) finden Sie zusätzliche Informationen und Lektionen zum Verwenden dieser Funktion.  
  
 Abschnitte in diesem Thema:  
  
-   [Grundlegendes zu Rollen](#bkmk_underst)  
  
-   [Berechtigungen](#bkmk_permissions)  
  
-   [Zeilenfilter](#bkmk_rowfliters)  
  
-   [Testen von Rollen](#bkmk_testroles)  
  
-   [Verwandte Aufgaben](#bkmk_rt)  
  
##  <a name="bkmk_underst"></a> Grundlegendes zu Rollen  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] werden Rollen zur Verwaltung der Sicherheit für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und Daten verwendet. Die folgenden beiden Rollentypen stehen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zur Verfügung:  
  
-   Die Serverrolle, bei der es sich um eine feste Rolle handelt, mit der der Administratorzugriff auf eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereitgestellt wird.  
  
-   Datenbankrollen. Von Modellentwicklern und Administratoren definierte Rollen, mit denen der Zugriff auf eine Modelldatenbank und Daten für Benutzer ohne Administratorrechte gesteuert wird.  
  
 Für ein tabellarisches Modell definierte Rollen sind Datenbankrollen. Dies bedeutet, dass die Rollen Mitglieder in Form von Windows-Benutzern oder -Gruppen enthalten, die über bestimmte Berechtigungen verfügen, mit denen die Aktion definiert wird, die diese Mitglieder für die Modelldatenbank ausführen können. Eine Datenbankrolle wird in der Datenbank als separates Objekt erstellt und gilt nur für die Datenbank, in der diese Rolle erstellt wurde. Windows-Benutzer und/oder Windows-Gruppen werden vom Modellentwickler, der standardmäßig über Administratorberechtigungen für den Arbeitsbereichsdatenbankserver verfügt, in die Rolle eingefügt. Bei einem bereitgestellten Modell werden sie durch einen Administrator eingefügt.  
  
 Auf Rollen in tabellarischen Modellen können zusätzlich Zeilenfilter angewendet werden. Zeilenfilter verwenden DAX-Ausdrücke, um die Zeilen in einer Tabelle und die in beliebige Richtungen verknüpften Zeilen zu definieren, die vom Benutzer abgefragt werden können. Zeilenfilter, in denen DAX-Ausdrücke verwendet werden, können nur für die Leseberechtigung sowie die Lese- und Verarbeitungsberechtigung definiert werden. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Zeilenfilter](#bkmk_rowfliters) .  
  
 Wenn Sie ein neues Projekt für tabellarische Modelle erstellen, weist das Modellprojekt standardmäßig keine Rollen auf. Rollen können im Dialogfeld "Rollen-Manager" in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]definiert werden. Wenn Rollen während der Modellerstellung definiert werden, werden sie auf die Arbeitsbereichsdatenbank des Modells angewendet. Wenn das Modell bereitgestellt wird, werden die gleichen Rollen auf das bereitgestellte Modell angewendet. Nachdem ein Modell bereitgestellt wurde, können Mitglieder der Serverrolle ([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Administrator) und Datenbankadministratoren die dem Modell zugeordneten Rollen und die jeder Rolle zugeordneten Mitglieder unter Verwendung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwalten.  
  
##  <a name="bkmk_permissions"></a> Berechtigungen  
 Jede Rolle verfügt über eine einzelne definierte Datenbankberechtigung (außer der kombinierten Lese- und Verarbeitungsberechtigung). Standardmäßig besitzt eine neue Rolle die Berechtigung "Keine". Wenn Mitglieder daher der Rolle mit der Berechtigung „Keine“ hinzugefügt werden, sind sie nicht in der Lage, Änderungen an der Datenbank vorzunehmen, einen Verarbeitungsvorgang auszuführen, Daten abzufragen oder die Datenbank anzuzeigen, sofern ihnen keine andere Berechtigung erteilt wird.  
  
 Eine Windows-Gruppe oder ein Windows-Benutzer kann Mitglied einer beliebigen Anzahl von Rollen sein, wobei jede Rolle über eine andere Berechtigung verfügen kann. Wenn ein Benutzer Mitglied mehrerer Rollen ist, sind die für jede Rolle definierten Berechtigungen kumulativ. Wenn ein Benutzer z. B. Mitglied einer Rolle mit der Leseberechtigung und zusätzlich Mitglied einer Rolle mit der Berechtigung "Keine" ist, verfügt dieser Benutzer über Leseberechtigungen.  
  
 Für jede Rolle kann eine der folgenden Berechtigungen definiert werden:  
  
|Berechtigungen|Description|Zeilenfilter unter Verwendung von DAX|  
|-----------------|-----------------|----------------------------|  
|InclusionThresholdSetting|Mitglieder können keine Änderungen am Modelldatenbankschema vornehmen und keine Daten abfragen.|Zeilenfilter sind nicht gültig. Benutzer in dieser Rolle können keine Daten anzeigen.|  
|Lesen|Mitglieder sind berechtigt, Daten (auf der Basis von Zeilenfiltern) abzufragen, sie können die Modelldatenbank in SSMS jedoch nicht anzeigen und keine Änderungen am Modell-Datenbankschema vornehmen, und der Benutzer kann das Modell nicht verarbeiten.|Zeilenfilter können angewendet werden. Nur Daten, die in der DAX-Formel des Zeilenfilters angegeben wurden, sind für Benutzer sichtbar.|  
|Lesen und verarbeiten|Mitglieder können Daten (basierend auf Filtern auf Zeilenebene) abfragen und Verarbeitungsvorgänge mithilfe eines Skripts oder eines Pakets ausführen, das einen Verarbeitungsbefehl enthält, sie können jedoch keine Änderungen an der Datenbank vornehmen. Die Modelldatenbank kann nicht in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]angezeigt werden.|Zeilenfilter können angewendet werden. Nur Daten können abgefragt werden, die in der DAX-Formel des Zeilenfilters angegeben wurden.|  
|Verarbeiten|Mitglieder können Verarbeitungsvorgänge ausführen, indem sie ein Skript oder ein Paket ausführen, das einen Verarbeitungsbefehl enthält. Das Modelldatenbankschema kann nicht geändert werden. Daten können nicht abgefragt werden. Die Modelldatenbank kann nicht in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]abgefragt werden.|Zeilenfilter sind nicht gültig. Daten können mit dieser Rolle nicht abgefragt werden|  
|Administrator|Mitglieder können Änderungen am Modellschema vornehmen und alle Daten im Modell-Designer, im Berichterstellungsclient und in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]abfragen.|Zeilenfilter sind nicht gültig. Sämtliche Daten können mit dieser Rolle abgefragt werden|  
  
##  <a name="bkmk_rowfliters"></a> Zeilenfilter  
 Zeilenfilter definieren, welche Zeilen in einer Tabelle für Mitglieder einer bestimmten Rolle abrufbar sind. Zeilenfilter werden für jede Tabelle in einem Modell mithilfe von DAX-Formeln definiert.  
  
 Zeilenfilter können nur für Rollen mit Leseberechtigung sowie mit Lese- und Verarbeitungsberechtigung definiert werden. Wenn ein Zeilenfilter nicht für eine bestimmte Tabelle definiert ist, sind Mitglieder einer Rolle, die über die Leseberechtigung bzw. die Lese- und Verarbeitungsberechtigung verfügt, standardmäßig in der Lage, alle Zeilen in der Tabelle abzufragen, es sei denn, ein Kreuzfilter von einer anderen Tabelle ist aktiv.  
  
 Sobald ein Zeilenfilter für eine bestimmte Tabelle definiert wurde, werden die Zeilen, die von Mitgliedern dieser spezifischen Rolle abgefragt werden können, durch eine DAX-Formel definiert, die den Wert TRUE oder FALSE ergeben muss. Nicht in die DAX-Formel eingeschlossene Zeilen können nicht abgefragt werden. Beispielsweise können Mitglieder der Rolle „Sales“ in der Tabelle „Customers“ mit dem Zeilenfilterausdruck *=Customers [Country] = USA* ausschließlich Kunden in den USA anzeigen.  
  
 Zeilenfilter gelten für die angegebenen sowie für verknüpfte Zeilen. Wenn eine Tabelle über mehrere Beziehungen verfügt, wird die Sicherheit für die aktive Beziehung mithilfe von Filtern gewährleistet. Für Zeilenfilter und Zeilenfilter, die für verknüpfte Tabellen definiert wurden, wird eine Schnittmenge gebildet. Beispiel:  
  
|Tabelle|DAX-Ausdruck|  
|-----------|--------------------|  
|Region|=Region[Country]="USA"|  
|ProductCategory|=ProductCategory[Name]="Bicycles"|  
|Transaktionen|=Transactions[Year]=2008|  
  
 Im Endeffekt ergeben diese Berechtigungen für die Transactions-Tabelle, dass Mitglieder berechtigt sind, Datenzeilen für Kunden in den USA, die Produktkategorie Bicycles und das Jahr 2008 abzufragen. Benutzer wären nicht in der Lage, Transaktionen außerhalb der USA, Transaktionen, die keine Fahrräder beinhalten, oder Transaktionen in einem anderen Jahr als 2008 abzufragen, es sei denn, sie sind Mitglied einer anderen Rolle, die diese Berechtigungen gewährt.  
  
 Sie können Zugriff auf alle Zeilen für eine ganze Tabelle mithilfe des Filters *=FALSE()* verweigern.  
  
### Dynamische Sicherheit  
 Dynamische Sicherheit bietet eine Möglichkeit, Zeilenebenensicherheit basierend auf dem Benutzernamen des aktuell angemeldeten Benutzers oder anhand der CustomData-Eigenschaft zu definieren, die von einer Verbindungszeichenfolge zurückgegeben wurde. Um dynamische Sicherheit zu implementieren, müssen Sie eine Tabelle mit Anmeldewerten (Windows-Benutzername) für Benutzer in das Modell einschließen. Ebenfalls erforderlich ist ein Feld, das verwendet werden kann, um eine bestimmte Berechtigung zu definieren; z. B., eine Tabelle "dimEmployees" mit einer Anmelde-ID (domäne\benutzername) sowie einem Abteilungswert für jeden Mitarbeiter.  
  
 Um dynamische Sicherheit zu implementieren, können Sie die folgenden Funktionen als Teil einer DAX-Formel verwenden, um den Benutzernamen des aktuell angemeldeten Benutzers oder die CustomData-Eigenschaft in einer Verbindungszeichenfolge zurückzugeben:  
  
|Funktion|Description|  
|--------------|-----------------|  
|[USERNAME-Funktion (DAX)](http://msdn.microsoft.com/de-de/22dddc4b-1648-4c89-8c93-f1151162b93f)|Gibt "domäne\benutzernamen" des aktuell angemeldeten Benutzers zurück.|  
|[CUSTOMDATA-Funktion (DAX)](http://msdn.microsoft.com/de-de/58235ad8-226c-43cc-8a69-5a52ac19dd4e)|Gibt die CustomData-Eigenschaft in einer Verbindungszeichenfolge zurück.|  
  
 Sie können die LOOKUPVALUE-Funktion zur Rückgabe von Werten für eine Spalte verwenden, in der der Windows-Benutzername der Gleiche ist wie derjenige, der von der USERNAME-Funktion zurückgegeben wurde oder einer Zeichenfolge entspricht, die von der CustomData-Funktion zurückgegeben wurde. Abfragen können dann eingeschränkt werden, wenn die von LOOKUPVALUE zurückgegebenen Werte Werten in der gleichen oder einer verknüpften Tabelle entsprechen.  
  
 Es wird z. B. die folgende Formel verwendet:  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 Die LOOKUPVALUE-Funktion gibt Werte für die Spalte "dimEmployees[DepartmentId]" zurück, in der "dimEmployees[LoginId]" der "LoginID" für den aktuell angemeldeten Benutzer entspricht, die von USERNAME zurückgegeben wurde, und die Werte für "dimEmployees[DepartmentId]" die Gleichen wie die Werte für "dimDepartmentGroup[DepartmentId]" sind. Die von LOOKUPVALUE in "DepartmentId" zurückgegebenen Werte werden dann verwendet, um die in der Tabelle "dimDepartment" abgefragten Zeilen und alle nach "DepartmentId" verknüpften Tabellen einzuschränken. Es werden nur Zeilen zurückgegeben, bei denen "DepartmentId" auch in den Werten für "DepartmentId" enthalten sind, die von der LOOKUPVALUE-Funktion zurückgegeben wurden.  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Produktion|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Personalwesen|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|Unternehmen|  
|2|Geschäftsführung und Verwaltung|  
|3|Bestandsmanagement|  
|4|Fertigung|  
|5|Qualitätssicherung|  
|6|Forschung und Entwicklung|  
|7|Vertrieb und Marketing|  
  
##  <a name="bkmk_testroles"></a> Testen von Rollen  
 Beim Erstellen eines Modellprojekts können Sie die Funktion In Excel analysieren verwenden, um die Wirksamkeit der definierten Rollen zu testen. Wenn Sie im Menü **Modell** im Modell-Designer auf **In Excel analysieren**klicken, bevor Excel geöffnet wird, wird das Dialogfeld **Anmeldeinformationen und Perspektive auswählen** angezeigt. In diesem Dialogfeld können Sie den aktuellen Benutzernamen, einen anderen Benutzernamen, eine Rolle und eine Perspektive angeben, um darüber eine Verbindung mit dem Arbeitsbereichsmodell als Datenquelle herzustellen. Weitere Informationen finden Sie unter [Analysieren in Excel &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen und Verwalten von Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|In den Aufgaben in diesem Thema wird beschrieben, wie Rollen mithilfe des Dialogfelds **Rollen-Manager** erstellt und verwaltet werden.|  
  
## Siehe auch  
 [Perspektiven &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Analysieren in Excel &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME-Funktion (DAX)](http://msdn.microsoft.com/de-de/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/de-de/73a51c4d-131c-4c33-a139-b1342d10caab)   
 [CUSTOMDATA-Funktion (DAX)](http://msdn.microsoft.com/de-de/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  