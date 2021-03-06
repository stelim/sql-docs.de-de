---
title: XQuery-Operatoren für den Xml-Datentyp | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 10102e3c726a3703a3a9f3aa953171fb4a5dd79b
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119278"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>XQuery-Operatoren für den xml-Datentyp
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery unterstützt die folgenden Operatoren:  
  
-   Numerische Operatoren (+, -, *, div, mod)  
  
-   Operatoren für Wertvergleiche (eq, ne, lt, gt, le, ge)  
  
-   Operatoren für allgemeine Vergleiche (=,! =, \<, >, \<=, > =)  
  
 Weitere Informationen zu diesen Operatoren finden Sie unter [Vergleichsausdrücke &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-general-operators"></a>A. Verwenden von allgemeinen Operatoren  
 Die folgende Abfrage zeigt die Verwendung allgemeiner Operatoren, die für Sequenzen gelten, sowie das Vergleichen von Sequenzen. Die Abfrage ruft eine Sequenz von Rufnummern für jeden Kunden aus der **AdditionalContactInfo** Spalte die **wenden Sie sich an** Tabelle. Diese Sequenz wird dann mit der Sequenz von zwei Rufnummern ("111-111-1111", "222-2222") verglichen.  
  
 Die Abfrage verwendet die **=** Vergleichsoperator. Jeder Knoten in der Sequenz auf der rechten Seite des der **=** Operator wird verglichen, wobei jeder Knoten in der Sequenz auf der linken Seite. Wenn die Knoten entsprechen ergibt, der knotenvergleich **"true"**. Der Wert wird anschließend in einen int-Wert konvertiert und mit 1 verglichen; die Abfrage gibt dann die Kunden-ID zurück.  
  
```sql
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 Besteht eine weitere Möglichkeit, beachten Sie, wie die vorherige Abfrage funktioniert: jeder rufnummernwert abgerufen, die von der **AdditionalContactInfo** Spalte mit dem Satz von zwei Rufnummern verglichen wird. Wenn der Wert im Satz enthalten ist, wird der betreffende Kunde im Ergebnis zurückgegeben.  
  
### <a name="b-using-a-numeric-operator"></a>B. Verwenden eines numerischen Operators  
 Der +-Operator in dieser Abfrage ist ein Wertoperator, weil er sich auf ein einzelnes Element bezieht. Der Wert 1 wird z. B. zu einer Chargengröße addiert, die von der Abfrage zurückgegeben wird:  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. Verwenden eines Wertoperators  
 Die folgende Abfrage ruft die <`Picture`>-Elemente für ein Produktmodell ab, wobei die Bildgröße "small" ist:  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Da beide der Operanden der **Eq** Operator atomare Werte, der Wert-Operator wird verwendet, in der Abfrage. Sie können die gleiche Abfrage schreiben, mithilfe des allgemeinen Vergleichsoperators ( **=** ).  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Funktionen für den Xml-Datentyp](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
