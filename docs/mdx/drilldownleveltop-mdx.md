---
title: DrilldownLevelTop (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d6532998f65625bf3dacd11de2949a3478ba6ea
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146215"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  Führt einen Drilldown der obersten Elemente einer Menge auf einer bestimmten Ebene in eine darunter liegende Ebene aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Count*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *Include_Calc_Members*  
 Ein Schlüsselwort zum Hinzufügen berechneter Elemente zu Drilldown-Ergebnissen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Wert angegeben wird, sortiert die **DrilldownLevelTop** -Funktion die untergeordneten Elemente jedes Elements in der angegebenen Menge absteigend nach dem Wert des numerischen Ausdrucks, ausgewertet über der Menge der untergeordneten Elemente. Wenn kein numerischer Wert angegeben wird, sortiert die Funktion die untergeordneten Elemente jedes Elements in der angegebenen Menge absteigend nach den Werten der durch die Menge der untergeordneten Elemente dargestellten Zellen, bestimmt durch den Abfragekontext.  
  
 Nach dem Sortieren gibt die **DrilldownLevelTop** -Funktion eine Menge zurück, die die übergeordneten Elemente und die in *Count,* angegebene Anzahl der untergeordneten Elemente mit dem höchsten Wert enthält.  
  
 Die **DrilldownLevelTop** -Funktion gleicht der [DrilldownLevel](../mdx/drilldownlevel-mdx.md) -Funktion, statt jedoch alle untergeordneten Elemente für jedes Element auf der angegebenen Ebene einzuschließen, gibt die **DrilldownLevelTop** -Funktion die angegebene Anzahl der obersten untergeordneten Elemente zurück.  
  
 Abfrage der XMLA-Eigenschaft MdpropMdxDrillFunctions können Sie das Maß an Unterstützung, die der Server die drillingfunktionen bereitgestellt; finden Sie unter [unterstützte XMLA-Eigenschaften &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) Details.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die obersten drei untergeordneten Elemente der Product Category-Ebene basierend auf dem Standardmeasure zurückgegeben. Im Adventure Works-Beispielcube sind die obersten drei untergeordneten Elemente für Accessories Bike Racks, Bike Stands und Bottles and Cages. In Management Studio können Sie im MDX-Abfragefenster zu Products | Product Categories | Members | All Products | Accessories navigieren, um die vollständige Liste anzuzeigen. Sie können das Count-Argument erhöhen, damit mehr Elemente zurückgegeben werden.  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 Im nächsten Beispiel wird die Verwendung des **include_calc_members** -Flags gezeigt. Dieses wird genutzt, um berechnete Elemente auf Drilldown-Ebene einzuschließen. Das Measure [Reseller Order Count] befindet sich in der **DrilldownLevelTop** -Anweisung, um sicherzustellen, dass die Rückgabewerte nach diesem Measure sortiert werden.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX-Funktionsreferenz &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
