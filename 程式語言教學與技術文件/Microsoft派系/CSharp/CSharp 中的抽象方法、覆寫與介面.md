#程式語言教學與技術文件 #Microsoft派系 #CSharp #理論 #物件導向
# C#中的抽象方法、覆寫與介面

# 物件導向OOP的再深入探討

C# 畢竟也是物件導向程式，依然有物件導向的特性，所以也會有類別、物件、繼承、多型、多載跟覆寫的能力，一般最常使用到的就是物件(Object)跟類別(Class)，其次會用到繼承，最後寫方法時才會用到所謂的多型、多載跟覆寫的功能，簡單說一下這三個：

- 覆寫(Override)：相同物件，相同函式名可以有不同的程式碼運作。
- 多載(Overload)：相同函式名可以有不同的參數輸入型別、樣式與數量。
- 多型(Polymorphism)：一個類別可以有不同的形態，父類別是子類別的通用格式，而子類別又可以利用覆寫跟參數變更來達到跟父類別相似卻又完全不同的樣子，以達到多型的特色，完成多型，其中一定少不了繼承的幫助。

# 抽象類別的出現

一般來說，大部分的類別都會直接實作，但當專案越來越大時，相似卻又完全不同的架構也會開始接踵而來，例如生產部跟採購部雖然完全不同，但一個是生產產品賣出去賺，一個是花錢把設備買進來，但請購單跟訂單這兩個形式上不同，但本質上一樣的狀況，抽象類別(abstract class)就是個很好的方式，抽象類別並不能直接使用，必須繼承在可實作的類別上才可以運作，但抽象類別卻大大的改善實作類別在大型系統的宣告麻煩度，也讓每個大單元的功能價透能更加清晰明瞭。

# 什麼是介面?

介面主要體現在OOP當中「組合」的部分，讓所有繼承這個介面的物件去實作他所有的定義，以便無論在哪個地方或哪個功能，都可以有相對應但卻是相同名稱的模組可以去做呼叫。介面一般使用在方法的接口上，但其實是可以宣告定義變數(const)或靜態(static)變數的。

舉個最好的例子，之前撰寫Xamarin.Forms的時候，iOS跟Android在處理陰影或是上傳東西時的處理方式不同，當時就是在Xamarin.Forms的主專案資料夾下建立Interface，並在其他的iOS/Android的資料夾下建立Interface的對應繼承函式並個別處理iOS跟Android的相關功能以達到跨平台使用的能力，這就是一種介面的展現。

不過因為Xamarin.Forms的資料夾分開，需要彼此做協調，才需要利用其他的方式(Dependency)去宣告這個東西依賴於XamarinForms的某個介面，這樣這個Interface才會知道要去找誰做繼承處理。

# 抽象類別又是什麼?

先說類別，類別主要是體現OOP當中「繼承」的部分，只要是繼承於類別的，無論是變數、函式、靜態、動態，全部都會被完整繼承下來，無論是不是抽象都有這個特性，所以當類別一被繼承，就不需要再幫他寫函式，因為他連函式內的功能都會被繼承下來，不過類別有所謂「覆寫」的能力，可以利用覆寫幫已經被繼承的類別做出相同名稱特性，但內容物卻不一樣的函式，達到「多型」的效果。至於抽象類別，雖然跟類別有完全一樣的特性，但卻是不能直接拿來使用的類別，畢竟是抽象阿，所以他必須依附在實際被建立出來的類別裡做繼承，才能拿來使用。

# 抽象類別跟介面的不同

抽象類別跟介面一樣都需要依附在實體上才可以真正拿來用，最大的不同是，介面必須強迫開發者實作一個跟他一樣的函式實體才可以，而抽象類別可以不需要，但也可以用覆寫做這件事，因為抽象類別本身就有函式定義，而介面只是個接口，他並沒有真正的函式在裡面。

# 實作程式碼說明

```csharp

using System;
using System.Collections.Generic;

namespace NotionTest
{
    class Program
    {
        //1. 先創建一個抽象類別為門，這東西是不能單獨做使用的
        abstract class Door
        {
            public virtual void Open()
            {
                Console.WriteLine("Open Door");
            }

            public virtual void Close()
            {
                Console.WriteLine("Close Door");
            }
        }

        //這個實體的水平門繼承了門的特性，也因為抽象類別被實體繼承了，所以他可以用
        class HorizontalDoor : Door { }

        //這個實體垂直門繼承門的特性，不單被實體繼承，也實作了門的所有方法，所以他繼承了門的特性，還擁有跟門完全不同的行為(多型)
        class VerticalDoor : Door
        {
            public override void Open()
            {
                Console.WriteLine("Open vertically");
            }

            public override void Close()
            {
                Console.WriteLine("Close vertically");
            }
        }

        //建立一個介面是鈴鐺(介面)
        interface IAlarm
        {
            void Alert();
        }

        //實作一個類別門鈴，而他繼承於鈴鐺介面(介面)
        class Alarm : IAlarm
        {
            public void Alert()
            {
                Console.WriteLine("Ring~~");
            }
        }

        //實作一個繼承門特性的門鈴門
        class AlarmDoor : Door
        {
            private IAlarm _alarm;
            public AlarmDoor()
            {
                _alarm = new Alarm();//初始化的時候就建立一個新的門鈴
            }

            public void Alert()//另外獨立實作Alert
            {
                _alarm.Alert();//呼叫Alarm中的Alert，而Alarm中的Alert是繼承於Interface的IAlarm
            }
        }
        //實作一個繼承門鈴門特性的自動門鈴門
        class AutoAlarmDoor : AlarmDoor
        {
            //繼承於AlarmDoor，而AlarmDoor繼承於Door，理所當然他也有Door的特性，所以可以開啟Door
            //當然也可以覆寫父類別的開門動作(覆寫)
            public override void Open()
            {
                base.Open();//啟用父類別Door本身的Open
                Alert();//這個是繼承於AlarmDoor
            }
        }
        //建立一個門鈴控制器類別
        class DoorController
        {
            protected List<Door> _dootList = new List<Door>();//建立一個門List
            public void AddDoor(Door Door)
            {
                _dootList.Add(Door);//把門加入控制器群組
            }

            public void OpenDoor()
            {
                foreach (var item in _dootList)
                {
                    item.Open();//叫所有門開門
                }
            }
        }

        static void Main(string[] args)
        {
            DoorController dc = new DoorController();//建立一個控制器
            dc.AddDoor(new HorizontalDoor());//建立一個新的水平門
            dc.AddDoor(new VerticalDoor());//建立一個新的垂直門
            dc.AddDoor(new AlarmDoor());//建立一個新的門鈴門
            dc.AddDoor(new AutoAlarmDoor());//建立一個新的自動門鈴門

            dc.OpenDoor();//全部給我開門
            Console.ReadLine();
        }
    }
}

```