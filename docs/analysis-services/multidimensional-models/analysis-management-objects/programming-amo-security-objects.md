---
title: Programmieren von AMO-Sicherheitsobjekten | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 949818a7dd9de846166ba149f47165b874c738e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="programming-amo-security-objects"></a>Programmieren von AMO-Sicherheitsobjekten
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]setzt das Programmieren von Sicherheitsobjekten und das Ausführen von Anwendungen, die diese AMO-Sicherheitsobjekte verwenden, die Mitgliedschaft bei der Gruppe der Serveradministratoren oder Datenbankadministratoren voraus. Serveradministrator und Datenbankadministrator sind von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]angegebene Zugriffsebenen.  
  
 In [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] wird der Benutzerzugriff auf beliebige Objekte durch eine Kombination aus Rollen und Berechtigungen gewährt, die dem jeweiligen Objekt zugewiesen werden. Weitere Informationen finden Sie unter [AMO-Sicherheitsklassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md).  
  
## <a name="role-and-permission-objects"></a>Role- und Berechtigungsobjekte  
 Serverrollen enthalten nur eine Rolle in der Auflistung: die des Administrators. Neue Rollen können der Serverrollenauflistung nicht hinzugefügt werden. Die Rolle eines Administrators ermöglicht den vollständigen Zugriff auf jedes Objekt auf dem Server.  
  
 <xref:Microsoft.AnalysisServices.Role>-Objekte werden auf Datenbankebene erstellt. Die Rollenverwaltung erfordert lediglich das Hinzufügen oder Entfernen von Mitgliedern zu oder aus einer Rolle sowie das Hinzufügen oder Löschen von Rollen zum oder aus dem <xref:Microsoft.AnalysisServices.Database>-Objekt. Eine Rolle kann nicht gelöscht werden, wenn keine <xref:Microsoft.AnalysisServices.Permission> Objekt, das der Rolle zugeordnet. Zum Löschen einer Rolle alle <xref:Microsoft.AnalysisServices.Permission> Objekte in der <xref:Microsoft.AnalysisServices.Database> Objekte durchsucht werden müssen, und die <xref:Microsoft.AnalysisServices.Role> entfernt von Berechtigungen, bevor die <xref:Microsoft.AnalysisServices.Role> kann gelöscht werden, aus der <xref:Microsoft.AnalysisServices.Database>.  
  
 Berechtigungen definieren die aktivierten Aktionen des Objekts, für das die Berechtigung erteilt wird. Berechtigungen für die folgenden Objekte angegeben werden: <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MiningStructure>, und <xref:Microsoft.AnalysisServices.MiningModel>. Die Berechtigungsverwaltung schließt das Gewähren oder Widerrufen von aktiviertem Zugriff durch die entsprechende Zugriffseigenschaft ein. Für jeden aktivierten Zugriff gibt es eine Eigenschaft, die auf die gewünschte Zugriffsstufe festgelegt werden kann. Der Zugriff kann für die folgenden Vorgänge definiert werden: Verarbeiten, ReadDefinition, Lesen, Schreiben und Verwalten. Verwalten der Zugriff wird nur definiert, auf die <xref:Microsoft.AnalysisServices.Database> Objekt. Die Datenbankadministratorsicherheitsstufe wird erteilt, wenn die Rollenmitgliedschaft gemeinsam mit der Datenbankberechtigung für die Verwaltung gewährt wird.  
  
 Im folgenden Beispiel werden vier Rollen erstellt: Database Administrators (Datenbankadministratoren), Processors (Verarbeiter), Writers (Schreiber) und Readers (Leser).  
  
 Datenbankadministratoren können die angegebene Datenbank verwalten.  
  
 Verarbeiter können alle Objekte in einer Datenbank verarbeiten und Ergebnisse überprüfen. Um Ergebnisse zu überprüfen, muss der Lesezugriff auf das Datenbankobjekt explizit für den angegebenen Cube aktiviert werden, da die Leseberechtigung nicht für alle untergeordneten Objekte gilt.  
  
 Schreiber können vom angegebenen Cube lesen und darin schreiben. Der Zellzugriff ist in der Kundendimension auf die USA begrenzt.  
  
 Leser können vom angegebenen Cube lesen. Der Zellzugriff ist in der Kundendimension auf die USA begrenzt.  
  
```  
static public void CreateRolesAndPermissions(Database db, Cube cube)  
{  
    Role role;  
    DatabasePermission dbperm;  
    CubePermission cubeperm;  
  
    #region Create the Database Administrators role  
  
    // Create the Database Administrators role.  
    role = db.Roles.Add("Database Administrators");  
    role.Members.Add(new RoleMember("")); // e.g. domain\user  
    role.Update();  
  
    // Assign administrative permissions to this role.  
    // Members of this role can perform any operation within the database.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Administer = true;  
    dbperm.Update();  
  
    #endregion  
  
    #region Create the Processors role  
  
    // Create the Processors role.  
    role = db.Roles.Add("Processors");  
    role.Members.Add(new RoleMember("")); // e.g. myDomain\johndoe  
    role.Update();  
  
    // Assign Read and Process permissions to this role.  
    // Members of this role can process objects in the database and query them to verify results.  
    // Process permission applies to all contained objects, i.e. all dimensions and cubes.  
    // Read permission does not apply to contained objects, so we must assign the permission explicitly on the cubes.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Process = true;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Writers role  
  
    // Create the Writers role.  
    role = db.Roles.Add("Writers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read and Write permissions to this role.  
    // Members of this role can discover, query and writeback to the Adventure Works cube.  
    // However cell access and writeback is restricted to the United States (in the Customer dimension).  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Write = WriteAccess.Allowed;  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.Read, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.ReadWrite, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Readers role  
  
    // Create the Readers role.  
    role = db.Roles.Add("Readers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read permissions to this role.  
    // Members of this role can discover and query the Adventure Works cube.  
    // However the Customer dimension is restricted to the United States.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    Dimension dim = db.Dimensions.GetByName("Customer");  
    DimensionAttribute attr = dim.Attributes.GetByName("Country-Region");  
    CubeDimensionPermission cubedimperm = cubeperm.DimensionPermissions.Add(dim.ID);  
    cubedimperm.Read = ReadAccess.Allowed;  
    AttributePermission attrperm = cubedimperm.AttributePermissions.Add(attr.ID);  
    attrperm.AllowedSet = "{[Customer].[Country-Region].[Country-Region].&[United States]}";  
    cubeperm.Update();  
  
    #endregion  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programmieren AMO-Sicherheitsobjekten](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [Berechtigungen und Zugriffsrechte & #40; Analysis Services – mehrdimensionale Daten & #41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Logische Architektur & #40; Analysis Services – mehrdimensionale Daten & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte & #40; Analysis Services – mehrdimensionale Daten & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
