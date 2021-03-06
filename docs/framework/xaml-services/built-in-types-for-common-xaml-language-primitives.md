---
title: "Built-in Types for Common XAML Language Primitives | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XAML language primitives [XAML Services]"
  - "XAML [XAML Services], built-in types"
  - "x:String [XAML Services]"
  - "x:TimeSpan [XAML Services]"
  - "x:Byte [XAML Services]"
  - "x:Double [XAML Services]"
  - "XAML [XAML Services], types"
  - "x:Uri [XAML Services]"
  - "XAML built-in types [XAML Services]"
  - "x:Int64 [XAML Services]"
  - "x:Single [XAML Services]"
  - "x:Int32 [XAML Services]"
ms.assetid: 11de2f08-5b95-4989-b5ec-5178eb968184
caps.latest.revision: 11
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 11
---
# Built-in Types for Common XAML Language Primitives
In XAML 2009 wird die Unterstützung auf XAML\-Sprachebene für mehrere Datentypen eingeführt, bei denen es sich um häufig verwendete Primitiven in der Common Language Runtime \(CLR\) und anderen Programmiersprachen handelt. In XAML 2009 wurde Unterstützung für die folgenden Primitiven hinzugefügt: `x:Object`, `x:Boolean`, `x:Char`, `x:String`, `x:Decimal`, `x:Single`, `x:Double`, `x:Int16`, `x:Int32`, `x:Int64`, `x:TimeSpan`, `x:Uri`, `x:Byte` und `x:Array`  
  
<a name="previous_techniques_for_language_primitives_in_xaml_markup"></a>   
## Vorherige Techniken für Sprachprimitive in XAML\-Markup  
 In XAML für frühere WPF\-Versionen konnten Sie durch die Zuordnung der Assembly und des Namespace, die eine CLR\-Primitivendefinitionsklasse für .NET Framework enthielten, auf die CLR\-Sprachprimitiven verweisen. Die meisten dieser Primitive befinden sich in der mscorlib\-Assembly und im <xref:System>\-Namespace. Um beispielsweise <xref:System.Int32> zu verwenden, konnten Sie die folgende Zuordnung deklarieren \(anschließend folgt eine Beispielverwendung\):  
  
```  
<Application xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:sys="clr-namespace:System;assembly=mscorlib"> <Application.Resources> <sys:Int32 x:Key="intMeaning">42</sys:Int32> </Application.Resources> </Application>  
```  
  
<a name="xaml_2009_language_primitives"></a>   
## XAML 2009\-Sprachprimitive  
 Gemäß der Konvention werden die Sprachprimitiven für XAML und alle anderen XAML\-Sprachelemente mit dem `x:`\-Präfix angezeigt. So werden XAML\-Sprachelemente in der Regel in realem Markup verwendet. Diese Konvention gilt in der Begriffsdokumentation für XAML in WPF und auch in der XAML\-Spezifikation.  
  
### x:Object  
 Für CLR\-Unterstützung entspricht die `x:Object`\-Primitive <xref:System.Object>.  
  
 Dieser Primitive wird in der Regel nicht in Anwendungsmarkup verwendet, könnte aber für einige Szenarios nützlich sein, wie z. B. die Überprüfung der Zuweisungsfähigkeit in einem XAML\-Typsystem.  
  
### x:Boolean  
 Für CLR\-Unterstützung entspricht die `x:Boolean`\-Primitive <xref:System.Boolean>.  
  
 Wenn XAML Werte für `x:Boolean` analysiert, wird die Groß\-\/Kleinschreibung nicht beachtet. Beachten Sie, dass `x:Bool` keine akzeptierte Alternative ist. Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.17 und 5.4.11](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Char  
 Für CLR\-Unterstützung entspricht die `x:Char`\-Primitive <xref:System.Char>.  
  
 Zeichenfolgen\- und Zeichentypen verfügen über Interaktion mit der Gesamtcodierung der Datei auf XML\-Ebene. Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.7 und 5.4.1](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:String  
 Für CLR\-Unterstützung entspricht die `x:String`\-Primitive <xref:System.String>.  
  
 Zeichenfolgen\- und Zeichentypen verfügen über Interaktion mit der Gesamtcodierung der Datei auf XML\-Ebene. Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.6](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Decimal  
 Für CLR\-Unterstützung entspricht die `x:Decimal`\-Primitive <xref:System.Decimal>.  
  
 Beachten Sie, dass die XAML\-Analyse grundsätzlich in der `en-US`\-Kultur erfolgt. Gemäß der `en-US`\-Kultur ist das richtige Trennzeichen für die Bestandteile einer Dezimalzahl immer ein Punkt \(`.`\), und zwar unabhängig von Kultureinstellungen der Entwicklungsumgebung oder dem tatsächlichen Clientziel, in das die XAML zur Laufzeit geladen wird.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.14 und 5.4.8](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Single  
 Für CLR\-Unterstützung entspricht die `x:Single`\-Primitive <xref:System.Single>.  
  
 Zusätzlich zu den numerischen Werten ermöglicht die Textsyntax für `x:Single` auch die `Infinity`\-, `-Infinity`\- und `NaN`\-Token. Bei diesen Token wird die Groß\-\/Kleinschreibung beachtet.  
  
 `x:Single` kann Werte in wissenschaftlicher Schreibweise unterstützen, wenn das erste Zeichen in der Textsyntax `e` oder `E` ist.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.8 und 5.4.2](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Double  
 Für CLR\-Unterstützung entspricht die `x:Double`\-Primitive <xref:System.Double>.  
  
 Zusätzlich zu den numerischen Werten ermöglicht die Textsyntax für `x:Double` auch die `Infinity`\-, `-Infinity`\- und `NaN`\-Token. Bei diesen Token wird die Groß\-\/Kleinschreibung beachtet.  
  
 `x:Double` kann Werte in wissenschaftlicher Schreibweise unterstützen. Verwenden Sie das Zeichen `e` oder `E`, um den Exponententeil einzuführen.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.9 und 5.4.3](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Int16  
 Für CLR\-Unterstützung entspricht die `x:Int16`\-Primitive <xref:System.Int16>, und `x:Int16` wird als signiert behandelt. In XAML wird das Nichtvorhandensein eines Pluszeichens \(`+`\) in der Textsyntax als positiv signierter Wert impliziert.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.11 und 5.4.5](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Int32  
 Für CLR\-Unterstützung entspricht die `x:Int32`\-Primitive <xref:System.Int32>.`x:Int32` wird als signiert behandelt. In XAML wird das Nichtvorhandensein eines Pluszeichens \(`+`\) in der Textsyntax als positiv signierter Wert impliziert.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.12 und 5.4.6](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Int64  
 Für CLR\-Unterstützung entspricht die `x:Int64`\-Primitive <xref:System.Int64>.`x:Int64` wird als signiert behandelt. In XAML wird das Nichtvorhandensein eines Pluszeichens \(`+`\) in der Textsyntax als positiv signierter Wert impliziert.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.13 und 5.4.7](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:TimeSpan  
 Für CLR\-Unterstützung entspricht die `x:TimeSpan`\-Primitive <xref:System.TimeSpan>.  
  
 Beachten Sie, dass XAML\-Analyse für das Zeitdatumsformat grundsätzlich in der `en-US`\-Kultur erfolgt.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.16 und 5.4.10](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Uri  
 Für CLR\-Unterstützung entspricht die `x:Uri`\-Primitive <xref:System.Uri>.  
  
 Die Überprüfung auf Protokolle ist nicht Bestandteil der XAML\-Definition für `x:Uri`.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.15 und 5.4.9](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Byte  
 Für CLR\-Unterstützung entspricht die `x:Byte`\-Primitive <xref:System.Byte>. Ein <xref:System.Byte> \/ `x:Byte` wird als Zahl ohne Vorzeichen behandelt.  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.10 und 5.4.4](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
### x:Array  
 Für CLR\-Unterstützung entspricht die `x:Array`\-Primitive <xref:System.Array>.  
  
 In XAML 2006 können Sie ein Array mit einer Markuperweiterungssyntax definieren. Die XAML 2009\-Syntax ist dagegen eine sprachdefinierte Primitive, die keinen Zugriff auf eine Markuperweiterung erfordert. Weitere Informationen zur Unterstützung von XAML 2006 finden Sie unter [x:Array Markup Extension](../../../docs/framework/xaml-services/x-array-markup-extension.md).  
  
 Die Definition der XAML\-Sprachspezifikation finden Sie unter [\[MS\-XAML\] Abschnitte 5.2.18](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
<a name="wpf_support"></a>   
## WPF\-Unterstützung  
 In WPF können Sie XAML 2009\-Funktionen verwenden, jedoch nur für XAML, das nicht markupkompiliert ist. Markupkompilierte XAML für WPF und die BAML\-Form von XAML unterstützen die XAML 2009\-Schlüsselwörter und \-Funktionen derzeit nicht.  
  
 Ein Szenario, in dem XAML 2009\-Funktionen mit WPF verwendet werden können, liegt vor, wenn Sie Loose XAML erstellen und dieses XAML dann mit <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName> in eine WPF\-Laufzeit und ein Objektdiagramm laden. Der WPF\-<xref:System.Windows.Markup.XamlReader?displayProperty=fullName> und sein <xref:System.Windows.Markup.XamlReader.Load%2A> können XAML 2009\-Sprachschlüsselwörter und \-Funktionen in eine gültige Objektdiagrammdarstellung verarbeiten.