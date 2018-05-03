---
title: Rollen | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c23948ae3a3326a6d8139b7e9556164108b9e1d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="roles"></a>Rollen
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Mit Rollen werden in tabellarischen Modellen Elementberechtigungen für ein Modell definiert. Rollenmitglieder können die durch die Rollenberechtigung definierten Aktionen für das Modell ausführen. Rollen, die mit Leseberechtigungen definiert wurden, können zusätzliche Sicherheit auf Zeilenebene bieten, indem Filter auf Zeilenebene verwendet werden. 
  
 Für SQL Server Analysis Services enthalten Rollen Benutzer Mitglieder von Windows-Benutzernamen oder Windows-Gruppen und Berechtigungen ("Lesen", "Prozess", "Administrator"). Für Azure Analysis Services müssen Benutzer in Ihrem Azure Active Directory und einen Benutzernamen und angegebene Gruppen Organisations-e Mailadresse oder den Benutzerprinzipalnamen werden. 
  
> [!IMPORTANT]  
>  Bei Benutzern die Verbindung mit einem bereitgestellten Modell mithilfe einer Clientanwendung zur berichtserstellung, müssen Sie mindestens über mindestens eine Rolle mit erstellen Read-Berechtigung, die Benutzer Mitglieder als.  
  
 Informationen in diesem Thema wird von tabellarischen Modellen bestimmt, die Rollen zu definieren, indem Sie mithilfe des Dialogfelds Rollen-Manager in SSDT. Während der Modellerstellung definierte Rollen gelten für die Arbeitsbereichsdatenbank des Modells. Nachdem eine Modelldatenbank bereitgestellt wurde, können Administratoren von modelldatenbanken verwalten (hinzufügen, bearbeiten und löschen) Mitglieder der Rolle mithilfe von SSMS. Zum Verwalten von Rollenmitgliedern in einer bereitgestellten Datenbank finden Sie unter [Rollen für tabellarische Modelle](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
##  <a name="bkmk_underst"></a> Understanding roles  
 Rollen werden in Analysis Services verwendet, um Zugriff auf Modelldaten zu verwalten. Die folgenden beiden Rollen stehen zur Verfügung:  
  
-   Die Serverrolle eine feste Rolle handelt, die Administratorzugriff auf eine Analysis Services-Server-Instanz bereitstellt.  
  
-   Datenbankrollen. Von Modellentwicklern und Administratoren definierte Rollen, mit denen der Zugriff auf eine Modelldatenbank und Daten für Benutzer ohne Administratorrechte gesteuert wird.  
  
 Für ein tabellarisches Modell definierte Rollen sind Datenbankrollen. D. h. die Rollen enthalten Mitglieder in Form von Benutzern oder Gruppen, die über die spezifischen Berechtigungen, die die Aktion definiert diese Mitglieder für die Modelldatenbank ausführen können. Eine Datenbankrolle wird in der Datenbank als separates Objekt erstellt und gilt nur für die Datenbank, in der diese Rolle erstellt wurde. Benutzer und Gruppen sind in der Rolle der Modellentwickler enthalten, die standardmäßig über Administratorberechtigungen auf dem arbeitsbereichsdatenbankserver verfügt; für ein bereitgestelltes Modell von einem Administrator.  
  
 Auf Rollen in tabellarischen Modellen können zusätzlich Zeilenfilter angewendet werden. Zeilenfilter verwenden DAX-Ausdrücke, um die Zeilen in einer Tabelle und die in beliebige Richtungen verknüpften Zeilen zu definieren, die vom Benutzer abgefragt werden können. Zeilenfilter, in denen DAX-Ausdrücke verwendet werden, können nur für die Leseberechtigung sowie die Lese- und Verarbeitungsberechtigung definiert werden. Weitere Informationen finden Sie unter [Zeilenfilter](#bkmk_rowfliters) weiter unten in diesem Thema.  
  
 Wenn Sie ein neues Projekt für tabellarische Modelle erstellen, weist das Modellprojekt standardmäßig keine Rollen auf. Rollen können mithilfe des Dialogfelds Rollen-Manager in SSDT definiert werden. Wenn Rollen während der Modellerstellung definiert werden, werden sie auf die Arbeitsbereichsdatenbank des Modells angewendet. Wenn das Modell bereitgestellt wird, werden die gleichen Rollen auf das bereitgestellte Modell angewendet. Nachdem ein Modell bereitgestellt wurde, können Mitglieder der Serverrolle ([Analysis Services-Administrator) und Datenbankadministratoren das Modell zugeordneten Rollen und die jeweiligen Rollen zugeordnet sind, mithilfe von SSMS Elemente verwalten.  
  
##  <a name="bkmk_permissions"></a> Berechtigungen  
 Jede Rolle verfügt über eine einzelne definierte Datenbankberechtigung (außer der kombinierten Lese- und Verarbeitungsberechtigung). Standardmäßig besitzt eine neue Rolle die Berechtigung "Keine". Wenn Mitglieder daher der Rolle mit der Berechtigung „Keine“ hinzugefügt werden, sind sie nicht in der Lage, Änderungen an der Datenbank vorzunehmen, einen Verarbeitungsvorgang auszuführen, Daten abzufragen oder die Datenbank anzuzeigen, sofern ihnen keine andere Berechtigung erteilt wird.  
  
 Eine Gruppe oder der Benutzer kann Mitglied einer beliebigen Anzahl von Rollen, wobei jede Rolle über eine andere Berechtigung verfügen. Wenn ein Benutzer Mitglied mehrerer Rollen ist, sind die für jede Rolle definierten Berechtigungen kumulativ. Wenn ein Benutzer z. B. Mitglied einer Rolle mit der Leseberechtigung und zusätzlich Mitglied einer Rolle mit der Berechtigung "Keine" ist, verfügt dieser Benutzer über Leseberechtigungen.  
  
 Für jede Rolle kann eine der folgenden Berechtigungen definiert werden:  
  
|Berechtigungen|Description|Zeilenfilter unter Verwendung von DAX|  
|-----------------|-----------------|----------------------------|  
|Keine|Mitglieder können keine Änderungen am Modelldatenbankschema vornehmen und keine Daten abfragen.|Zeilenfilter sind nicht gültig. Benutzer in dieser Rolle können keine Daten anzeigen.|  
|Lesen|Mitglieder sind berechtigt, Daten (auf der Basis von Zeilenfiltern) abzufragen, sie können die Modelldatenbank in SSMS jedoch nicht anzeigen und keine Änderungen am Modell-Datenbankschema vornehmen, und der Benutzer kann das Modell nicht verarbeiten.|Zeilenfilter können angewendet werden. Nur Daten, die in der DAX-Formel des Zeilenfilters angegeben wurden, sind für Benutzer sichtbar.|  
|Lesen und verarbeiten|Mitglieder können Daten (basierend auf Filtern auf Zeilenebene) abfragen und Verarbeitungsvorgänge mithilfe eines Skripts oder eines Pakets ausführen, das einen Verarbeitungsbefehl enthält, sie können jedoch keine Änderungen an der Datenbank vornehmen. Die Modelldatenbank in SSMS nicht angezeigt werden.|Zeilenfilter können angewendet werden. Nur Daten können abgefragt werden, die in der DAX-Formel des Zeilenfilters angegeben wurden.|  
|Verarbeiten|Mitglieder können Verarbeitungsvorgänge ausführen, indem sie ein Skript oder ein Paket ausführen, das einen Verarbeitungsbefehl enthält. Das Modelldatenbankschema kann nicht geändert werden. Daten können nicht abgefragt werden. Die Modelldatenbank in SSMS kann nicht abgefragt werden.|Zeilenfilter sind nicht gültig. Daten können mit dieser Rolle nicht abgefragt werden|  
|Administrator|Mitglieder können Änderungen am Modellschema vornehmen und alle Daten im Modell-Designer, berichterstellungsclient und SSMS Abfragen.|Zeilenfilter sind nicht gültig. Sämtliche Daten können mit dieser Rolle abgefragt werden|  
  
##  <a name="bkmk_rowfliters"></a> Row filters  
 Zeilenfilter definieren, welche Zeilen in einer Tabelle für Mitglieder einer bestimmten Rolle abrufbar sind. Zeilenfilter werden für jede Tabelle in einem Modell mithilfe von DAX-Formeln definiert.  
  
 Zeilenfilter können nur für Rollen mit Leseberechtigung sowie mit Lese- und Verarbeitungsberechtigung definiert werden. Wenn ein Zeilenfilter nicht für eine bestimmte Tabelle definiert ist, sind Mitglieder einer Rolle, die über die Leseberechtigung bzw. die Lese- und Verarbeitungsberechtigung verfügt, standardmäßig in der Lage, alle Zeilen in der Tabelle abzufragen, es sei denn, ein Kreuzfilter von einer anderen Tabelle ist aktiv.  
  
 Sobald ein Zeilenfilter für eine bestimmte Tabelle definiert wurde, werden die Zeilen, die von Mitgliedern dieser spezifischen Rolle abgefragt werden können, durch eine DAX-Formel definiert, die den Wert TRUE oder FALSE ergeben muss. Nicht in die DAX-Formel eingeschlossene Zeilen können nicht abgefragt werden. Beispielsweise können Mitglieder der Rolle „Sales“ in der Tabelle „Customers“ mit dem Zeilenfilterausdruck *=Customers [Country] = USA*ausschließlich Kunden in den USA anzeigen.  
  
 Zeilenfilter gelten für die angegebenen sowie für verknüpfte Zeilen. Wenn eine Tabelle über mehrere Beziehungen verfügt, wird die Sicherheit für die aktive Beziehung mithilfe von Filtern gewährleistet. Für Zeilenfilter und Zeilenfilter, die für verknüpfte Tabellen definiert wurden, wird eine Schnittmenge gebildet. Beispiel:  
  
|Tabelle|DAX-Ausdruck|  
|-----------|--------------------|  
|Region|=Region[Country]="USA"|  
|ProductCategory|=ProductCategory[Name]="Bicycles"|  
|Transaktionen|=Transactions[Year]=2008|  
  
 Im Endeffekt ergeben diese Berechtigungen für die Transactions-Tabelle, dass Mitglieder berechtigt sind, Datenzeilen für Kunden in den USA, die Produktkategorie Bicycles und das Jahr 2008 abzufragen. Benutzer wären nicht in der Lage, Transaktionen außerhalb der USA, Transaktionen, die keine Fahrräder beinhalten, oder Transaktionen in einem anderen Jahr als 2008 abzufragen, es sei denn, sie sind Mitglied einer anderen Rolle, die diese Berechtigungen gewährt.  
  
 Sie können Zugriff auf alle Zeilen für eine ganze Tabelle mithilfe des Filters *=FALSE()* verweigern.  
  
### <a name="dynamic-security"></a>Dynamische Sicherheit  
 Dynamische Sicherheit bietet eine Möglichkeit, Zeilenebenensicherheit basierend auf dem Benutzernamen des aktuell angemeldeten Benutzers oder anhand der CustomData-Eigenschaft zu definieren, die von einer Verbindungszeichenfolge zurückgegeben wurde. Um dynamische Sicherheit zu implementieren, müssen Sie eine Tabelle mit Anmeldewerten (Windows-Benutzername) für Benutzer in das Modell einschließen. Ebenfalls erforderlich ist ein Feld, das verwendet werden kann, um eine bestimmte Berechtigung zu definieren; z. B., eine Tabelle "dimEmployees" mit einer Anmelde-ID (domäne\benutzername) sowie einem Abteilungswert für jeden Mitarbeiter.  
  
 Um dynamische Sicherheit zu implementieren, können Sie die folgenden Funktionen als Teil einer DAX-Formel verwenden, um den Benutzernamen des aktuell angemeldeten Benutzers oder die CustomData-Eigenschaft in einer Verbindungszeichenfolge zurückzugeben:  
  
|Funktion|Description|  
|--------------|-----------------|  
|[USERNAME-Funktion (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)|Gibt "domäne\benutzernamen" des aktuell angemeldeten Benutzers zurück.|  
|[CUSTOMDATA-Funktion (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)|Gibt die CustomData-Eigenschaft in einer Verbindungszeichenfolge zurück.|  
  
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
  
##  <a name="bkmk_testroles"></a> Testing roles  
 Beim Erstellen eines Modellprojekts können Sie die Funktion In Excel analysieren verwenden, um die Wirksamkeit der definierten Rollen zu testen. Wenn Sie im Menü **Modell** im Modell-Designer auf **In Excel analysieren**klicken, bevor Excel geöffnet wird, wird das Dialogfeld **Anmeldeinformationen und Perspektive auswählen** angezeigt. In diesem Dialogfeld können Sie den aktuellen Benutzernamen, einen anderen Benutzernamen, eine Rolle und eine Perspektive angeben, um darüber eine Verbindung mit dem Arbeitsbereichsmodell als Datenquelle herzustellen. Weitere Informationen finden Sie unter [in Excel analysieren](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen und Verwalten von Rollen](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|In den Aufgaben in diesem Thema wird beschrieben, wie Rollen mithilfe des Dialogfelds **Rollen-Manager** erstellt und verwaltet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Perspektiven](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [In Excel analysieren](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME-Funktion (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)   
 [CUSTOMDATA-Funktion (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
