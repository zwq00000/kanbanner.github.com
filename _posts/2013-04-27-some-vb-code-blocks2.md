---
layout: post
title: "Some VB Code Blocks(2)..."
---

{% highlight vbnet %}
'数据驱动图形展示, 数据区块连续示例
Sheets(sheetName).Activate
'既存图表名称: EVMChart
ActiveSheet.ChartObjects("EVMChart").Activate
'数据源: Sheet("DATA").Range("A4-D/weekno"), 横坐标: A列/数据列: BCD共3列, 显示3个SeriesCollection
ActiveChart.SetSourceData Source:=Range("'DATA'!$A$4:$D$" & weekno)
'A4:B/weekno
ActiveChart.SeriesCollection(1).Formula = "=SERIES(""PV"",'DATA'!$A$4:$A$" & weekno & ",'DATA'!$B$4:$B$" & weekno & ",1)"
'A4:C/weekno
ActiveChart.SeriesCollection(2).Formula = "=SERIES(""AC"",'DATA'!$A$4:$A$" & weekno & ",'DATA'!$C$4:$C$" & weekno & ",2)"
'A4:D/weekno
ActiveChart.SeriesCollection(3).Formula = "=SERIES(""EV"",'DATA'!$A$4:$A$" & weekno & ",'DATA'!$D$4:$D$" & weekno & ",3)"

'数据驱动图形展示, 数据区块不连续示例

'既存图表名称: RISKChart
ActiveSheet.ChartObjects("RISKChart").Activate
'数据源: Sheet("DATA")的A4-A/weekno和E4-E/weekno, 横坐标: A列/数据列: E列, 显示1个SeriesCollection
Dim riskrange As Range
Set riskrange = Application.Union(Sheets("DATA").Range("$A$4:$A$" & weekno), Sheets("DATA").Range("$E$4:$E$" & weekno))
ActiveChart.SetSourceData Source:=riskrange
ActiveChart.SeriesCollection(1).Formula = "=SERIES(""Risk"",'DATA'!$A$4:$A$" & weekno & ",'DATA'!$E$4:$E$" & weekno & ",1)"

ActiveSheet.Range("A1").Select
'注意: EXCEL图表默认(自动产生其它SeriesCollection)保持SourceData中“数据列”和“SeriesCollection”一致.


'ADO数据库表格化处理Excel Sheet数据
Sub DoWhoWant()
    Dim deptStr As String
    sheetName = "Sheet1"
    deptStr = Worksheets(sheetName).Range("B2")
    
    Dim conn As Object
    Set conn = getConn
    
    Dim dateStr1 As String, dateStr2 As String
    dateStr2 = "2013/08/31"
    dateStr1 = Left(dateStr2, InStrRev(dateStr2, "/")) & "1"
    dateStr2 = "#" & dateStr2 & "#"
    dateStr1 = "#" & dateStr1 & "#"
        
    Dim linesStr
    linesStr = getLines(conn, "DATA", deptStr, dateStr1, dateStr2)
    
    conn.Close
    Set conn = Nothing
    
    MsgBox "Done!"

End Sub

'获取数据连接
Function getConn() As Object
    Dim conn As Object
    Set conn = CreateObject("ADODB.Connection")
    
    With conn
        .Provider = "Microsoft.ACE.OLEDB.12.0"
        .Properties("Extended Properties").Value = "Excel 12.0 Macro;HDR=YES;"
        .Open "Data Source = D:\费用明细.xlsm"
    End With
    Set getConn = conn
End Function

'获取数据集对象
Function getRs(conn, sql) As Object
    Dim rs As Object
    Set rs = CreateObject("ADODB.Recordset")
    
    With rs
        .Source = sql
        .ActiveConnection = conn
        .CursorLocation = adUseClient
        .CursorType = adOpenForwardOnly
        .LockType = adLockReadOnly
        .Open
    End With
    Set getRs = rs
End Function


'前3个最多的飞行行程 by 部门和出票日期
Function getLines(conn, sheetName, deptStr, dateStr1, dateStr2)
    Dim sSQL As String
    sSQL = "SELECT [行程], Count([行程]) FROM [" & sheetName & "$] WHERE [客户部门] = '" & deptStr & "'and [出票日期] >= " & dateStr1 & " and [出票日期] <= " & dateStr2 & " group by [行程] order by Count([行程]) desc"
    '"SELECT * FROM [Sheet1$A1:B10]"
    
    Dim rs As Object
    Set rs = getRs(conn, sSQL)
    
    Dim result As String, i As Integer
    result = ""
    While Not rs.EOF And i <= 2
        result = result & rs.Fields(0).Value & "(" & rs.Fields(1).Value & ")" & vbCrLf
        i = i + 1
        rs.MoveNext
    Wend
    
    rs.Close
    Set rs = Nothing
    
    getLines = result
    
End Function
{% endhighlight %}