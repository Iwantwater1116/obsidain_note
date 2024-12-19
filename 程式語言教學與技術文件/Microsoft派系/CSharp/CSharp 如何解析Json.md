#程式語言教學與技術文件 #Microsoft派系 #CSharp
# C#如何解析Json

C#或Dart(物件導向)在解析Json時，會先在Postman那邊求一次API，了解Json的構造後，創建一個結構與Json相同的物件類別，最後解析就直接把值丟到類別內當作新物件，依照剛剛Student的構造來講解看看吧。

```csharp
using System;
using System.IO;//Stream Reader會用到
using Newtonsoft.Json;//C#專門拿來解析Json的套件，請用Nuget下載安裝
using System.Collections.Generic;//List<T>會用到

namespace dotnetcoreconsole
{
    class Program
    {
                //先建立跟Json一模一樣的類別們
        public class Student{
            public string Name{get;set;}
            public string StudentNumber{get;set;}
            public DateTime Birthday{get;set;}
            public string Sex{get;set;}
            public int Effective{get;set;}
        }

                //Class
        public class ClassRoom{
            public List<Student> Students{get;set;}
        }
                
                //讀取Json
        public static ClassRoom LoadJson(){
                        //短暫使用並讀取，避免把檔案鎖死
            using(StreamReader r = new StreamReader("class.json")){
                string json = r.ReadToEnd();//讀取Json
                                //解析Json
                ClassRoom classRoom = JsonConvert.DeserializeObject<ClassRoom>(json);
                return classRoom;//回傳解析後的ClassRomm類別
            }
        }
        static void Main(string[] args)
        {
                        //讀取並解析
            ClassRoom Classroom = LoadJson();
                        //顯示
            foreach(var item in Classroom.Students){
                Console.WriteLine("===========================");
                Console.WriteLine("Name：{0}",item.Name);
                Console.WriteLine("StudentNumber：{0}",item.StudentNumber);
                Console.WriteLine("Birthday：{0}",item.Birthday);
                Console.WriteLine("Sex：{0}",item.Sex);
                Console.WriteLine("Effective：{0}",item.Effective);
                Console.WriteLine("===========================");
            }
        }
    }
}

```