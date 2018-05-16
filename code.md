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
