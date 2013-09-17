---
layout: post
title: "Some VB Code Blocks(1)..."
---

{% highlight vbnet %}
'读块
Dim countRows, countCols, codes
'Sheet("DATA")有countRows行数据
countRows = Worksheets("DATA").UsedRange.Rows.count
'Sheet("DATA")有countCode行数据
countCols = Worksheets("DATA").UsedRange.Columns.count
'Sheet("DATA")从A1位置，读countRows行，countCols列数据块到二维数组codes
codes = Worksheets("DATA").Range("A1").Resize(countRows, countCols).Value

'写块
Dim matrix
ReDim matrix(1 To countRows, 1 To countCols)'countRows行, countCols列
'Sheet("Report")从B3位置开始写countRows行, countCols列; 取值: 二维数组matrix
Worksheets("Report").Range("B3").Resize(countRows, countCols) = matrix
{% endhighlight %}

{% highlight vbnet %}
'数字转EXCEL列头, 如: 1->A, 2->B, ... 27->AA
Function NUM2APH(intx)
  Dim modX As Integer
  modX = intx \ 27
  If modX >= 1 Then
    NUM2APH = Chr(modX + 64) & Chr(intx - modX * 26 + 64)
  Else
    NUM2APH = Chr(intx + 64)
  End If
End Function
{% endhighlight %}

{% highlight vbnet %}
'regexp.test
Function ExpTest(str As String, strPattern As String, _
                				 blnIgnoreCase As Boolean) As Boolean
  Dim regEX As Object
  Set regEX = CreateObject("VBSCRIPT.REGEXP")
  regEX.Global = True
  regEX.Pattern = strPattern
  regEX.ignoreCase = blnIgnoreCase
  ExTest = regEX.Test(str)
  Set regEX = Nothing
End Function
{% endhighlight %}

{% highlight vbnet %}
'Return Timed(yyyyMMdd) GUID(Globally Unique Identifier) without "-"
Public Function getTimedGUID() As String
  Dim guidStr 
  guidStr = Mid(CreateObject("Scriptlet.TypeLib").GUID, 2, 36)
  getTimedGUID = Format(Date, "yyyyMMdd") + Replace(guidStr, "-", "")
End Function
{% endhighlight %}

{% highlight vbnet %}
'dictionary ops
Function dictOPs()
  Dim dict, i
  Set dict = CreateObject("Scripting.Dictionary")
  For i = 1 To 100
    dict.Add "K:" + CStr(i), "V:" + CStr(100 - i)
  Next
  
  Dim k, v, Key, Value 
  k = dict.keys
  v = dict.Items
  For i = 0 To dict.count - 1
    Key = k(i)
    Value = v(i) 'dict.Item(Key)
    Debug.Print Key & "=" & Value
  Next
End Function
{% endhighlight %}