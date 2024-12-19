#程式語言教學與技術文件 #Microsoft派系 #CSharp 
# ADO.NET Access資料庫記事

這是目前利用ADP.NET與access建立資料庫的一些基本流程與條件：

**範例：**

```csharp
private void Cmb_Series_DropDown(object sender, System.EventArgs e)
{
    OleDbConnection conn = new OleDbConnection(Accdb_Adress);
    DataSet DataSet_1 = new DataSet();
    conn.Open();
    string str1 = "Select* from 機種目錄";
    OleDbDataAdapter adp1 = new OleDbDataAdapter(str1, conn);
    adp1.Fill(DataSet_1, "1a");
    DataTable dt = DataSet_1.Tables["1a"];
    for (int i = 0; i < dt.Rows.Count; i++)
    {
        if (Cmb_Series.FindString(Convert.ToString(dt.Rows[i]["系列"])) == -1)
        {
            Cmb_Series.Items.Add(dt.Rows[i]["系列"]);
        }
    }
    adp1.Dispose();
    conn.Close();
    Cmb_Model.Enabled = true;
}
```

**流程：**

連接資料庫 --> 宣告Dataset物件 -->打開資料庫 --> 抓資料庫中要的資料表 --> 開始使用

1. **引用命名空間**
```csharp
using System.Data;

using System.Data.Oledb;
```

2. **建立連接字串**

```csharp
**** public string Accdb_Adress = "Provider=Microsoft.ACE.Oledb.12.0;Data source=<檔案路徑>"; //(新版本，都能跑)
```

或是

```csharp
public string Accdb_Adress = "Provider=Microsoft.Jet.Oledb.4.0 Data source=<檔案路徑>"; //(較舊版本，只能在X86跑)
```

3.**連接資料庫並開啟**

```csharp
****OleDbConnection conn = new OleDbConnection(Accdb_Adress);
conn.Open();
```

4. **設定要的資料表並且將要的資料表給新的DataSet物件(DataSet可以包含很多DataTable)**

```csharp
string str1 = "Select* from 機種目錄";
OleDbDataAdapter adp1 = new OleDbDataAdapter(str1, conn);
adp1.Fill(DataSet_1, "1a");
```

5. **開始使用**