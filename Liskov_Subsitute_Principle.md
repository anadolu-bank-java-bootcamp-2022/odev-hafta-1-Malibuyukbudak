Alt seviye sınıflardan oluşan nesnelerin/sınıfların, ana(üst) sınıfın nesneleri ile yer değiştirdikleri zaman, aynı davranışı sergilemesi gerekmektedir. 

Türetilen sınıflar, türeyen sınıfların tüm özelliklerini kullanabilmelidir.

Örnek;

    namespace LiskovSubstitutionPrinciple
    {
        public abstract class Computer : 
        {
            public string Run()
            {
                return "Bilgisayar çalıştırıldı.";
            }

            public abstract string OpenCdRom();
        }
    }

Burada bir adet bilgisayar sınıfı var ve iki adet soyut olarak tanımlanmış methodu bulunuyor. Run methodu bilgisayar çalıştıracak OpenCdRom methodu ise cd yerine açacak.  

    public class Asus : Computer
        {
        public override string Run(){
        
        return "Bilgisayar Çalıştı";

        }
            public override string OpenCdRom()
            {
                return "Cd açıldı.";
            }
        }

        public class Lenovo : Computer
        {
            public override string Run (){
            
            return "Bilgisayar Çalıştı";
            
            }
        
            public override string OpenCdRom()
            {
                throw new NotImplementedException();
                //return null;
            }
        }

Lenovo' in dikkat edilirse kliması olmadığı için null geçilmiş ancak ilerde bir başka bir yazılımcı aşağıdaki gibi kodlama yapılırsa sorunlar çıkabilir.

    static void Main(string[] args)
            {
                Computer computer = new Asus();
                computer.Run();
                computer.OpenCdRom();
                // Sıkıntı yok her şey yolunda.

                Computer computer1 = new Lenovo();
                computer1.Run();
                computer1.OpenCdRom(); // ?
            }
Liskov'a göre alt sınıflardan oluşan nesnelerin üst sınıfın nesneleri ile yer değiştirdikleri zaman, aynı davranışı sergilemesini beklemektir. Bu durumda murat131 bu davranışı göstermiyor.


Alttaki gibi refactor edebiliriz.

using System;

    namespace LiskovSubstitutionPrinciple
    {
        public interface IOpenCdRom
        {
            string OpenCdRom();
        }

        public abstract class Computer
        {
            public string Run()
            {
                return "Bilgisayar Çalıştı";
            }
        }

        public class Asus : Computer, IOpenCdRom
        {
            public string OpenCdRom()
            {
                return "Cd açıldı.";
            }
        }

        public class Lenovo : Computer
        {
            public override string Run()
            {
                return "Bilgisayar Çalıştı.";
            }
        }

    }

