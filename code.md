# testing
#CK1 checkBox name
Private Sub CK1_CheckedChanged(sender As Object, e As EventArgs) Handles CK1.CheckedChanged
    If CK1.Checked = True Then
        Try
            Dim I As Integer
            For I = 0 To Dgrd.Rows.Count - 1
                Dim CHKRow As DataGridViewCheckBoxCell = Dgrd.Rows(I).Cells(0)
                If CHKRow.Value = False Then
                    CHKRow.Value = True
                End If
            Next
        Catch ex As Exception
        End Try
    Else
        Try
            Dim I As Integer
            For I = 0 To Dgrd.Rows.Count - 1
                Dim CHKRow As DataGridViewCheckBoxCell = Dgrd.Rows(I).Cells(0)
                If CHKRow.Value = True Then
                    CHKRow.Value = False
                End If
            Next
        Catch ex As Exception
        End Try
    End If
End Sub
####################################################################################

Public Class Form1
    Dim mySqlCon As Data.OleDb.OleDbConnection
    Dim mySqlCmd As Data.OleDb.OleDbCommand
    Dim mySqlReader As Data.OleDb.OleDbDataReader
    Dim SQL As String

    Dim dataLineItem As DataTable
    Dim editLine As Integer
    Private Sub connectDB()

        ' connect to database
        Dim sConnString As String

        'sConnString = "Provider=SQLOLEDB.1;Data Source=SERVER_NAME;" & _
        '              "Initial Catalog=DB_NAME;User ID=USER;Password=PASSWORD"
        sConnString = "Provider=SQLOLEDB.1;Data Source=AUTOMATION-PC\SQLEXPRESS;" & _
                      "Initial Catalog=test;User ID=ok;Password=ok"

        mySqlCon = New Data.OleDb.OleDbConnection(sConnString)

    End Sub
    Protected Sub updateGridLineItem()
        ' Copy data from Collection to DataTable
        If (dataLineItem Is Nothing) Then
            dataLineItem = New DataTable("Name")
            dataLineItem.Columns.Add(New DataColumn("ID"))

           
        End If
        DataGrid.DataSource = dataLineItem
        

    End Sub
    Public Sub showLine(ByVal Name)
        'Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        '    connectDB()
        mySqlCon.Open()

        Dim command As Data.OleDb.OleDbCommand = New Data.OleDb.OleDbCommand()
        command.Connection = mySqlCon
        command.CommandText = "SELECT * FROM Student"
        command.Parameters.Add("Name", Data.OleDb.OleDbType.VarChar, 10)
        command.Parameters(0).Value = Name
        command.Prepare()
        command.ExecuteNonQuery()
        Try

            mySqlReader = command.ExecuteReader()
            While mySqlReader.Read()
                Dim dr As DataRow
                dr = dataLineItem.NewRow()
                dr("Name") = mySqlReader.Item(0)
                dr("ID") = mySqlReader.Item(1)

                dataLineItem.Rows.Add(dr)
            End While
            'Session("dataLineItem") = dataLineItem
        Catch ex As Exception
            MsgBox("connect")
        End Try

        mySqlCon.Close()

    End Sub


    Private Sub CK1_CheckedChanged(sender As Object, e As EventArgs) Handles ChBox.CheckedChanged
        If ChBox.Checked = True Then
            Try
                Dim I As Integer
                For I = 0 To DataGrid.Rows.Count - 1
                    Dim CHKRow As DataGridViewCheckBoxCell = DataGrid.Rows(I).Cells(0)
                    If CHKRow.Value = False Then
                        CHKRow.Value = True
                    End If
                Next
            Catch ex As Exception
                MsgBox("ok")

            End Try
        Else
            Try
                Dim I As Integer
                For I = 0 To DataGrid.Rows.Count - 1
                    Dim CHKRow As DataGridViewCheckBoxCell = DataGrid.Rows(I).Cells(0)
                    If CHKRow.Value = True Then
                        CHKRow.Value = False
                    End If
                Next
            Catch ex As Exception
                MsgBox("No")
            End Try
        End If
    End Sub

    'Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
    '    showLine()

    'End Sub



End Class
